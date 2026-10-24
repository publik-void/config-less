# `config-less`

## Setup

`less` supports configuration via environment variables or files. Environment
variables can be convenient but need to be managed for every shell, so this
repository instead uses file-based configuration, specified in `lesskey`.
Different `less` versions require different setup, however.

The following commands show the setup for different `less` versions. Simply
running all of them is an option too and should generally result in `less` using
the newest supported configuration file location. However, two of the three
files will usually be unnecessary and the `lesskey` command was removed in
version 706.

`PWD` is used to supply an absolute path to the `ln` commands and should be the
path to the repository root directory where the `lesskey` file resides.

### Versions ≥596 (or ≥583 if `XDG_CONFIG_HOME` is set)

```sh
config_dir=${XDG_CONFIG_HOME:-"$HOME/.config"}
ln -sfn "$PWD/lesskey" "$config_dir/lesskey"
```

### Versions 582 – 595

```sh
ln -sfn "$PWD/lesskey" "$HOME/.lesskey"
```

### Versions <582

```sh
lesskey -o "$HOME/.less" "$PWD/lesskey"
```

Re-running this is needed to apply an updated version of `$PWD/lesskey`.

Some systems with `less` versions <582 like macOS may not provide the `lesskey`
executable, so either a manual install or a compilation on another machine is
needed.

