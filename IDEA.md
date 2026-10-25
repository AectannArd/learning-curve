# Learning Curve — A Practical Rust Course

**Status:** concept agreed (2026-10-25). This document records the shared understanding from the design interview; it is the source of truth for the course until superseded by specs.

## Product

An open, practice-driven Rust course that takes practicing developers from first principles to a multithreaded web application backed by a relational database and a cache.

- Public repository: `AectannArd/learning-curve`, license **Apache-2.0** (whole repository).
- Rendering: mdBook → GitHub Pages. English book at the site root, Russian book at `/ru/`, language switcher on every page, deployed from `main`.

## Audience

Practicing developers fluent in other languages (Go/Python/JS/C++), new to Rust. Fast pace; ownership and borrowing are taught early and in depth — that is their main barrier. No OOP-migration hand-holding.

## Bilingual model

Two parallel content trees: `content/en/` and `content/ru/` — both prose and code comments are translated.

- EN is the source of truth; any EN change ships in the same PR with the RU update.
- CI enforces structural parity between the trees (same chapters, headings, and code-block counts). Translation quality is human-reviewed.

## Block format

20 blocks, 1–2 hours each. Every block consists of:

1. a chapter explaining the block's concepts with runnable examples;
2. a from-scratch mini-app task in `blocks/NN-slug/` — no starter code, only a README with the task statement and a **Definition of Done** checklist;
3. a reference solution in `solutions/NN-slug/` with tests, exercised by CI.

Mini-app themes never repeat across blocks (reduces copy-paste motivation). Verification is manual against the DoD; from mid-course, unit tests (`#[test]`) are part of the taught content and written by the learner.

## Stack

axum · PostgreSQL · sqlx · Redis · tokio. Concurrency taught in two steps: std threads (threads, channels, `Mutex`/`Arc`) on console apps first, then async/tokio on the web part. Toolchain: rustup stable, edition 2024, any OS; Docker (compose file from the repo) required from block 14.

## Trajectory

**01–07 Foundations** — unit converter (variables/types/functions) · word-frequency counter (ownership, `String`/`&str`) · vending-machine state machine (enums, `match`) · CSV address book (collections, `Result`/`Option`/`?`) · pluggable-sink logger (traits/generics) · access-log analyzer (closures/iterators) · lib+bin refactor of the address book (modules, cargo, `#[test]`).

**08–11 Systems** — org-chart graph (`Box`/`Rc`/`RefCell`) · parallel file checksummer (threads, channels, `Mutex`/`Arc`) · async site checker (tokio, futures, `join`/`select`) · external JSON API CLI (serde, reqwest, anyhow/thiserror).

**12–16 Web** — in-memory quotes API (axum routing/extractors/JSON) · middleware + shared state + tracing (rate-limited service) · bookmark service with tags (PostgreSQL/sqlx: migrations, compile-time queries) · currency-rates API (Redis cache: TTL, invalidation) · JWT auth middleware (optional block).

**17–20 Capstone — library platform, three integrated services over one PostgreSQL (per-service schemas, HTTP integration):**

- **A. Catalog & Issuance** — books, copies, members, checkouts, reviews, ratings, recommendations.
- **B. Care & Repair** — copy state machine (damaged → in repair → ready), repair/maintenance orders; integrates with A over HTTP.
- **C. Reader Portal** — personal cabinet (my books, my reviews, personalized recommendations); stateless aggregator with **no own database**, Redis-cached.

Block 20 hardens the platform: hot-endpoint caching, background jobs, load testing across all three services.

## Authoring process

Phase by phase — Foundations → Systems → Web → Capstone — each phase through the spec-driven loop: spec → plan → delegated implementation (Claude Code / OpenCode) → review. Phase 0 (repository skeleton: bilingual mdBook, CI, docker, block/solution templates) follows the same loop. Phase DoD: all chapters EN+RU, solutions green in CI.
