---
title: "Crate List"
source: "https://blessed.rs/crates"
author:
published:
created: 2026-11-04
description:
tags:
  - "clippings"
---
### Common

Very commonly used crates that everyone should know about

#### General

General purpose

| Use Case | Recommended Crates |
| --- | --- |
| Random numbers | **[rand](https://lib.rs/crates/rand)** [\[docs\]](https://docs.rs/rand)   De facto standard random number generation library split out from the standard library  **[fastrand](https://lib.rs/crates/fastrand)** [\[docs\]](https://docs.rs/fastrand)   A simple and fast random number generator (but not cryptographically secure). |
| Time & Date | The time, chrono, and jiff crates are all high-quality libraries that are widely used and maintained by trusted members of the community.   If you're unsure which to use then we weakly recommend jiff as we think it has the nicest API. However, if you need integration with other crates in the ecosystem then you may find that chrono and/or time are more widely supported.  **[jiff](https://lib.rs/crates/jiff)** [\[docs\]](https://docs.rs/jiff)   A datetime library with an API based on JavaScript's Temporal, automatic tzdb integration and convenient daylight saving time calendar arithmetic, but that currently lacks some of the ecosystem integration that time and chrono have.  **[time](https://lib.rs/crates/time)** [\[docs\]](https://docs.rs/time)   A widely used datetime library with a focused API, a flexible parsing/formatting DSL and compile time datetime literals.  **[chrono](https://lib.rs/crates/chrono)** [\[docs\]](https://docs.rs/chrono)   A widely used datetime library with built-in time zone support, a traditional parsing/formatting DSL and some support for calendar arithmetic. It also has a conservative a MSRV policy. However, it is [soft-deprecated](https://github.com/chronotope/chrono/issues/1768).  ***See also*** (click to open)  **[icu\_datetime](https://lib.rs/crates/icu_datetime)** [\[docs\]](https://docs.rs/icu_datetime)   A library focused on providing support for datetime internationalization using the [International Components for Unicode](https://icu.unicode.org/). The [icu](https://lib.rs/icu) crate re-exports this along with other ICU-focused crates, so you might want that instead.  **[hifitime](https://lib.rs/crates/hifitime)** [\[docs\]](https://docs.rs/hifitime)   An ultra-precise datetime library focused towards scientific applications. |
| Regular Expressions | **[regex](https://lib.rs/crates/regex)** [\[docs\]](https://docs.rs/regex)   De facto standard regex library. Very fast, but does not support fancier features such as backtracking.  **[fancy-regex](https://lib.rs/crates/fancy-regex)** [\[docs\]](https://docs.rs/fancy-regex)   Use if need features such as backtracking which regex doesn't support |
| UUIDs | **[uuid](https://lib.rs/crates/uuid)** [\[docs\]](https://docs.rs/uuid)   Implements generating and parsing UUIDs and a number of utility functions |
| Temporary files | **[tempfile](https://lib.rs/crates/tempfile)** [\[docs\]](https://docs.rs/tempfile)   Supports both temporary files and temporary directories |
| Gzip (de)compression | **[flate2](https://lib.rs/crates/flate2)** [\[docs\]](https://docs.rs/flate2)   Uses a pure-Rust implementation by default. Use feature flags to opt in to system zlib. |
| Insertion-ordered map | **[indexmap](https://lib.rs/crates/indexmap)** [\[docs\]](https://docs.rs/indexmap)   A HashMap that separately keeps track of insertion order and allows you to efficiently iterate over its elements in that order |
| Stack-allocated arrays | **[arrayvec](https://lib.rs/crates/arrayvec)** [\[docs\]](https://docs.rs/arrayvec)   Arrays that are ONLY stack-allocated with fixed capacity  **[smallvec](https://lib.rs/crates/smallvec)** [\[docs\]](https://docs.rs/smallvec)   Arrays that are stack-allocated with fallback to the heap if the fixed stack capacity is exceeded  **[tinyvec](https://lib.rs/crates/tinyvec)** [\[docs\]](https://docs.rs/tinyvec)   Stack allocated arrays in 100% safe Rust code but requires items to implement the Default trait. |
| HTTP Requests | See the HTTP section below for server-side libraries  **[reqwest](https://lib.rs/crates/reqwest)** [\[docs\]](https://docs.rs/reqwest)   Full-fat HTTP client. Can be used in both synchronous and asynchronous code. Requires tokio runtime.  **[ureq](https://lib.rs/crates/ureq)** [\[docs\]](https://docs.rs/ureq)   Minimal synchronous HTTP client focused on simplicity and minimising dependencies. |

#### Logging

Crates for logging. Note that in general you will need a separate crate for actually printing/storing the logs

| Use Case | Recommended Crates |
| --- | --- |
| Text-based logging | **[tracing](https://lib.rs/crates/tracing)** [\[docs\]](https://docs.rs/tracing)   Tracing is now the go-to crate for logging.  **[log](https://lib.rs/crates/log)** [\[docs\]](https://docs.rs/log)   An older and simpler crate if your needs are simple and you are not using any async code. |
| Structured logging | **[tracing](https://lib.rs/crates/tracing)** [\[docs\]](https://docs.rs/tracing)   Tracing is now the go-to crate for logging.  **[slog](https://lib.rs/crates/slog)** [\[docs\]](https://docs.rs/slog)   Structured logging |

#### Language Extensions

General purpose utility crates that extend language and/or stdlib functionality.

| Use Case | Recommended Crates |
| --- | --- |
| Lazy static variable initialization | This functionality is now [included in the standard library](https://doc.rust-lang.org/stable/std/sync/struct.LazyLock.html)  ***See also*** (click to open)  **[once\_cell](https://lib.rs/crates/once_cell)** [\[docs\]](https://docs.rs/once_cell)   Newer crate with more ergonomic API. Has since been adopted into the std library  **[lazy\_static](https://lib.rs/crates/lazy_static)** [\[docs\]](https://docs.rs/lazy_static)   Older crate. API is less convenient, but crate is stable and maintained. |
| Iterator helpers | **[itertools](https://lib.rs/crates/itertools)** [\[docs\]](https://docs.rs/itertools)   A bunch of useful methods on iterators that aren't in the stdlib |
| Macro helpers | **[syn](https://lib.rs/crates/syn)** [\[docs\]](https://docs.rs/syn)   Parse rust source code  **[quote](https://lib.rs/crates/quote)** [\[docs\]](https://docs.rs/quote)   Quasi quoting rust (useful for interpolating generated code with literal code)  **[pastey](https://lib.rs/crates/pastey)** [\[docs\]](https://docs.rs/pastey)   Concatenating and manipulating identifiers  **[darling](https://lib.rs/crates/darling)** [\[docs\]](https://docs.rs/darling)   Derive macro to easily parse derive macro inputs |
| Safe type casts | **[bytemuck](https://lib.rs/crates/bytemuck)** [\[docs\]](https://docs.rs/bytemuck)  **[zerocopy](https://lib.rs/crates/zerocopy)** [\[docs\]](https://docs.rs/zerocopy) |
| Bitflags | **[bitflags](https://lib.rs/crates/bitflags)** [\[docs\]](https://docs.rs/bitflags)   Strongly typed bitflag types |

#### Serialization

Encode/decode between in-memory representations and general-purpose wire formats

| Use Case | Recommended Crates |
| --- | --- |
| General-purpose / format agnostic | **[serde](https://lib.rs/crates/serde)** [\[docs\]](https://docs.rs/serde)   De facto standard serialization library. Use in conjunction with sub-crates like \`serde\_json\` for the specific format that you are using (JSON, YAML, etc). Supports a variety of both text and binary protocols, including self-describing ones. |
| Non-self-describing, external schema file | **[serde\_json](https://lib.rs/crates/serde_json)** [\[docs\]](https://docs.rs/serde_json)   A fast and heavily optimized JSON encoder and decoder.  **[toml](https://lib.rs/crates/toml)** [\[docs\]](https://docs.rs/toml)   Serde compatible encoder for Tom's obvious, minimal language. Very commonly used for human-friendly configuration data.  **[prost](https://lib.rs/crates/prost)** [\[docs\]](https://docs.rs/prost)   Protocol buffer library with strong ergonomics and wide industry adoption. Commonly used with gRPC / \`tonic\`. Use in conjunction with \`protox\` to avoid dependency on \`protoc\`.  **[capnp](https://lib.rs/crates/capnp)** [\[docs\]](https://docs.rs/capnp)   Cap'n Proto library. Offers zero-copy usage mode that is optimal for large messages, along with other improvements over Protocol Buffers. Tradeoffs are less wide usage and less developer-friendly.  **[flatbuffers](https://lib.rs/crates/flatbuffers)** [\[docs\]](https://docs.rs/flatbuffers)   Flatbuffers library. Also offers zero-copy usage and is more widely used than cap'n proto, with further cost to ergonomics. |
| Non-self-describing, no external schema file | **[postcard](https://lib.rs/crates/postcard)** [\[docs\]](https://docs.rs/postcard)   `no_std` focused Serde serializer/deserializer, aimed at constrained environments.  **[rkyv](https://lib.rs/crates/rkyv)** [\[docs\]](https://docs.rs/rkyv)   Fast zero-copy deserialization framework that allows arbitrary field types and safe zero-copy mutation. |

#### System

For low-level interaction with the underling platform / operating system

| Use Case | Recommended Crates |
| --- | --- |
| Memory mapping files | **[memmap2](https://lib.rs/crates/memmap2)** [\[docs\]](https://docs.rs/memmap2)   The older memmap crate is unmaintained. |
| Libc | **[libc](https://lib.rs/crates/libc)** [\[docs\]](https://docs.rs/libc)   Bindings for directly calling libc functions. |
| Windows (OS) | **[windows](https://lib.rs/crates/windows)** [\[docs\]](https://docs.rs/windows)   The official Microsoft-provided crate for interacting with windows APIs |
| macOS/iOS | **[objc2](https://lib.rs/crates/objc2)** [\[docs\]](https://docs.rs/objc2)   A whole family of crates that cover binding to Objective-C and most of the Apple system APIs |
| \*nix (OSs) | **[rustix](https://lib.rs/crates/rustix)** [\[docs\]](https://docs.rs/rustix)   Efficient and safe POSIX / \*nix / Winsock syscall-like APIs. It uses idiomatic Rust types: refs, slices, Results instead of raw pointers, safe wrappers around raw file descriptors, bitflags instead of bare integer flags, and several other conveniences.  **[nix](https://lib.rs/crates/nix)** [\[docs\]](https://docs.rs/nix)   Bindings to the various \*nix system functions. (Unix, Linux, MacOS, etc.) |
| Signal handling | **[signal-hook](https://lib.rs/crates/signal-hook)** [\[docs\]](https://docs.rs/signal-hook)   Provides high-level, sync APIs for handling signals safely. The low-level machinery is also exposed as a separate crate, [`signal-hook-registry`](https://lib.rs/crates/signal-hook-registry), which lets other libraries like [`tokio::signal`](https://docs.rs/tokio/latest/tokio/signal) interoperate with it. |

#### Tooling

Developer tools for working with Rust projects.

| Use Case | Recommended Crates |
| --- | --- |
| Toolchain Management | **[rustup](https://rustup.rs/)** [\[docs\]](https://rust-lang.github.io/rustup)   Install, manage, and upgrade versions of rustc, cargo, clippy, rustfmt and more. |
| Linting | **[clippy](https://github.com/rust-lang/rust-clippy#usage)** [\[docs\]](https://doc.rust-lang.org/clippy/)   The official Rust linter.  **[cargo-semver-checks](https://github.com/obi1kenobi/cargo-semver-checks)**   Lint your crate releases for semantic versioning violations. |
| Code Formatting | **[rustfmt](https://github.com/rust-lang/rustfmt#rustfmt----)** [\[docs\]](https://rust-lang.github.io/rustfmt/)   The official Rust code formatter. |
| Cross Compilation | **[cross](https://github.com/cross-rs/cross#cross)** [\[docs\]](https://github.com/cross-rs/cross/wiki/Getting-Started)   Seamless cross-compiling using Docker containers.  **[cargo-zigbuild](https://github.com/rust-cross/cargo-zigbuild)**   Easily cross-compile using Zig as the linker. |
| Managing Dependencies | **[cargo-edit](https://github.com/killercup/cargo-edit)**   Adds 'cargo upgrade' and 'cargo set-version' commands to cargo  **[cargo-outdated](https://github.com/kbknapp/cargo-outdated#cargo-outdated)**   Finds dependencies that have available updates  **[cargo-audit](https://github.com/RustSec/rustsec/tree/main/cargo-audit#rustsec-cargo-audit)**   Check dependencies for reported security vulnerabilities  **[cargo-license](https://github.com/onur/cargo-license#cargo-license)**   Lists licenses of all dependencies  **[cargo-deny](https://github.com/EmbarkStudios/cargo-deny#-cargo-deny)** [\[docs\]](https://embarkstudios.github.io/cargo-deny/)   Enforce policies on your code and dependencies. |
| Testing | **[cargo-nextest](https://nexte.st/)**   Faster, better test runner  **[insta](https://insta.rs/)** [\[docs\]](https://insta.rs/docs/)   Snapshot testing with inline snapshot support |
| Benchmarking | **[criterion](https://lib.rs/crates/criterion)** [\[docs\]](https://docs.rs/criterion)   Statistically accurate benchmarking tool for benchmarking libraries  **[divan](https://lib.rs/crates/divan)** [\[docs\]](https://docs.rs/divan)   Simple yet powerful benchmarking library with allocation profiling  **[gungraun](https://lib.rs/crates/gungraun)** [\[docs\]](https://docs.rs/gungraun)   High-precision, one-shot and consistent benchmarking framework/harness for Rust. All Valgrind tools at your fingertips.  **[hyperfine](https://github.com/sharkdp/hyperfine#hyperfine)**   Tool for benchmarking compiled binaries (similar to unix time command but better)  **[hotpath-rs](https://hotpath.rs/)**   Profiler for CPU, memory, SQL, HTTP, and async performance, with Prometheus and Grafana support. |
| Performance | **[cargo-flamegraph](https://github.com/flamegraph-rs/flamegraph#cargo-flamegraph)**   Execution flamegraph generation  **[dhat](https://lib.rs/crates/dhat)** [\[docs\]](https://docs.rs/dhat)   Heap memory profiling  **[cargo-show-asm](https://lib.rs/crates/cargo-show-asm)** [\[docs\]](https://docs.rs/cargo-show-asm)   Print the generated assembly for a Rust function |
| Debugging Macros | [Rust Analyzer](https://github.com/rust-lang/rust-analyzer) also allows you to [expand macros directly in your editor](https://rust-analyzer.github.io/manual.html#expand-macro-recursively)  **[cargo-expand](https://github.com/dtolnay/cargo-expand#cargo-expand)**   Allows you to inspect the code that macros expand to |
| Release Automation | **[cargo-release](https://github.com/crate-ci/cargo-release#cargo-release)** [\[docs\]](https://github.com/crate-ci/cargo-release/tree/master/docs)   Helper for publishing new crate versions.  **[Release-plz](https://release-plz.ieni.dev/)** [\[docs\]](https://release-plz.ieni.dev/docs)   Release Rust crates from CI with a Release PR. |
| Continuous Integration | **[rust-toolchain (github action)](https://github.com/dtolnay/rust-toolchain#install-rust-toolchain)**   Github action to install Rust components via rustup  **[rust-cache (github action)](https://github.com/Swatinem/rust-cache#rust-cache-action)**   Github action to cache compilation artifacts and speed up subsequent runs.  **[install-action (github action)](https://github.com/taiki-e/install-action)**   GitHub Action for installing development tools (mainly from GitHub Releases). |

### Math / Scientific

The [num](https://lib.rs/crates/num) crate is trusted and has a variety of numerical functionality that is missing from the standard library.

| Use Case | Recommended Crates |
| --- | --- |
| Abstracting over different number types | **[num-traits](https://lib.rs/crates/num-traits)** [\[docs\]](https://docs.rs/num-traits)   Traits like Number, Add, etc that allow you write functions that are generic over the specific numeric type |
| Big Integers | **[num-bigint](https://lib.rs/crates/num-bigint)** [\[docs\]](https://docs.rs/num-bigint)   It's not the fastest, but it's part of the trusted num library.  **[malachite](https://lib.rs/crates/malachite)** [\[docs\]](https://docs.rs/malachite)   LGPL licensed. Much faster than num-bigint while still being pure-Rust.  **[rug](https://lib.rs/crates/rug)** [\[docs\]](https://docs.rs/rug)   LGPL licensed. Wrapper for the GMP C library. Much faster than num-bigint. |
| Big Decimals | **[rust\_decimal](https://lib.rs/crates/rust_decimal)** [\[docs\]](https://docs.rs/rust_decimal)   The binary representation consists of a 96 bit integer number, a scaling factor used to specify the decimal fraction and a 1 bit sign. |
| Sortable Floats | **[ordered-float](https://lib.rs/crates/ordered-float)** [\[docs\]](https://docs.rs/ordered-float)   Float types that don't allow NaN and are therefore orderable. You can also use the `total_cmp` method from the standard library like `.sort_by(\|a, b\| a.total_cmp(&b))`. |
| Linear Algebra | **[nalgebra](https://lib.rs/crates/nalgebra)** [\[docs\]](https://docs.rs/nalgebra)   General-purpose linear algebra library with transformations and statically-sized or dynamically-sized matrices. However it supports only vectors (1d) and matrices (2d) and not higher-dimensional tensors.  **[ndarray](https://lib.rs/crates/ndarray)** [\[docs\]](https://docs.rs/ndarray)   Less featureful than nalgebra but supports arbitrarily dimensioned arrays |
| DataFrames | **[polars](https://lib.rs/crates/polars)** [\[docs\]](https://docs.rs/polars)   Similar to the Pandas library in Python but in pure Rust. Uses the Apache Arrow Columnar Format as the memory model.  **[datafusion](https://lib.rs/crates/datafusion)** [\[docs\]](https://docs.rs/datafusion)   [Apache DataFusion](https://arrow.apache.org/datafusion) is an in-memory query engine that uses Apache Arrow as the memory model |

### FFI / Interop

Crates that allow Rust to interact with code written in other languages.

| Use Case | Recommended Crates |
| --- | --- |
| C | **[bindgen](https://lib.rs/crates/bindgen)** [\[docs\]](https://docs.rs/bindgen)   Generate Rust bindings to C libraries  **[cbindgen](https://lib.rs/crates/cbindgen)** [\[docs\]](https://docs.rs/cbindgen)   Generate C bindings to Rust libraries  **[cc](https://lib.rs/crates/cc)** [\[docs\]](https://docs.rs/cc)   Compile and link C code as part of your Cargo build |
| C++ | **[cxx](https://lib.rs/crates/cxx)** [\[docs\]](https://docs.rs/cxx)   Safe C++ <-> Rust interop by generating code for both sides. |
| Python | **[pyo3](https://lib.rs/crates/pyo3)** [\[docs\]](https://docs.rs/pyo3)   Supports both calling python code from Rust and exposing Rust code to Python |
| Node.js | **[napi](https://lib.rs/crates/napi)** [\[docs\]](https://docs.rs/napi)   is a framework for building pre-compiled Node.js addons in Rust.  **[neon](https://lib.rs/crates/neon)** [\[docs\]](https://docs.rs/neon)   Slower than napi, but also widely used and well-maintained |
| Ruby | **[magnus](https://lib.rs/crates/magnus)** [\[docs\]](https://docs.rs/magnus)   Ruby bindings for Rust. Write Ruby extension gems in Rust, or call Ruby from Rust. Supported by Ruby's rubygems and bundler  **[rutie](https://lib.rs/crates/rutie)** [\[docs\]](https://docs.rs/rutie)   Supports both embedding Rust into Ruby applications and embedding Ruby into Rust applications |
| Objective-C | **[objc2](https://lib.rs/crates/objc2)** [\[docs\]](https://docs.rs/objc2)   Sound and Idiomatic Rust to Objective-C interface and runtime bindings. Main crate in the objc2 project. |
| Java/JVM | **[jni](https://lib.rs/crates/jni)** [\[docs\]](https://docs.rs/jni)   Implement Java methods for JVM and Android in Rust. Call Java code from Rust. Embed JVM in Rust applications.  **[duchess](https://lib.rs/crates/duchess)** [\[docs\]](https://docs.rs/duchess)   Autogenerates safe wrappers so safe Rust code can invoke methods on Java objects. No unsafe code required. Limited support for calling Rust from Java. |
| Lua | **[mlua](https://lib.rs/crates/mlua)** [\[docs\]](https://docs.rs/mlua)   Bindings to Lua 5.4, 5.3, 5.2, 5.1 (including LuaJIT) |
| Dart/Flutter | **[flutter\_rust\_bridge](https://lib.rs/crates/flutter_rust_bridge)** [\[docs\]](https://docs.rs/flutter_rust_bridge)   Works with Dart with or without Flutter |
| Erlang/Elixir | **[rustler](https://lib.rs/crates/rustler)** [\[docs\]](https://docs.rs/rustler)   Safe Rust bridge for creating Erlang NIF functions |
| Kotlin/Swift/Python/Ruby | **[uniffi](https://lib.rs/crates/uniffi)** [\[docs\]](https://docs.rs/uniffi)   Share Rust codebase to create cross-platform apps (also 3rd party support for Kotlin Multiplatform, Go, C#, Dart) |

### Cryptography

Crates that provide implementations of cryptographic algorithms. This section attempts to list the best crates for the listed algorithms, but does not intend to make recommendations for the algorithms themselves.

| Use Case | Recommended Crates |
| --- | --- |
| Password Hashing | For more algorithms, see [Rust Crypto Password Hashes](https://github.com/RustCrypto/password-hashes#rustcrypto-password-hashes).  **[argon2](https://lib.rs/crates/argon2)** [\[docs\]](https://docs.rs/argon2)  **[scrypt](https://lib.rs/crates/scrypt)** [\[docs\]](https://docs.rs/scrypt)  **[bcrypt](https://lib.rs/crates/bcrypt)** [\[docs\]](https://docs.rs/bcrypt) |
| General Purpose Hashing | For more algorithms, see [Rust Crypto Hashes](https://github.com/RustCrypto/hashes#rustcrypto-hashes).  **[blake3](https://lib.rs/crates/blake3)** [\[docs\]](https://docs.rs/blake3)  **[sha2](https://lib.rs/crates/sha2)** [\[docs\]](https://docs.rs/sha2) |
| AEAD Encryption | For more algorithms, see [Rust Crypto AEADs](https://github.com/RustCrypto/AEADs#rustcrypto-authenticated-encryption-with-associated-data-aead-algorithms).  **[aes-gcm-siv](https://lib.rs/crates/aes-gcm-siv)** [\[docs\]](https://docs.rs/aes-gcm-siv)  **[aes-gcm](https://lib.rs/crates/aes-gcm)** [\[docs\]](https://docs.rs/aes-gcm)  **[chacha20poly1305](https://lib.rs/crates/chacha20poly1305)** [\[docs\]](https://docs.rs/chacha20poly1305) |
| RSA | **[rsa](https://lib.rs/crates/rsa)** [\[docs\]](https://docs.rs/rsa) |
| Digital Signatures | For more algorithms, see [Rust Crypto Signatures](https://github.com/RustCrypto/signatures#rustcrypto-signatures--).  **[ed25519](https://lib.rs/crates/ed25519)** [\[docs\]](https://docs.rs/ed25519)   Use in conjunction with the ed25519-dalek crate.  **[ecdsa](https://lib.rs/crates/ecdsa)** [\[docs\]](https://docs.rs/ecdsa)  **[dsa](https://lib.rs/crates/dsa)** [\[docs\]](https://docs.rs/dsa) |
| Certificate Formats | For more formats, see [Rust Crypto Formats](https://github.com/RustCrypto/formats#rustcrypto-formats--).  **[der](https://lib.rs/crates/der)** [\[docs\]](https://docs.rs/der)  **[pem-rfc7468](https://lib.rs/crates/pem-rfc7468)** [\[docs\]](https://docs.rs/pem-rfc7468)  **[pkcs8](https://lib.rs/crates/pkcs8)** [\[docs\]](https://docs.rs/pkcs8)  **[x509-cert](https://lib.rs/crates/x509-cert)** [\[docs\]](https://docs.rs/x509-cert) |
| TLS / SSL | **[rustls](https://lib.rs/crates/rustls)** [\[docs\]](https://docs.rs/rustls)   Rustls is a modern TLS library that aims to provide a good level of cryptographic security and no unsafe features or obsolete cryptography by default.  **[native-tls](https://lib.rs/crates/native-tls)** [\[docs\]](https://docs.rs/native-tls)   Delegates to the system TLS implementations on windows and macOS, and uses OpenSSL on linux.  ***See also*** (click to open)  **[webpki](https://lib.rs/crates/webpki)** [\[docs\]](https://docs.rs/webpki)   X.509 Certificate validation. Builds on top of ring.  **[ring](https://lib.rs/crates/ring)** [\[docs\]](https://docs.rs/ring)   Fork of BoringSSL. Provides low-level cryptographic primitives for TLS/SSL |
| Utilities | **[subtle](https://lib.rs/crates/subtle)** [\[docs\]](https://docs.rs/subtle)   Utilities for writing constant-time algorithms  **[zeroize](https://lib.rs/crates/zeroize)** [\[docs\]](https://docs.rs/zeroize)   Securely erase memory |

### Networking

TCP, HTTP, GRPc, etc. And the executors required to do asynchronous networking.

#### Async Foundations

To do async programming using the async-await in Rust you need a runtime to execute drive your Futures.

| Use Case | Recommended Crates |
| --- | --- |
| General Purpose Async Executors | **[tokio](https://lib.rs/crates/tokio)** [\[docs\]](https://docs.rs/tokio)   The oldest async runtime in the Rust ecosystem and still the most widely supported. Recommended for new projects.  **[futures-executor](https://lib.rs/crates/futures-executor)** [\[docs\]](https://docs.rs/futures-executor)   A minimal executor. In particular, the [block\_on](https://docs.rs/futures-executor/latest/futures_executor/fn.block_on.html) function is useful if you want to run an async function synchronously in codebase that is mostly synchronous.  **[smol](https://lib.rs/crates/smol)** [\[docs\]](https://docs.rs/smol)   A small and modular async runtime. Since the implementation is modularized in smaller crates, you can directly use only the required crates instead of depending on the entire runtime. |
| Async Utilities | **[futures](https://lib.rs/crates/futures)** [\[docs\]](https://docs.rs/futures)   Utility functions for working with Futures and Streams  **[async-trait](https://lib.rs/crates/async-trait)** [\[docs\]](https://docs.rs/async-trait)   Provides a workaround for the lack of language support for async functions in traits |
| io\_uring | **[glommio](https://lib.rs/crates/glommio)** [\[docs\]](https://docs.rs/glommio)   Use if you need io\_uring support. Still somewhat experimental but rapidly maturing. |

#### HTTP

HTTP client and server libraries, as well as lower-level building blocks.

| Use Case | Recommended Crates |
| --- | --- |
| Types & Interfaces | **[http](https://lib.rs/crates/http)** [\[docs\]](https://docs.rs/http)   The \`http\` crate doesn't actually contain an HTTP implementation. Just types and interfaces to help interoperability. |
| Low-level HTTP Implementation | **[hyper](https://lib.rs/crates/hyper)** [\[docs\]](https://docs.rs/hyper)   A low-level HTTP implementation (both client and server). Implements HTTP/1, and HTTP/2. Works best with the tokio async runtime, but can support other runtimes. |
| HTTP Client | **[reqwest](https://lib.rs/crates/reqwest)** [\[docs\]](https://docs.rs/reqwest)   Full-fat HTTP client. Can be used in both synchronous and asynchronous code. Requires tokio runtime.  **[ureq](https://lib.rs/crates/ureq)** [\[docs\]](https://docs.rs/ureq)   Minimal synchronous HTTP client focused on simplicity and minimising dependencies. |
| HTTP Server | **[axum](https://lib.rs/crates/axum)** [\[docs\]](https://docs.rs/axum)   A minimal and ergonomic framework. An official part of the tokio project. Recommend for most new projects.  **[actix-web](https://lib.rs/crates/actix-web)** [\[docs\]](https://docs.rs/actix-web)   A performance focused framework. All Rust frameworks are fast, but choose actix-web if you need the absolutely maximum performance.  ***See also*** (click to open)  **[warp](https://lib.rs/crates/warp)** [\[docs\]](https://docs.rs/warp)   Very similar to axum but with a quirkier API. This is a solid framework, but you should probably prefer Axum unless you particularly like the API  **[salvo](https://lib.rs/crates/salvo)** [\[docs\]](https://docs.rs/salvo)   Hyper/tokio-based with simplified handler signatures (no complex generic bounds), built-in OpenAPI and TLS/ACME.  **[rocket](https://lib.rs/crates/rocket)** [\[docs\]](https://docs.rs/rocket)   Has an excellent API and a solid implementation. However development has been intermittent. |
| GraphQL Server | **[async-graphql](https://lib.rs/crates/async-graphql)** [\[docs\]](https://docs.rs/async-graphql)   A high-performance graphql server library that's fully specification compliant. Integrates with actix-web, axum, poem, rocket, tide, warp. |

#### Websockets

This section includes libraries for you to use just websockets. However note that many of the HTTP server frameworks in the section above also support websockets

| Use Case | Recommended Crates |
| --- | --- |
| Low-level | **[tungstenite](https://lib.rs/crates/tungstenite)** [\[docs\]](https://docs.rs/tungstenite)   Low-level crate that others build on |
| General Purpose | **[tokio-tungstenite](https://lib.rs/crates/tokio-tungstenite)** [\[docs\]](https://docs.rs/tokio-tungstenite)   If you are using the tokio executor  **[async-tungstenite](https://lib.rs/crates/async-tungstenite)** [\[docs\]](https://docs.rs/async-tungstenite)   If you are using the async-std executor |

#### gRPC

| Use Case | Recommended Crates |
| --- | --- |
| General Purpose | **[tonic](https://lib.rs/crates/tonic)** [\[docs\]](https://docs.rs/tonic)   gRPC over HTTP/2 with full support for asynchronous code. Works with tokio |

#### D-Bus

For cross-platform D-Bus clients and services.

| Use Case | Recommended Crates |
| --- | --- |
| General Purpose | **[zbus](https://lib.rs/crates/zbus)** [\[docs\]](https://docs.rs/zbus)   A Rust-only (a)sync implementation of the protocol. Provides high-level proxies and zbus\_xmlgen for scaffolding. Includes a book for D-Bus/zbus beginners. |
| Bindings | **[dbus](https://lib.rs/crates/dbus)** [\[docs\]](https://docs.rs/dbus)   Bindings for the battle-tested libdbus implementation. Has sister crates for asynchrony, codegen, etc. |

### Databases

#### SQL Databases

The multi-database options (SQLx and Diesel) are generally quite good, and worth considering even if you only need support for a single database.

| Use Case | Recommended Crates |
| --- | --- |
| Multi Database | **[sqlx](https://lib.rs/crates/sqlx)** [\[docs\]](https://docs.rs/sqlx)   Works with Postgres, MySQL, SQLite, and MS SQL.   Supports compile time checking of queries. Async: supports both tokio and async-std. |
| ORMs | **[diesel](https://lib.rs/crates/diesel)** [\[docs\]](https://docs.rs/diesel)   Has excellent performance and takes an approach of strict compile time guarantees. The main crate is Sync only, but [diesel-async](https://lib.rs/crates/diesel-async) provides an async connection implementation.  **[sea-orm](https://lib.rs/crates/sea-orm)** [\[docs\]](https://docs.rs/sea-orm)   Built on top of sqlx (see above). There is also a related sea-query crate that provides a query builder without full ORM functionality. |
| Postgres | **[tokio-postgres](https://lib.rs/crates/tokio-postgres)** [\[docs\]](https://docs.rs/tokio-postgres)   Postgres-specific library. Performs better than SQLx |
| MySQL | **[mysql\_async](https://lib.rs/crates/mysql_async)** [\[docs\]](https://docs.rs/mysql_async)   Has a poorly designed API. Prefer SQLx or Diesel for MySQL |
| SQLite | **[rusqlite](https://lib.rs/crates/rusqlite)** [\[docs\]](https://docs.rs/rusqlite)   Provides a sync API to SQLite + provides access to advanced sqlite features. |
| MS SQL | **[tiberius](https://lib.rs/crates/tiberius)** [\[docs\]](https://docs.rs/tiberius)   MS SQL specific library. Has better support for advanced column types than SQLx. |
| Oracle | **[diesel-oci](https://lib.rs/crates/diesel-oci)** [\[docs\]](https://docs.rs/diesel-oci)   Diesel backend and connection implementation for oracle databases  **[oracle](https://lib.rs/crates/oracle)** [\[docs\]](https://docs.rs/oracle)   Rust bindings to ODPI-C  **[sibyl](https://lib.rs/crates/sibyl)** [\[docs\]](https://docs.rs/sibyl)   An OCI-based interface supporting both blocking (threads) and nonblocking (async) AP |

#### Other Databases

| Use Case | Recommended Crates |
| --- | --- |
| Redis | **[redis](https://lib.rs/crates/redis)** [\[docs\]](https://docs.rs/redis) |
| MongoDB | **[mongodb](https://lib.rs/crates/mongodb)** [\[docs\]](https://docs.rs/mongodb) |
| ElasticSearch | **[elasticsearch](https://lib.rs/crates/elasticsearch)** [\[docs\]](https://docs.rs/elasticsearch) |
| LMDB | [The rkv crate](https://github.com/mozilla/rkv) depends on [the lmdb-rkv dependency](https://github.com/mozilla/lmdb-rs) which is archived and is inactive.  **[heed](https://lib.rs/crates/heed)** [\[docs\]](https://docs.rs/heed)   A fully typed LMDB wrapper with minimum overhead. |
| Rocks DB | **[rocksdb](https://lib.rs/crates/rocksdb)** [\[docs\]](https://docs.rs/rocksdb) |
| Cassandra | **[cassandra-protocol](https://lib.rs/crates/cassandra-protocol)** [\[docs\]](https://docs.rs/cassandra-protocol)   Low-level Cassandra protocol implementation.  **[cdrs-tokio](https://lib.rs/crates/cdrs-tokio)** [\[docs\]](https://docs.rs/cdrs-tokio)   High-level async Cassandra driver. |

#### Utilities

| Use Case | Recommended Crates |
| --- | --- |
| Connection pool | **[deadpool](https://lib.rs/crates/deadpool)** [\[docs\]](https://docs.rs/deadpool)   A dead simple async pool for connections and objects of any type. |

### CLIs

#### Argument Parsing

See [argparse-benchmarks-rs](https://github.com/rust-cli/argparse-benchmarks-rs) for a full comparison of the crates mentioned here and more.

| Use Case | Recommended Crates |
| --- | --- |
| Fully-featured | **[clap](https://lib.rs/crates/clap)** [\[docs\]](https://docs.rs/clap)   Ergonomic, battle-tested, includes the kitchen sink, and is fast at runtime. However compile times can be slow  ***See also*** (click to open)  **[bpaf](https://lib.rs/crates/bpaf)** [\[docs\]](https://docs.rs/bpaf)   Faster compile times than clap while still being featureful. But still has some rough edges, and the API can be confusing at times. |
| Minimal | **[lexopt](https://lib.rs/crates/lexopt)** [\[docs\]](https://docs.rs/lexopt)   Fast compile times, fast runtime, pedantic about correctness. API is less ergonomic  **[pico-args](https://lib.rs/crates/pico-args)** [\[docs\]](https://docs.rs/pico-args)   Fast compile times, fast runtime, more lax about correctness. API is more ergonomic |

#### Utility

Helpers that are often useful when implementing CLIs

| Use Case | Recommended Crates |
| --- | --- |
| Globbing | **[globset](https://crates.io/crates/globset)** [\[docs\]](https://docs.rs/globset)   High-performance globbing that allows multiple globs to be evaluated at once |
| Directory walking | **[walkdir](https://crates.io/crates/walkdir)** [\[docs\]](https://docs.rs/walkdir)   Basic recursive filesystem walking.  **[ignore](https://crates.io/crates/ignore)** [\[docs\]](https://docs.rs/ignore)   Recursive filesystem walking that respects ignore files (like.gitignore) |
| File watching | **[notify](https://lib.rs/crates/notify)** [\[docs\]](https://docs.rs/notify)   Watch files or directories and execute a function when they change |
| User directories | **[dirs](https://lib.rs/crates/dirs)** [\[docs\]](https://docs.rs/dirs)   Provide platform-specific locations for configuration, cache, and other data  **[directories](https://lib.rs/crates/directories)** [\[docs\]](https://docs.rs/directories)   A higher-level library that can also compute paths for applications  ***See also*** (click to open)  **[etcetera](https://lib.rs/crates/etcetera)** [\[docs\]](https://docs.rs/etcetera)   An alternative with a different license |

#### Terminal Rendering

For fancy terminal rendering and TUIs. The crates recommended here work cross-platform (including windows).

| Use Case | Recommended Crates |
| --- | --- |
| Coloured Output | **[termcolor](https://crates.io/crates/termcolor)** [\[docs\]](https://docs.rs/termcolor)   Cross-platform terminal colour output |
| Progress indicators | **[indicatif](https://lib.rs/crates/indicatif)** [\[docs\]](https://docs.rs/indicatif)   Progress bars and spinners |
| TUI | **[ratatui](https://lib.rs/crates/ratatui)** [\[docs\]](https://docs.rs/ratatui)   A high-level TUI library with widgets, layout, etc.  **[crossterm](https://lib.rs/crates/crossterm)** [\[docs\]](https://docs.rs/crossterm)   Low-level cross-platform terminal rendering and event handling |
| Interactive prompts | **[inquire](https://lib.rs/crates/inquire)** [\[docs\]](https://docs.rs/inquire)   Ask for confirmation, selection, text input and more |

### Concurrency

#### Data Structures

| Use Case | Recommended Crates |
| --- | --- |
| Mutex | **[parking\_lot](https://lib.rs/crates/parking_lot)** [\[docs\]](https://docs.rs/parking_lot)   std::sync::Mutex also works fine. But Parking Lot is faster. |
| Atomic pointer swapping | **[arc-swap](https://lib.rs/crates/arc-swap)** [\[docs\]](https://docs.rs/arc-swap)   Useful for sharing data that has many readers but few writers |
| Concurrent HashMap | See [conc-map-bench](https://github.com/xacrimon/conc-map-bench) for comparative benchmarks of concurrent HashMaps.  **[dashmap](https://lib.rs/crates/dashmap)** [\[docs\]](https://docs.rs/dashmap)   The fastest for general purpose workloads  **[papaya](https://lib.rs/crates/papaya)** [\[docs\]](https://docs.rs/papaya)   Particularly good for read-heavy workloads. |
| Channels | See [communicating-between-sync-and-async-code](https://docs.rs/tokio/latest/tokio/sync/mpsc/index.html#communicating-between-sync-and-async-code) for notes on when to use async-specific channels vs general purpose channels.  **[crossbeam-channel](https://lib.rs/crates/crossbeam-channel)** [\[docs\]](https://docs.rs/crossbeam-channel)   The same channel algorithm as in the standard library but with a more powerful API, offering a Go-like 'select' feature.  **[flume](https://lib.rs/crates/flume)** [\[docs\]](https://docs.rs/flume)   Smaller and simpler than crossbeam-channel and almost as fast  **[tokio](https://lib.rs/crates/tokio)** [\[docs\]](https://docs.rs/tokio)   Tokio's sync module provides channels for using in async code  **[postage](https://lib.rs/crates/postage)** [\[docs\]](https://docs.rs/postage)   Channels that integrate nicely with async code, with different options than Tokio |
| Parallel computation | **[rayon](https://lib.rs/crates/rayon)** [\[docs\]](https://docs.rs/rayon)   Convert sequential computation into parallel computation with one call - \`par\_iter\` instead of \`iter\` |

### Graphics

#### GUI

| Use Case | Recommended Crates |
| --- | --- |
| GTK | **[gtk4](https://lib.rs/crates/gtk4)** [\[docs\]](https://docs.rs/gtk4)   Rust bindings to GTK4. These are quite well supported, although you'll often need to use the C documentation.  **[relm4](https://lib.rs/crates/relm4)** [\[docs\]](https://docs.rs/relm4)   A higher-level library that sits on top of gtk4-rs |
| Frontend Web GUI | **[leptos](https://lib.rs/crates/leptos)** [\[docs\]](https://docs.rs/leptos)  **[dioxus-web](https://lib.rs/crates/dioxus-web)** [\[docs\]](https://docs.rs/dioxus-web) |
| Webview-based GUI | **[tauri](https://lib.rs/crates/tauri)** [\[docs\]](https://docs.rs/tauri)   Electron-like web-based UI. Except it uses system webviews rather than shipping chromium, and non-UI code is written in Rust rather than node.js  **[dioxus-desktop](https://lib.rs/crates/dioxus-desktop)** [\[docs\]](https://docs.rs/dioxus-desktop)   Uses the same webview as Tauri for rendering but the UI is defined in Rust/Dioxus rather than JavaScript. Dioxus runs outside the webview with the framework handling IPC to update the DOM |
| Native GUI | **[iced](https://lib.rs/crates/iced)** [\[docs\]](https://docs.rs/iced)   Retained mode UI with a nice API.  **[egui](https://lib.rs/crates/egui)** [\[docs\]](https://docs.rs/egui)   Immediate-mode UI with lots of widgets. Very useable out of the box if your needs are simple and you don't need to customise the look and feel  **[slint](https://lib.rs/crates/slint)** [\[docs\]](https://docs.rs/slint)   A stable and feature-rich UI toolkit with a declarative language. Licensed under GPL, royalty-free for desktop/mobile, or with paid options for proprietary embedded use.  **[gpui](https://lib.rs/crates/gpui)** [\[docs\]](https://www.gpui.rs/#docs)   High performance framework used in the Zed text editor. However, focus has recently moved away from community contributions.  ***See also*** (click to open)  **[dioxus-native](https://lib.rs/crates/dioxus-native)** [\[docs\]](https://docs.rs/dioxus-native)   A native backend for Dioxus built on top of [Blitz](https://github.com/DioxusLabs/blitz)  **[floem](https://lib.rs/crates/floem)** [\[docs\]](https://docs.rs/floem)   Inspired by Xilem, Leptos and rui, Floem is currently more complete than any of them for native UI. Used by the Lapce text editor.  **[vizia](https://github.com/vizia/vizia)** [\[docs\]](https://book.vizia.dev/)   Fairly complete with sophisticated layout and text layout, but has yet to make a stable release.  **[freya](https://freyaui.dev/)** [\[docs\]](https://docs.rs/freya/latest/freya/)   Cross-platform, native, declarative GUI library powered by Skia, with a built-in headless testing runner, common components, and flexible state management and styling APIs  **[xilem](https://github.com/linebender/xilem)** [\[docs\]](https://docs.rs/xilem)   The replacement for Druid based on the more interoperable Vello and Glazier crates. However, it's currently not complete enough to be usable.  **[makepad](https://github.com/makepad/makepad)**   Makepad has a strong focus on performance and minimising bloat but is consequently less feature complete in areas such as accessibility and system integration.  **[ribir](https://ribir.org/)** [\[docs\]](https://ribir.org/docs/introduction/)  **[kas](https://lib.rs/crates/kas)** [\[docs\]](https://docs.rs/kas) |
| Window creation | **[winit](https://lib.rs/crates/winit)** [\[docs\]](https://docs.rs/winit)   The defacto standard option. Uses an event loop based architecture. Widely used and should probably be the default choice.  ***See also*** (click to open)  **[tao](https://lib.rs/crates/tao)** [\[docs\]](https://docs.rs/tao)   A fork of winit by the Tauri project which adds support for things like system menus that desktop apps need.  **[baseview](https://github.com/RustAudio/baseview)**   Specialized window creation library targeting windows to be embedded in other applications (e.g. DAW plugins) |
| 2D Renderers | **[skia-safe](https://lib.rs/crates/skia-safe)** [\[docs\]](https://docs.rs/skia-safe)   Bindings to the Skia C++ library. The most complete option with excellent performance. However, it can be difficult to get it to compile.  **[vello](https://lib.rs/crates/vello)** [\[docs\]](https://docs.rs/vello)   WGPU based and uses cutting edge techniques to render vector paths using the GPU.  **[vello\_cpu](https://lib.rs/crates/vello_cpu)** [\[docs\]](https://docs.rs/vello_cpu)   Pure-CPU (no GPU) rendering with excellent performance (multithreaded and SIMD-accelerated.  ***See also*** (click to open)  **[femtovg](https://lib.rs/crates/femtovg)** [\[docs\]](https://docs.rs/femtovg)   OpenGL based. Offers a simple API. Probably the easiest to get started with.  **[webrender](https://lib.rs/crates/webrender)** [\[docs\]](https://docs.rs/webrender)   OpenGL based. Mature with production usage in Firefox but documentation and OSS maintenance are lacking.  **[vger](https://lib.rs/crates/vger)** [\[docs\]](https://docs.rs/vger)   A simpler WGPU based option which is less innovative but currently more stable than vello. |
| UI layout | **[taffy](https://lib.rs/crates/taffy)** [\[docs\]](https://docs.rs/taffy)   Supports Flexbox and CSS Grid algorithms.  **[morphorm](https://lib.rs/crates/morphorm)** [\[docs\]](https://docs.rs/morphorm)   Implements an algorithm based on Figma's AutoLayout |
| Text layout | Parley and Cosmic-Text are more similar than they are different. Both build on top of Fontations and HarfRust, and handle rich text and BiDi.  **[parley](https://lib.rs/crates/parley)** [\[docs\]](https://docs.rs/parley)   Supports advanced layout features like laying out boxes inline with text.  **[cosmic-text](https://lib.rs/crates/cosmic-text)** [\[docs\]](https://docs.rs/cosmic-text)   Has better support for large buffers of monospace text |
| Accessibility | **[accesskit](https://lib.rs/crates/accesskit)** [\[docs\]](https://docs.rs/accesskit)   Allows you to export a semantic tree representing your UI to make accessible to screen readers and other assistive technologies |
| Clipboard | **[arboard](https://lib.rs/crates/arboard)** [\[docs\]](https://docs.rs/arboard)   A fork of rust-clipboard that supports copy and pasting of both text and images on Linux (X11/Wayland), MacOS and Windows. |
| File Dialogs | **[rfd](https://lib.rs/crates/rfd)** [\[docs\]](https://docs.rs/rfd)   Platform-native open/save file dialogs. Can be used in conjunction with other UI libraries. |

#### Game Development

| Use Case | Recommended Crates |
| --- | --- |
| Game Engines | **[bevy](https://lib.rs/crates/bevy)** [\[docs\]](https://docs.rs/bevy)   An ECS based game engine, good for 3D but also capable of 2D.  **[fyrox](https://lib.rs/crates/fyrox)** [\[docs\]](https://docs.rs/fyrox)   An OOP-focused game engine with 3D and 2D support and a full GUI scene editor.  **[ggez](https://lib.rs/crates/ggez)** [\[docs\]](https://docs.rs/ggez)   A simpler option for 2d games only.  **[macroquad](https://lib.rs/crates/macroquad)** [\[docs\]](https://docs.rs/macroquad)   A simple and easy to use 2d game library, great for beginners. |
| 3D Math | **[glam](https://lib.rs/crates/glam)** [\[docs\]](https://docs.rs/glam)   Fast math library optimised for game development use cases |