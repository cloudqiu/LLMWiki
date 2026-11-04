---
title: "10 Rust Crates Every Developer Should Know in 2026"
source: "https://rustify.rs/articles/10-rust-crates-every-developer-should-know-2026"
author:
  - "[[Max Wells]]"
published: 2026-07-10
created: 2026-11-04
description: "The Rust ecosystem has 150,000+ crates, but 10 dominate professional development. This guide covers the essentials for serialization, async, web, and testing."
tags:
  - "clippings"
---
The Rust ecosystem has 150,000+ crates: but 10 dominate professional Rust development. This guide covers the essential crates for serialization, async, web, error handling, CLI, testing, and more.

**Most professional Rust developers spend 90% of their time with the same 10 crates: mastering them is the fastest path to reading and contributing to any Rust codebase at production scale.**

*By Max Wells, updated July 2026*

> **TL;DR**: Most professional Rust code uses the same ~10 crates. Learn these and you can read and contribute to almost any Rust project. Combined download count: over 10 billion. All are actively maintained, semver-stable, and production-tested at scale.
> 
> - **serde**: serialization/deserialization: the most downloaded Rust crate, ~700M downloads
> - **tokio**: async runtime: powers axum, sqlx, reqwest, tonic, and almost all async Rust
> - **anyhow** + **thiserror**: error handling duo: every project uses one or both
> - **clap**: CLI argument parsing: 200M+ downloads, derive-based
> - **rayon**: data parallelism: `.par_iter()` turns sequential loops into parallel with one word

---

## Who Should Read This?

This article is written for working developers: backend engineers with 2–8 years of experience in Python, Go, TypeScript, or Java who are moving into Rust professionally or evaluating it for a new project. You have already written some Rust code but are uncertain which third-party crates are worth your time to learn deeply. You may be a mid-level engineer targeting your first Rust role (US median: $155K–$185K) or a senior engineer ($185K–$230K) looking to expand your production toolkit. This guide skips the toy examples and focuses on the crates you will actually see in pull requests, architecture documents, and job interview code challenges at companies that run Rust in production.

---

## Why Do These 10 Crates Matter?

**Ten crates account for the vast majority of third-party dependencies in production Rust code: knowing them gives you an immediate ability to read and contribute to almost any Rust project.**

The Rust ecosystem has over 150,000 published crates on crates.io, but the distribution is heavily concentrated. Walk through the dependency trees of any production Rust project and you will find serde, tokio, anyhow or thiserror, and clap appearing in virtually every one. This concentration exists because Rust's compile-time guarantees make it expensive to switch foundational dependencies once chosen: teams converge on well-audited, stable crates and stay there. Understanding why each crate exists, what problem it solves, and when to reach for it separates developers who can navigate real Rust codebases from those who only know the language syntax.

---

## 1\. serde: Serialization and Deserialization

**serde is the foundational data serialization library in Rust: it powers JSON, TOML, YAML, MessagePack, and 50+ other format crates through a shared derive interface.**

Downloads: ~700M | Dependents: ~100K crates

```toml
[dependencies]
serde = { version = "1", features = ["derive"] }
serde_json = "1"
toml = "0.8"
```
```rust
use serde::{Deserialize, Serialize};
 
#[derive(Serialize, Deserialize, Debug)]
struct Config {
    host: String,
    port: u16,
    features: Vec<String>,
}
 
// Serialize to JSON
let config = Config { host: "localhost".into(), port: 8080, features: vec!["auth".into()] };
let json = serde_json::to_string_pretty(&config)?;
 
// Deserialize from JSON
let config: Config = serde_json::from_str(&json)?;
 
// Same struct, different format: no code change
let toml_str = toml::to_string(&config)?;
let config: Config = toml::from_str(&toml_str)?;
```

If you only learn one Rust crate outside the standard library, learn serde. It's in virtually every Rust project. The derive macros generate efficient serialization code at compile time: no reflection, no runtime overhead. The same `#[derive(Serialize, Deserialize)]` annotation works with any compatible format crate: JSON, TOML, YAML, MessagePack, CBOR, and dozens more.

