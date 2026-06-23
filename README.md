# Awesome machin [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of things built with **[machin](https://github.com/javimosch/machin)** — MFL, the Machine-First Language. machin compiles a terse, type-inferred, agent-friendly language to native code through C: small static binaries, no runtime.

> New machin app? Open a PR adding a one-line entry. Keep the list machine-first: terse, linked, current.

## The language

- **[machin](https://github.com/javimosch/machin)** — the compiler + language (MFL → C → native). Generics, closures, goroutines/channels (`select`, `close`, range, comma-ok), arena GC, C FFI, a `machweb` web framework, and a growing builtin surface (networking, native TLS + WebSocket, file I/O, SQLite, JSON + jq-style path queries, regex, base64, SHA-256/HMAC, `(value, err)` error handling).

## Apps & tools

- **[boilerplate-cli-ui-machin](https://github.com/javimosch/boilerplate-cli-ui-machin)** — a single-binary CLI serving an embedded React web UI + JSON API, with a background daemon via the C FFI. The machin entry in the [SuperCLI](https://github.com/javimosch) boilerplate family (smallest binary at ~27 KB).
- **[machin-healthcheck](https://github.com/javimosch/machin-healthcheck)** — a concurrent HTTP status/latency checker. One goroutine per URL, results over a channel. Drove `dial`/`now_ms`/`parse_int` into machin.
- **[machin-ssg](https://github.com/javimosch/machin-ssg)** — a static-site generator (markdown subset → HTML). Drove native file I/O and a parser fix into machin.
- **[machin-fetch](https://github.com/javimosch/machin-fetch)** — a tiny HTTPS client CLI (a pocket `curl` for `https://`). GET/POST, single binary. Drove **native TLS** (`https_get`/`https_post`, OpenSSL) into machin.
- **[machin-wscat](https://github.com/javimosch/machin-wscat)** — a tiny duplex WebSocket (`wss://`) client CLI (a pocket `websocat`). Stdin → send, recv → stdout. Drove a **native WebSocket client** (`wss_open`/`send`/`recv`/`close`, RFC 6455 over TLS) into machin.
- **[machin-linkcheck](https://github.com/javimosch/machin-linkcheck)** — a concurrent link checker that classifies each URL (OK / 4xx / 5xx / unreachable) and exits non-zero on broken links. Drove **error handling** into machin: `http_get` returning `(status, body, err)` plus `exit`.
- **[machin-jq](https://github.com/javimosch/machin-jq)** — a tiny `jq`-style JSON path query CLI (`.a.b[0].name`). Pairs with machin-fetch for a native HTTPS→query pipeline. Drove a **JSON path engine** (`json_get`) into machin.
- **[machin-pool](https://github.com/javimosch/machin-pool)** — a bounded-concurrency URL checker: a fixed worker pool racing results against an overall deadline. Drove **`select`** (multi-way channel waits, timeouts) into machin.
- **[machin-pipe](https://github.com/javimosch/machin-pipe)** — a streaming parallel fetch pipeline: producer → workers → fan-in, each stage terminating by closing its channel. Drove **channel `close`** + range-over-channel into machin.
- **[machin-batch](https://github.com/javimosch/machin-batch)** — groups a line stream into JSON-array chunks by size or by timer (flushing the rest on EOF). Its `select` over input + ticker drove the **comma-ok receive** (`v, ok := <-ch`) into machin.
- **[machin-http](https://github.com/javimosch/machin-http)** — a multi-command HTTPS client (`get`/`post`/`head`) with short+long flags and auto `--help`. Drove a reusable **flag parser** (`framework/flags.src`) into machin.
- **[machin-grep](https://github.com/javimosch/machin-grep)** — a regex line matcher (pocket `grep`): match/invert/count/only/line-numbers over a POSIX ERE. Drove **regex** builtins (`regex_match`/`find`/`groups`/`replace`) into machin.
- **[machin-jwt](https://github.com/javimosch/machin-jwt)** — a JWT decoder: decode header/payload (base64url JSON) and extract a claim. Drove **base64** builtins (`base64_encode`/`base64_decode`) into machin.
- **[machin-hmac](https://github.com/javimosch/machin-hmac)** — compute/verify HMAC-SHA256 (or SHA-256) signatures — webhook verification (GitHub/Stripe). Drove **hash** builtins (`sha256`/`hmac_sha256`) into machin.
- **[machin-wc](https://github.com/javimosch/machin-wc)** — a `wc` clone (lines/words/bytes), matching coreutils. Drove **`read_stdin`** (slurp stdin verbatim) into machin.
- **[machin-kv](https://github.com/javimosch/machin-kv)** — a persistent key-value store (set/get/del/list), data surviving across runs. Drove **SQLite** builtins (`sqlite_open`/`exec`/`query`/`close`) into machin.
- **[machin-cron](https://github.com/javimosch/machin-cron)** — a cron-expression evaluator: prints the next N times a crontab line fires. Drove **`time_fields`** (decompose a Unix timestamp into calendar fields) into machin.
- **[machin-date](https://github.com/javimosch/machin-date)** — a `date(1)`-style timestamp formatter (output matches GNU `date`). Drove **`time_format`** (strftime over a Unix timestamp) into machin.
- **[machin-meet](https://github.com/javimosch/machin-meet)** — a minimal self-hostable **Calendly for one person**: a single binary (HTTP + SQLite + embedded booking page) serving free slots, `.ics` files, and signed manage/cancel links. Drove **`time_make`** (build a Unix timestamp from calendar fields) into machin, completing the time trio.

## In the machin repo

- **[`framework/`](https://github.com/javimosch/machin/tree/main/framework)** — reusable MFL modules: `machweb` (a web framework — router, response builders, JSON) and `flags.src` (a CLI flag parser), each composed ahead of your app with `machin encode`.
- **[`examples/`](https://github.com/javimosch/machin/tree/main/examples)** — runnable programs: a raylib **GUI** game menu, JSON-over-HTTP servers, generics, concurrency, FFI, and more.

## Why these exist

machin's current direction is **dogfooding**: build real tools, hit real gaps, and grow the language to fill them. Each app above added capabilities to machin itself — that's the point. To contribute an app, build something real and send a PR here with the link.
