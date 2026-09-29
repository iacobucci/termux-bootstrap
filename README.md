# termux-bootstrap

Script di bootstrap modulare e robusto per ambienti **Termux** su Android.

## Installazione rapida (one-liner via curl)

Su un nuovo ambiente Termux è possibile avviare il bootstrap direttamente da remoto con:

```bash
# Esecuzione completa diretta
curl -fsSL https://raw.githubusercontent.com/iacobucci/termux-bootstrap/refs/heads/master/termux-bootstrap | bash

# Simulazione (dry-run) passando argomenti a bash (-s -- <opzioni>)
curl -fsSL https://raw.githubusercontent.com/iacobucci/termux-bootstrap/refs/heads/master/termux-bootstrap | bash -s -- --dry-run

# Esempio saltando l'installazione dei pacchetti
curl -fsSL https://raw.githubusercontent.com/iacobucci/termux-bootstrap/refs/heads/master/termux-bootstrap | bash -s -- --no-install-packages
```

## Workflow

1. **Storage**: Richiede i permessi di archiviazione (`termux-setup-storage`).
2. **Mirror**: Configura i mirror europei veloci tramite `termux-change-repo`.
3. **Pacchetti**: Abilita `glibc-repo` e `x11-repo` e installa i toolchain di compilazione e le utilità di sviluppo.
4. **Directory**: Crea la struttura `~/.local/dir` (`config`, `forks`, `notes`, `script`, `source`, `templates`), genera `.update.sh` e crea i symlink in `$HOME`.
5. **SSH**: Verifica la presenza e i permessi delle chiavi private in `~/.ssh/`.
6. **Clone**: Clona repository personali e fork da GitHub/server privato.
7. **Compilazione**: Compila i programmi personali (`htop-vim`, `lf`, `rstow`, `pwdshort`) in `~/.local/bin/`.
8. **Dotfiles**: Esegue `update` da `~/script` in `~/config` (gestito da `rstow`) e crea il symlink `~/.termux` -> `~/config/termux` (impostando `zsh` come shell predefinita).
9. **Antigravity CLI**: Configura `127.0.0.1 localhost` e `::1 ip6-localhost` in `/etc/hosts` e installa [antigravity-cli-termux](https://github.com/wallentx/antigravity-cli-termux).
10. **Servizi**: Abilita il demone SSH (`sv-enable sshd`).

## Utilizzo locale

```bash
# Esecuzione completa (primo avvio)
./termux-bootstrap

# Salta l'installazione dei pacchetti
./termux-bootstrap --no-install-packages

# Salta il cloning e la compilazione
./termux-bootstrap --no-clone --no-compile

# Simulazione (dry-run)
./termux-bootstrap --dry-run
```

## Opzioni principali

| Opzione | Descrizione |
| :--- | :--- |
| `--no-install-packages` | Salta l'aggiornamento e l'installazione dei pacchetti |
| `--no-storage` | Salta la configurazione dello storage Android |
| `--no-change-repo` | Salta la selezione mirror via `termux-change-repo` |
| `--no-dirs` | Salta la creazione di `~/.local/dir` e dei collegamenti in home |
| `--no-ssh-check` | Salta la verifica delle credenziali SSH |
| `--no-clone` | Salta il cloning dei repository e dei fork |
| `--no-compile` | Salta la compilazione dei binari in `~/.local/bin/` |
| `--no-dotfiles` | Salta la configurazione dei dotfiles con `rstow` e il link di `~/.termux` |
| `--no-antigravity` | Salta l'installazione di Antigravity CLI e la modifica di `/etc/hosts` |
| `--no-services` | Salta l'attivazione del servizio `sshd` |
| `-y, --yes` | Risponde sì automaticamente ai prompt di installazione |
| `-n, --dry-run` | Mostra i comandi senza eseguirli |
| `-h, --help` | Mostra la guida completa |