---

## 2\. tokio: Async Runtime

**tokio is the async runtime that executes `async/await` code: it provides a thread pool, I/O multiplexing, timers, channels, and synchronization primitives.**

Downloads: ~400M | Dependents: ~60K crates

```toml
[dependencies]
tokio = { version = "1", features = ["full"] }
```
```rust
use tokio::time::{sleep, Duration};
use tokio::sync::mpsc;
 
#[tokio::main]
async fn main() {
    // Concurrent tasks
    let (tx, mut rx) = mpsc::channel::<String>(100);
 
    // Spawn background task
    tokio::spawn(async move {
        for i in 0..5 {
            sleep(Duration::from_millis(100)).await;
            tx.send(format!("message {}", i)).await.unwrap();
        }
    });
 
    // Receive messages
    while let Some(msg) = rx.recv().await {
        println!("Received: {}", msg);
    }
}
```

Almost all async Rust crates (axum, sqlx, reqwest, tonic) are built on tokio. Learn tokio's channels, `spawn`, and `select!` and you can work with the whole async ecosystem.

Tokio uses a work-stealing scheduler that distributes tasks across multiple OS threads. For most web and network services, the `"full"` feature flag is appropriate. For embedded or resource-constrained environments, `"current-thread"` provides a single-threaded executor. The `tokio::sync` module provides async-aware Mutex, RwLock, Semaphore, and Barrier types that correctly yield control to the scheduler instead of blocking a thread.

---

## 3\. anyhow: Application Error Handling

**anyhow provides `Result<T, anyhow::Error>`: a flexible error type that accepts any `std::error::Error` and adds context messages. It's the standard choice for application-level error handling.**

Downloads: ~200M | Best for: binary applications (not libraries)

```toml
[dependencies]
anyhow = "1"
```
```rust
use anyhow::{Context, Result};
 
fn read_config(path: &str) -> Result<Config> {
    let content = std::fs::read_to_string(path)
        .with_context(|| format!("Failed to read config file: {}", path))?;
 
    let config: Config = serde_json::from_str(&content)
        .context("Failed to parse config JSON")?;
 
    Ok(config)
}
 
fn main() -> Result<()> {
    let config = read_config("config.json")?;
    println!("Running on port {}", config.port);
    Ok(())
}
```

Error output: `Error: Failed to read config file: config.json\n\nCaused by:\n    No such file or directory (os error 2)`

The `.context()` and `.with_context()` methods attach human-readable messages to any error while preserving the original cause. This produces error chains that are genuinely useful for debugging in production: you see both what went wrong and why. For binaries and services, anyhow is almost always the right choice because callers are humans or log aggregators, not code that matches specific error variants.

---

## 4\. thiserror: Library Error Handling

**thiserror generates the `std::error::Error` boilerplate for custom error types: the standard choice for library crates that need structured, typed errors.**

Downloads: ~200M | Best for: library crates

```toml
[dependencies]
thiserror = "2"
```
```rust
use thiserror::Error;
 
#[derive(Error, Debug)]
pub enum DatabaseError {
    #[error("Connection failed: {url}")]
    ConnectionFailed { url: String },
 
    #[error("Query failed: {0}")]
    QueryFailed(String),
 
    #[error("Record not found: id={id}")]
    NotFound { id: i64 },
 
    // Wrap another error transparently
    #[error(transparent)]
    Io(#[from] std::io::Error),
}
 
// Usage: match on specific variants
fn handle_error(err: DatabaseError) {
    match err {
        DatabaseError::NotFound { id } => eprintln!("No record with id={}", id),
        DatabaseError::ConnectionFailed { url } => eprintln!("Can't connect to {}", url),
        _ => eprintln!("Database error: {}", err),
    }
}
```

Rule: use `thiserror` in library crates (where callers need to match specific errors), use `anyhow` in application binaries (where you just need good error messages).

