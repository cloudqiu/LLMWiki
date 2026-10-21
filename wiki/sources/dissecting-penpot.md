---
title: "Dissecting Penpot：Docker 部署与镜像检查记录"
type: source
created: 2026-10-21
updated: 2026-10-21
tags: [penpot, docker, self-hosting]
status: growing
sources: [raw/Dissecting penpot.md]
author: "未署名（个人操作记录）"
source_url: ""
raw_file: "raw/Dissecting penpot.md"
format: notes
---

# Dissecting Penpot：Docker 部署与镜像检查记录

## 来源信息

- 作者 / 出处：未署名的本地操作记录；文中引用 [Penpot 官方 Docker 安装指南](https://help.penpot.app/technical-guide/getting-started/docker/)，但本页摄入对象是操作记录本身。
- 获取日期：2026-10-21（本库文件时间；原记录未注明撰写日期）。
- 本地文件：`raw/Dissecting penpot.md`。
- 原始链接：未提供。

## 一句话概括

> 一份 Penpot 2.18 的 Docker Compose 部署快照：记录服务关系、示例配置、容器启动输出和各镜像的元数据，适合追溯这次本地安装，不能单独证明应用功能正常。

## 核心要点

- Compose 定义 8 个服务：frontend、backend、admin-console、mcp、exporter、PostgreSQL、Valkey、MailCatcher。frontend 映射主机 `9001` 到容器 `8080`；MailCatcher 映射 `1080`。见原文 L181–L579。
- frontend 依赖 backend、admin-console、mcp、exporter；backend 等待 PostgreSQL 和 Valkey 的健康检查；exporter 也依赖 Valkey。所有服务接入 `penpot` 网络。见 L181–L279、L377–L463。
- 数据库与上传素材分别放在 `penpot_postgres_v15`、`penpot_assets` 卷中。配置用文件系统存储素材，并预留 S3 选项。见 L121–L127、L261–L329、L467–L513。官方指南也要求定期备份这两类卷。
- Penpot 服务使用 `PENPOT_VERSION`，记录中的默认 tag 为 `2.18`；镜像检查输出的 Penpot 构建标签为 `2.18.3`。tag 与构建版本是不同层次，升级时应重新检查。见 L181–L183、L726–L1391。
- 启动输出显示 PostgreSQL、Valkey 为 Healthy，其余 Penpot 服务为 Started。记录未含登录、创建文件或导出测试，故应用层可用性**待验证**。见 L580–L598。

## 关键细节（值得引用的原文片段）

- L55–L61：配置注释明确提醒，向互联网开放时应移除 `disable-secure-session-cookies` 和 `disable-email-verification`；当前 flags 包含两者。
- L83–L111：`PENPOT_SECRET_KEY` 是派生会话等子密钥的主密钥，快照仍使用 `change-this-insecure-key`；数据库账号密码也采用示例值。此处是**示例配置状态**，不推断机器实际是否向外网开放。
- L351–L373、L553–L579：SMTP 指向 MailCatcher，供临时接收邮件；不等同于生产邮件投递。
- L600–L1391：后半部分主要是 Valkey Dockerfile 与 `docker image inspect` 输出，含 tag、digest、镜像用户、运行时及构建标签；不是 Penpot 源码架构分析。

## 与既有知识的关系

- 新建 [[penpot]]，记录这份资料支持的产品与实例事实；新建 [[penpot-self-hosting]]，整理部署拓扑和运维边界。
- 当前库中没有与此来源直接矛盾的既有页面。
- **待验证**：应用层功能是否正常、实际公网暴露范围、当前运行实例是否仍为该快照版本。

## 由本来源派生 / 更新的页面

- [[penpot]]（新建）
- [[penpot-self-hosting]]（新建）

## 留给用户的讨论问题

- 这次拆解更想深入哪一层：服务通信、镜像构成、MCP 集成，还是把当前本地实例整理成可复现的部署与备份手册？
