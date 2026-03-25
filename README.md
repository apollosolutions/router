# apollosolutions/router — rhai-test fork

> **This is a fork of [apollographql/router](https://github.com/apollographql/router), maintained solely to support [apollosolutions/rhai-test](https://github.com/apollosolutions/rhai-test).**

## Why this fork exists

The [`rhai-test`](https://github.com/apollosolutions/rhai-test) CLI tool lets customers unit-test their Apollo Router Rhai scripts before deploying them. To build mock objects and register the same type getters/setters that the real Router provides (headers, body, context, URI, etc.), `rhai-test` needs access to the Router's internal Rhai plugin types and registration functions.

These internals are not part of the Router's public API — they live behind `pub(crate)` visibility. This fork makes them accessible by:

- Re-exporting the `rhai` plugin module through `_private::rhai` in `lib.rs`
- Changing visibility of key types (`SharedMut`, `OptionDance`, `Rhai*Request`/`Rhai*Response` structs) from `pub(crate)` to `pub`
- Making the `registration::register()` function and exported Rhai modules (`router_plugin`, `router_header_map`, `router_context`, etc.) public
- Making the `plugins`, `rhai`, and stage submodules (`router`, `supergraph`, `execution`, `subgraph`) public

## Branch conventions

| Branch | Based on | Purpose |
|---|---|---|
| `feature/rhaitest-v2.12.0` | Official Router [v2.12.0](https://github.com/apollographql/router/releases/tag/v2.12.0) | Current branch used by `rhai-test` |

When a new Router version ships with an updated Rhai engine, create a new branch from that tag and apply the same visibility changes.

## What this fork does NOT do

- No behavioral changes to the Router
- No new features or bug fixes
- No modifications to the Rhai scripting engine itself
- Should never be used to run a production Router — use the [official releases](https://github.com/apollographql/router/releases)

## Upstream

For the official Apollo Router, see: https://github.com/apollographql/router
