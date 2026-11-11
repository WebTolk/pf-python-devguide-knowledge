# Python Developer's Guide

English | [Русский](README.ru.md)

Shared, updatable knowledge package for [ProcessForge](https://github.com/WebTolk/process-forge). Contains 11 selected Markdown files from the existing snapshot, with their original upstream URLs and capture dates. It is a reference collection, not an installation of Python or development tools.

- Package ID: `docs.python-devguide`; resource ID: `root`; version: `1.0.1`.
- [Document index](resources/README.md), [provenance and licenses](NOTICE.md), [file hashes](sources.json).
- [Releases](https://github.com/WebTolk/pf-python-devguide-knowledge/releases), [stable update manifest](https://github.com/WebTolk/pf-python-devguide-knowledge/releases/latest/download/python-devguide.json).

## Install and use

Download `docs.python-devguide-1.0.1.zip` and `python-devguide.json` from the same versioned release. Verify the ZIP SHA-256 against the manifest before extraction. Extract the ZIP contents directly into the selected PF package root's `docs.python-devguide/` directory, so `package.yaml` sits at that directory's root. Configure that package root in the workplace's `registries/package-roots.yaml` if necessary. Do not overwrite an existing installation without preserving it first. Record the initial installation in `registries/installed-subjects.yaml` with `type: knowledge_package`, the exact package `id`, `scope: workplace`, its `version`, and the actual workplace-relative `install_path`. This record is required so the updater replaces the existing dotted package directory instead of guessing a different destination. Preserve unrelated registry entries.

From an installed PF distribution, with its Python environment:

```sh
python bin/pf.py knowledge-package-doctor --workplace <workplace> --package docs.python-devguide --package-root global
python bin/pf.py update entity-sources rebuild --workplace <workplace>
python bin/pf.py update candidates refresh --workplace <workplace>
```

For a PF-managed consumer project, select `docs.python-devguide` in `requirements.knowledge_packages`, then refresh and verify its project context and search index. When contributing to ProcessForge itself, use its contributor guide and read selected `resources/` files directly; root project `.pf` state is not required. Load the document index first and only open pages relevant to the task. The reference snapshot may describe a newer Python version than the project's minimum supported version.

## Updates

`package.yaml` declares the stable GitHub Releases update site. PF discovers new versions, stages the ZIP, verifies SHA-256, and applies an update only through an explicit operator command. No arbitrary post-install commands are shipped. Use native `update stage`, `update verify`, `update apply --confirm` and `update rollback` with the discovered candidate id. An existing 1.0.0 workplace installation can acquire update discovery by adding this package's `update_sites` block while preserving the rest of its manifest.

The archive contains `package.yaml`, `resources/`, `indexes/`, `licenses/`, `sources.json`, `NOTICE.md` and `CHANGELOG.md`. Repository guides, build tooling, Git data and private PF state are excluded. See [maintenance](MAINTAINING.md).

Known PF limit at tested Core revision `8ebacb61`: native rollback restores package files but leaves the installed-subject registry version at the newer value. After rollback, compare `package.yaml` with `registries/installed-subjects.yaml` and reconcile that exact record before another update check. A successful rollback exit alone does not establish consistent version bookkeeping.
