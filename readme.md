# `config-less`

## Setup

`less` supports configuration via environment variables or files. Environment
variables can be convenient but need to be managed for every shell, so this
repository instead uses file-based configuration, specified in `lesskey`.
Different `less` versions require different setup, however. Running all of the
following should generally have newer `less` versions use the newest way the
support, but the `lesskey` command was removed in version 706. `repo_root` is
the path to the repository containing the `lesskey` file.

### Versions ≥596 (or ≥583 if `XDG_CONFIG_HOME` is set)

```sh
config_dir=${XDG_CONFIG_HOME:-"$HOME/.config"}
ln -sfn "$repo_root/lesskey" "$config_dir/lesskey"
```

### Versions 582 – 595

```sh
ln -sfn "$repo_root/lesskey" "$HOME/.lesskey"
```

### Versions <582

```sh
lesskey -o "$HOME/.less" "$repo_root/lesskey"
```

Re-running this is needed to apply an updated version of `$repo_root/lesskey`.

Some systems with `less` versions <582 like macOS may not provide the `lesskey`
executable, so either a manual install or a compilation on another machine is
needed.