The `#[from]` attribute automatically generates `From` implementations that let you use `?` to convert from the source error type. The `#[error(transparent)]` attribute forwards both the display and source implementations to the wrapped error, making it invisible to callers who just need the error chain.

---

## 5\. clap: CLI Argument Parsing

**clap is Rust's standard CLI argument parsing library: the derive API turns annotated structs into fully-featured CLIs with help text, shell completions, and validation.**

Downloads: ~200M

```toml
[dependencies]
clap = { version = "4", features = ["derive"] }
```
```rust
use clap::{Parser, Subcommand};
 
#[derive(Parser)]
#[command(version, about = "My tool")]
struct Cli {
    #[arg(short, long)]
    verbose: bool,
 
    #[command(subcommand)]
    command: Commands,
}
 
#[derive(Subcommand)]
enum Commands {
    /// Search for pattern in files
    Search { pattern: String },
    /// Build the project
    Build { #[arg(long)] release: bool },
}
 
fn main() {
    let cli = Cli::parse();
    match cli.command {
        Commands::Search { pattern } => println!("Searching for: {}", pattern),
        Commands::Build { release } => println!("Building (release: {})", release),
    }
}
```

Clap automatically generates `--help`, `--version`, error messages with suggested corrections, and shell completion scripts for bash, zsh, and fish. The derive API means your argument parser is defined entirely in your data structures: no separate parsing logic to maintain. Adding a field to your `Cli` struct adds it to the CLI automatically.

---

## 6\. rayon: Data Parallelism

**rayon makes data-parallel programming trivial: replace `.iter()` with `.par_iter()` and your loop runs on all CPU cores. It uses a work-stealing thread pool and is safe by construction.**

Downloads: ~100M

```toml
[dependencies]
rayon = "1"
```
```rust
use rayon::prelude::*;
 
fn main() {
    let data: Vec<i64> = (0..10_000_000).collect();
 
    // Sequential: uses one core
    let sum: i64 = data.iter().map(|&x| x * x).sum();
 
    // Parallel: uses all cores, same result, ~4-8x faster
    let par_sum: i64 = data.par_iter().map(|&x| x * x).sum();
 
    assert_eq!(sum, par_sum);
 
    // Parallel sort
    let mut sorted = data.clone();
    sorted.par_sort();
}
```

rayon automatically handles load balancing, thread pool management, and safe data sharing: there's no unsafe code required to use it.

The thread pool size defaults to the number of logical CPU cores. Operations like `par_sort`, `par_iter().filter().collect()`, and `par_chunks()` all produce correct results guaranteed by Rust's type system. If your closure captures data that is not `Send`, rayon will refuse to compile the parallel version: preventing data races at compile time rather than runtime.

---

## 7\. reqwest: HTTP Client

**reqwest is Rust's most-used HTTP client: async, TLS-enabled by default, cookie-aware, and streaming. Built on hyper + tokio.**

Downloads: ~150M

```toml
[dependencies]
reqwest = { version = "0.12", features = ["json"] }
tokio = { version = "1", features = ["full"] }
```
```rust
use reqwest::Client;
use serde::Deserialize;
 
#[derive(Deserialize)]
struct Post { id: u32, title: String }
 
#[tokio::main]
async fn main() -> Result<(), reqwest::Error> {
    let client = Client::new();
 
    // GET with JSON deserialization
    let posts: Vec<Post> = client
        .get("https://jsonplaceholder.typicode.com/posts")
        .send()
        .await?
        .json()
        .await?;
 
    println!("Got {} posts, first: {}", posts.len(), posts[0].title);
    Ok(())
}
```

The `Client` struct maintains a connection pool: create it once and reuse it across requests for performance. For blocking contexts where you cannot use async, the `reqwest::blocking` module provides a synchronous API. The `json()` feature enables automatic serde deserialization from response bodies.

---

## 8\. tracing: Structured Logging and Instrumentation

