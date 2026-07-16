# From direnv and nix to mise

Up to now I used [direnv](https://direnv.net) and Nix packages to get per-project tools.

Somehow this was not working well. Nix is built by highly intelligent people, but I am just a mere
mortal, average person.

[mise](https://github.com/jdx/mise) is both a package manager and a replacement for `direnv`.

## Installation

On Ubuntu, the installation is easy:

```bash
sudo apt install extrepo
sudo apt extrepo enable mise
sudo apt update
sudo apt install mise
```

Then activate mise in your shell by adding this to your `~/.bashrc` or `~/.zshrc`:

```bash
eval "$(mise activate bash)"   # or: mise activate zsh
```

## Usage

Each project gets a `mise.toml` file defining its tools and environment variables.

```toml
[tools]
go = "1.22"
prek = "latest" # alternative to pre-commit

[env]
MY_VAR = "value"

# mise.toml is public and tracked in git. Do not add secrets/token here.
# Add secrets into .env, and load them:
_.file = ".env"
```

Run `mise install` in the project directory to install the pinned tool versions, then `cd` into
the directory (or open a new shell) to have them picked up automatically.

Like `direnv allow`, mise won't load a `mise.toml` it hasn't seen before (or that changed) until
you run `mise trust` in that directory once.

## More

- [Bash Strict Mode](https://github.com/guettli/bash-strict-mode)
- [Thomas WOL: Working out Loud](https://github.com/guettli/wol)
