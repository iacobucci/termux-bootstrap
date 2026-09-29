# termux-bootstrap

Modular and robust bootstrap script for **Termux** environments on Android.

## Quick Install (one-liner via curl)

1. Transfer your SSH credentials to `~/.ssh/`

2. Run the command:

```bash
curl -fsSL https://raw.githubusercontent.com/iacobucci/termux-bootstrap/refs/heads/master/termux-bootstrap | bash -s -- # options
```

## Workflow

1. **Storage**: Request Android storage access permissions (`termux-setup-storage`).
2. **Mirror**: Configure fast European mirrors via `termux-change-repo`.
3. **Packages**: Enable `glibc-repo` and `x11-repo`, and install compilation toolchains and development utilities.
4. **Directories**: Set up `~/.local/dir` (`config`, `content`, `forks`, `notes`, `script`, `source`, `templates`), generate `.update.sh`, and create symlinks in `$HOME`.
5. **SSH**: Verify presence and file permissions of private keys in `~/.ssh/`.
6. **Clone & Remotes**: Clone personal repositories (`config`, `content`, `notes`, `script`, `templates`) configuring multi-remotes (`origin`, `rock`, `github`), clone `password-store` (`~/.local/share/password-store`) and `gnupg` (`~/.config/gnupg`, moving any pre-existing non-git directory to `gnupg.old`) from `rock` (`ssh://valerio@rock/git/...`), clone external forks/utilities, and synchronize all personal repos, password-store, and gnupg to branch `termux` with pull.
7. **Compilation**: Compile personal programs (`htop-vim`, `lf`, `rstow`, `pwdshort`) into `~/.local/bin/`.
8. **Python Packages**: Install Python packages (`ptpython`, `mutagen`, `eyed3`, `requests`, `totp`) via `pip install --break-system-packages`.
9. **Dotfiles**: Run `update` from `~/script` in `~/config` (managed by `rstow`), symlink `~/.termux` -> `~/config/termux` (setting `zsh` as default login shell), link `.termux/zshenv` to `/data/data/com.termux/files/usr/etc/zshenv` (to initialize `$ZDOTDIR`), and move `/etc/motd` to `/etc/motd.old` to silence the login banner.
10. **Antigravity CLI**: Configure `127.0.0.1 localhost` and `::1 ip6-localhost` in `/etc/hosts` and install [antigravity-cli-termux](https://github.com/wallentx/antigravity-cli-termux).
11. **Services**: Enable background SSH daemon (`sv-enable sshd`).

## Local Usage

```bash
# Full bootstrap (first run)
./termux-bootstrap

# Skip package installation
./termux-bootstrap --no-install-packages

# Skip cloning and compilation
./termux-bootstrap --no-clone --no-compile

# Dry-run simulation
./termux-bootstrap --dry-run
```

## Main Options

| Option | Description |
| :--- | :--- |
| `--no-install-packages` | Skip package repository updates and package installation |
| `--no-storage` | Skip Android storage access configuration |
| `--no-change-repo` | Skip mirror selection via `termux-change-repo` |
| `--no-dirs` | Skip creating `~/.local/dir` and home symlinks |
| `--no-ssh-check` | Skip SSH credentials verification |
| `--no-clone` | Skip cloning repositories and forks |
| `--no-compile` | Skip compiling binaries into `~/.local/bin/` |
| `--no-python` | Skip installing Python packages (`ptpython`, `mutagen`, `eyed3`, `requests`, `totp`) |
| `--no-dotfiles` | Skip dotfiles configuration with `rstow` and `~/.termux` link |
| `--no-antigravity` | Skip Antigravity CLI installation and `/etc/hosts` configuration |
| `--no-services` | Skip enabling background services (`sshd`) |
| `-y, --yes` | Automatically answer yes to package manager prompts |
| `-n, --dry-run` | Show commands without executing them |
| `-h, --help` | Display full help information |