**tracing is Rust's structured logging library: it captures events with structured fields (not plain strings) and integrates with async tasks, spans, and distributed tracing (OpenTelemetry).**

Downloads: ~200M

```toml
[dependencies]
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }
```
```rust
use tracing::{debug, error, info, instrument, warn};
 
// Instrument functions: spans capture duration and context
#[instrument(skip(password))]
async fn login(username: &str, password: &str) -> Result<String, String> {
    info!(username, "Login attempt");
 
    if username == "admin" && password == "secret" {
        info!(username, "Login successful");
        Ok("token-abc".to_string())
    } else {
        warn!(username, "Login failed: invalid credentials");
        Err("Invalid credentials".into())
    }
}
 
fn main() {
    // Initialize subscriber (respects RUST_LOG env var)
    tracing_subscriber::fmt()
        .with_env_filter("info")
        .init();
 
    tokio::runtime::Runtime::new().unwrap().block_on(async {
        let _ = login("admin", "secret").await;
    });
}
```

The `#[instrument]` macro automatically creates a span around the function, recording its arguments (with the ability to skip sensitive ones), and propagating the span context across async await points. This means distributed traces work correctly even when an async function is interrupted and resumed on a different thread.

---

## 9\. axum: Web Framework

**axum is Rust's most popular web framework in 2026: built on tokio + hyper + tower, with type-safe routing, extractor-based handlers, and seamless middleware.**

Downloads: ~80M

```toml
[dependencies]
axum = "0.8"
tokio = { version = "1", features = ["full"] }
serde = { version = "1", features = ["derive"] }
```
```rust
use axum::{routing::get, Json, Router};
use serde::Serialize;
 
#[derive(Serialize)]
struct Status { status: &'static str, version: &'static str }
 
async fn health() -> Json<Status> {
    Json(Status { status: "ok", version: "1.0.0" })
}
 
#[tokio::main]
async fn main() {
    let app = Router::new().route("/health", get(health));
    let listener = tokio::net::TcpListener::bind("0.0.0.0:3000").await.unwrap();
    axum::serve(listener, app).await.unwrap();
}
```

Axum's extractor system is its most distinctive feature: handler function arguments are automatically populated from the request (path parameters, query strings, JSON bodies, headers) by the type system. If you add a `Json<MyPayload>` argument to a handler, axum automatically parses the request body as JSON and returns a 422 error if parsing fails. No manual extraction code required.

---

## 10\. sqlx: Async Database Client

**sqlx provides compile-time verified SQL queries: the macro checks your SQL against a real database at compile time, so query typos and type mismatches are compile errors, not runtime errors.**

Downloads: ~80M

```toml
[dependencies]
sqlx = { version = "0.8", features = ["runtime-tokio", "postgres"] }
tokio = { version = "1", features = ["full"] }
```
```rust
use sqlx::postgres::PgPool;
 
#[derive(sqlx::FromRow)]
struct User { id: i64, name: String }
 
#[tokio::main]
async fn main() -> Result<(), sqlx::Error> {
    let pool = PgPool::connect("postgres://user:pass@localhost/db").await?;
 
    // Compile-time verified SQL: typos are compile errors
    let users = sqlx::query_as!(User, "SELECT id, name FROM users WHERE active = true")
        .fetch_all(&pool)
        .await?;
 
    for user in users {
        println!("{}: {}", user.id, user.name);
    }
    Ok(())
}
```

The `query!` and `query_as!` macros connect to your database at compile time (using the `DATABASE_URL` environment variable) and verify that your SQL is syntactically valid, references real tables and columns, and returns types that match your Rust structs. For CI environments without a database, the `sqlx prepare` command saves a JSON snapshot of query metadata so the build can proceed offline.

---

## Honorable Mentions

| Crate | Purpose |
| --- | --- |
| `uuid` | UUID generation (v4, v7) |
| `chrono` | Date/time handling |
| `regex` | Regular expressions |
| `itertools` | Extra iterator adapters |
| `once_cell` / `std::sync::OnceLock` | Lazy statics (OnceLock is now in std) |
| `bytes` | Efficient byte buffer operations |
| `crossbeam` | Advanced concurrent data structures |
| `dashmap` | Concurrent HashMap |
| `parking_lot` | Faster Mutex/RwLock than std |
| `criterion` | Benchmarking |

