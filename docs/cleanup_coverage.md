# Cleanup Coverage & Potential Enhancements

## Current Cleanup Functionality

`mac-cleanup-py` ships a wide range of modules to clear caches, logs and temporary files for many common tools and applications, such as `brew`, `npm`, `yarn`, `docker`, `gradle`, `poetry`, `pyenv`, `xcode`, `android`, and numerous others. For example, the Node/JS modules run commands like `npm cache clean --force`, `pnpm store prune`, and `yarn cache clean --force` to remove package-manager caches.

## Potential Enhancements & Suitable New Modules

| Category | Proposed Module(s) / Extension | Notes |
|---------|---------------------------------|-------|
| **General user caches & temp** | `user_cache` for `~/.cache/*` (e.g., puppeteer, prisma, huggingface); `mail_attachments` for Mail Downloads; `downloads_prune` to delete specific file types in Downloads | Extends coverage beyond `~/Library/Caches/*` handled by `system_caches`. |
| **System temp & logs** | `system_tmp` for `/private/tmp/*` and `/private/var/tmp/*`; extend `system_log` to include `/private/var/log/*` | Addresses temporary files and log directories not currently cleaned. |
| **Homebrew** | Extend `brew` to run `brew autoremove` and clear `~/Library/Caches/Homebrew/*` explicitly | Complements existing `brew cleanup -s`. |
| **Node / JS package managers** | Expand `npm`, `yarn`, `pnpm` modules to add `npm cache verify`, `pnpm store path` cleanup, Yarn cache paths, and remove `~/.node-gyp` | Covers additional caches and verification steps. |
| **Python** | Add `pip_cache`, `uv_cache`, `conda_cache`; optional `pycache_clean` (with `PYCACHE_ALLOW_IN_PROTECTED`) | Complements existing `poetry` and `pyenv` modules. |
| **Java / JVM** | New `maven_cache` module for `~/.m2/repository`; extend `gradle` to remove `daemon` and `wrapper/dists` | Covers Maven repositories and full Gradle cache. |
| **Go & Rust** | Extend `go` to include module cache; add `rust_cache` for `~/.cargo/{registry,git}` and optional `rustup_toolchains` pruning | Adds Rust ecosystem support. |
| **Xcode / SwiftPM / iOS** | Extend `xcode` to clean `CoreSimulator`, `com.apple.dt.Xcode` container, `SwiftPM` caches; add flags for DeviceSupport (`XCODE_DEEP_DEVICE_SUPPORT`) and Archives (`XCODE_CLEAN_ARCHIVES`) | Improves coverage of Xcode-related artifacts. |
| **Android Studio & JetBrains IDEs** | `android_studio_cache` for `~/.AndroidStudio*/system/{caches,index,compile-server,tmp,log}` and optional AVD cleanup; `jetbrains_cache` for `~/Library/Caches/<product>*/` and log paths | Goes beyond current Android cache and JetBrains log cleanup. |
| **Visual Studio (Mac)** | `visual_studio_cache` for caches/logs in `~/Library/Caches/VisualStudio` and related paths | Adds support for Microsoft’s IDE. |
| **VS Code** | `vscode_cache` to remove cache directories (`Cache`, `CachedData`, `Code Cache`, `GPUCache`, `Service Worker/CacheStorage`) and optional `workspaceStorage` | Addresses a very common developer tool. |
| **Docker** | Extend `docker` module to include `docker builder prune -af`, optional `--volumes`, and `docker scout cache prune` (`DOCKER_SCOUT_CLEAN` / `DOCKER_SCOUT_CLEAR_SBOMS`) | Adds builder-cache and Scout cleanups alongside existing `system prune`. |
| **Time Machine snapshots** | `tm_snapshots` with `TM_SNAPSHOTS=keep-latest|delete-all` via `tmutil` | Handles local snapshot buildup. |

## Optional “Big-Rock” Modules

These caches are often large but potentially disruptive; they are good candidates for opt-in modules with explicit flags:

- **JVM extras** – `ivy_cache`, `coursier_cache`, `kotlin_cache`
- **.NET / C#** – `nuget_prune` (existing `nuget` could expose CLI flags); optional `dotnet_sdk` review
- **C/C++ toolchains** – `ccache_clear`, `clangd_index`, `bazel_cache`
- **JS runtimes & version managers** – `nvm_prune`, `asdf_cleanup`, `deno_cache`, `bun` (already present)
- **Python extras** – `conda_pkgs`, `virtualenvs_cleanup`, `pipx_cleanup`
- **Ruby** – extend `gem` and add `rbenv_cleanup`
- **Rust toolchains** – `rustup_prune`, `cargo_target` (per-project, opt-in)
- **Mobile/game tooling** – `android_sdk_cleanup`, `unity_cache`, `unreal_derived_data`
- **Containers & local clusters** – `podman_prune`, `colima_cleanup`, `lima_cleanup`, `kind_delete`, `k3d_delete`, `minikube_delete`
- **Apple developer extras** – `ios_device_logs`, `instruments_traces`
- **Other package managers** – `macports_clean`, `carthage_cache` (CocoaPods already covered by `pod`)

---

This document outlines existing cleanup coverage and future module ideas for `mac-cleanup-py`.
