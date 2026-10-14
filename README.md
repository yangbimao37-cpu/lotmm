# LotMM

LotMM is split into two companion projects: an HTTP API and a browser client. This repository links each project as a Git submodule.

- [`api`](api) — authentication, business rules, persistence, and listing photo storage.
- [`app`](app) — the browser interface and API client.

Clone this repository and its child projects together:

```sh
git clone --recurse-submodules https://github.com/yangbimao37-cpu/lotmm.git
```

If you already cloned without submodules, initialize them with:

```sh
git submodule update --init --recursive
```

See each project's `Readme.md` for setup and local development instructions.