---

## What Common Mistakes Do Rust Developers Make When Choosing Crates?

**Developers new to Rust often pick crates based on familiarity with other ecosystems rather than understanding Rust's own well-established conventions, leading to fragile or poorly integrated codebases.**

- **Using a custom error type with `Box<dyn Error>` instead of `anyhow` or `thiserror`.** `Box<dyn Error>` is valid but loses the ability to attach context messages or match specific error variants. Teams that skip `anyhow` / `thiserror` usually end up reinventing a worse version of them. Pick one based on whether you are writing a library or an application binary.
- **Spawning a new `tokio::runtime::Runtime` inside a function instead of using the existing runtime.** This creates a nested runtime which panics in Tokio 1.x. If you need to call async code from sync code inside an already-running runtime, use `tokio::task::block_in_place` or `tokio::runtime::Handle::current().block_on(...)`.
- **Not enabling the `derive` feature for serde.** The derive macros (`Serialize`, `Deserialize`) are opt-in for compile-time reasons. Forgetting `features = ["derive"]` produces a confusing error: the trait exists but the derive macro does not. Always add the feature explicitly.
- **Using `reqwest::get()` (the free function) in a loop instead of a shared `Client`.** The free function creates a new client with a new connection pool on every call. For repeated requests, create one `Client::new()` and clone or share it: HTTP connection reuse dramatically reduces latency and resource usage.
- **Choosing `actix-web` by default because it was historically fastest.** Both axum and actix-web are extremely fast in 2026: the gap is negligible for most production workloads. Axum's tight integration with the tower ecosystem (middleware, rate limiting, timeouts) makes it the better default choice for most projects. Only choose actix-web if you have a specific reason.
- **Ignoring `tracing` in favor of `println!` or `log` during development.** Replacing `println!` with tracing late in a project is painful because tracing requires structuring your context differently. Adding `tracing` instrumentation early means your development output, production logs, and distributed traces all share the same structured format from the start.

---

## How Do You Choose the Right Crates for Your Project?

**The key is matching crates to project goals: not all 10 crates appear in every project. A CLI tool, web service, and embedded system use different subsets.**

- **CLI tool**: serde, clap, anyhow, optional: reqwest, rayon
- **Web API**: tokio, axum, serde, sqlx, anyhow, tracing, reqwest
- **Batch data processing**: rayon, serde, anyhow, tokio (if network I/O needed)
- **Library crate**: thiserror (not anyhow), serde with `derive` feature explicitly documented
- **Performance-critical service**: tokio, tracing, anyhow/thiserror, careful about allocation: consider parking\_lot for Mutex/RwLock

Start with serde and anyhow. Every other crate solves a domain-specific problem. Learn them when you need them, not in advance.

---

## Ready to Build Production Systems with These Crates?

**Knowing crate APIs is different from knowing how to combine them into production systems that handle real traffic, edge cases, and failures.** If you want a structured path from individual crates to complete backend services: with 1:1 code review, production patterns, and project deliverables: [Rustify's 9-week bootcamp](https://rustify.rs/bootcamps/backend) covers exactly this: building and deploying production-grade Rust services using axum, sqlx, serde, tokio, and tracing in a mentored curriculum.

---

## Keep Reading

- [Rust Developer Salary in the USA (2026)](https://rustify.rs/articles/rust-developer-salary-usa-2026)
- [How Long to Learn Rust by Background: Hours, Timeline & ROI](https://rustify.rs/articles/how-long-to-learn-rust)
- [Best Way to Learn Rust in 2026](https://rustify.rs/articles/best-way-to-learn-rust-2026)
- [Is Rust Hard to Learn?](https://rustify.rs/articles/is-rust-hard-to-learn)

---