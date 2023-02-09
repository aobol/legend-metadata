# legend-metadata

All LEGEND metadata repositories in one Git repository.

## Rationale

This repository collects all LEGEND metadata Git repositories in a single, coherently structured, folder tree.
The various sub-repositories are linked via [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) as follows:

- `dataprod/`
  - `config` → [legend-dataflow-config](https://github.com/legend-exp/legend-dataflow-config)
  - `overrides` → [legend-dataflow-overrides](https://github.com/legend-exp/legend-dataflow-overrides)
- `hardware/`
  - `configuration` → [legend-hardware-configuration](https://github.com/legend-exp/legend-hardware-configuration)
  - `detectors` → [legend-hardware-configuration](https://github.com/legend-exp/legend-detectors)
  
To access the metadata, usage of existing helpers (listed at the bottom of this page) is generally recommended.
These software tools usually manage legend-metadata on your behalf (e.g. cloning and setting up the Git repository).
If this is not the case or you need to customize legend-metadata, keep reading.

## Management

The [Pro Git book](https://git-scm.com/book) provides an excellent guide about
[working with Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules).
Here's a summary.

### Cloning

A standard `git clone` will result in uninitialized submodules (i.e. empty directories).
To get the desired behavior, the `--recursive` flag should be passed:

```console
$ git clone --recursive git@github.com:legend-exp/legend-metadata
```

If you already cloned the repository without the flag, you can still initialize and clone the submodules as a separate step:

```console
$ git submodule --init update
```

### Keeping metadata in sync

The version of a certain submodule (e.g. `dataprod/config` → [legend-dataflow-config](https://github.com/legend-exp/legend-dataflow-config))
pinned in legend-metadata can be older than the latest commit found upstream in the linked repository.
Similarly, a user might want to checkout a version of choice. Since Git submodules are Git repositories
themselves, governing their state is straightforward. To pull the latest version of 
[legend-dataflow-config](https://github.com/legend-exp/legend-dataflow-config):

```console
$ cd dataprod/config
$ git checkout main
$ git pull
```

To checkout a specific version:

```console
$ cd dataprod/config
$ git checkout [tag | commit]
```

**Note:** if you think the version of a submodule should be updated, consider submitting a Pull Request.
  
## Accessors
- From Python: [pylegendmeta](https://github.com/legend-exp/pylegendmeta)
