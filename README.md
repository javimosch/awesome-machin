# Awesome machin [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of things built with **[machin](https://github.com/javimosch/machin)** — MFL, the Machine-First Language. machin compiles a terse, type-inferred, agent-friendly language to native code through C: small static binaries, no runtime.

> New machin app? Open a PR adding a one-line entry. Keep the list machine-first: terse, linked, current.

## The language

- **[machin](https://github.com/javimosch/machin)** — the compiler + language (MFL → C → native). Generics, closures, goroutines/channels, arena GC, C FFI, a `machweb` web framework, and a growing builtin surface (networking, file I/O, JSON).

## Apps & tools

- **[boilerplate-cli-ui-machin](https://github.com/javimosch/boilerplate-cli-ui-machin)** — a single-binary CLI serving an embedded React web UI + JSON API, with a background daemon via the C FFI. The machin entry in the [SuperCLI](https://github.com/javimosch) boilerplate family (smallest binary at ~27 KB).
- **[machin-healthcheck](https://github.com/javimosch/machin-healthcheck)** — a concurrent HTTP status/latency checker. One goroutine per URL, results over a channel. Drove `dial`/`now_ms`/`parse_int` into machin.
- **[machin-ssg](https://github.com/javimosch/machin-ssg)** — a static-site generator (markdown subset → HTML). Drove native file I/O and a parser fix into machin.

## In the machin repo

- **[`framework/`](https://github.com/javimosch/machin/tree/main/framework)** — `machweb`, a web framework written in MFL (router, response builders, JSON).
- **[`examples/`](https://github.com/javimosch/machin/tree/main/examples)** — runnable programs: a raylib **GUI** game menu, JSON-over-HTTP servers, generics, concurrency, FFI, and more.

## Why these exist

machin's current direction is **dogfooding**: build real tools, hit real gaps, and grow the language to fill them. Each app above added capabilities to machin itself — that's the point. To contribute an app, build something real and send a PR here with the link.
