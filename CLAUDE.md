# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Purpose

This is a personal git configuration reference repository. `README.md` is a reference document — not a script — containing global git alias setup commands and workflow documentation for Cesar Galvis Leon (`cgalvisleon@gmail.com`).

**`README.md` is written in Spanish.** All alias descriptions, section headings, and comments in that file follow Spanish conventions.

## Repository Structure

`README.md` has two parallel setup blocks that must always be kept in sync:
1. **macOS / Linux / Git Bash** — uses single-quoted shell functions.
2. **Windows CMD** — uses double-quoted strings with escaped inner quotes (`\"`).

When adding or modifying an alias, update **both** blocks and the reference table that follows each one.

`README.md` covers:
- **Global git aliases** set via `git config --global alias.<name> "..."`.
- **Two remote targets**: `origin` (GitHub personal, host alias `github-cgalvisleon`) and `josephine` (Celsia/work, host alias `github-celsia`). Aliases prefixed with `j` target `josephine`.
- **SSH multi-account config** for `~/.ssh/config` with separate `ed25519` key files per identity.
- **Techniques**: merge/conflict resolution, gitignore cache cleanup, sensitive-data removal, history search, and remote URL changes.

## Alias Reference

### View / Info

| Alias | Effect |
|-------|--------|
| `git l` | Pretty graph log |
| `git s` | Short status with branch |
| `git v` | Latest tag (version) |
| `git b` | Abbreviated version tag |
| `git aliases` | Print all aliases grouped by category |

### Branch

| Alias | Usage | Effect |
|-------|-------|--------|
| `new` | `git new <branch>` | `checkout -b` |
| `set` | `git set <branch>` | `checkout` |
| `del` | `git del <branch>` | `branch -D` |
| `rn` | `git rn <branch>` | Rename current branch |
| `main` | `git main` | Rename to `main` |
| `lb` | `git lb` | List local branches |
| `lba` | `git lba` | List all branches |
| `lbr` | `git lbr` | List remote branches |
| `upstream` | `git upstream <branch>` | Set upstream and push |
| `up` | `git up` | `push -u origin` |
| `odel` | `git odel <branch>` | Delete remote branch |
| `orn` | `git orn <old> <new>` | Rename branch on origin |
| `set-head` | `git set-head` | Update remote HEAD |

### Pull

| Alias | Usage | Effect |
|-------|-------|--------|
| `get` | `git get <branch>` | `pull origin <branch>` |
| `getall` | `git getall` | `pull origin` |
| `bring` | `git bring <branch>` | `pull origin <branch>` |

### Commit + Push — origin

All aliases below run `git add . && git commit -m "<Prefix>:$1" && git push -u origin`.

| Alias | Commit prefix |
|-------|---------------|
| `prepare` | `Prepare` (no push) |
| `initial` | `Initial` + `push --all` |
| `update` / `upd` | `Update` |
| `backup` | `Backup` |
| `feat` | `Feat` |
| `review` | `Review` |
| `fix` | `Fix` |
| `bug` | `Bug` |
| `deploy` | `Deploy` |
| `down` | `Down` |
| `rollback` | `Rollback` |
| `merge` | `Merge` |

### Commit + Push — josephine (work remote)

| Alias | Usage | Effect |
|-------|-------|--------|
| `jbackup` | `git jbackup <branch>` | Backup to josephine |
| `jreview` | `git jreview <branch>` | Review to josephine |
| `jmerge` | `git jmerge <branch>` | Merge to josephine |
| `jdeploy` | `git jdeploy <branch>` | Deploy to josephine |
| `jfix` | `git jfix <branch>` | Fix to josephine |
| `jbring` | `git jbring <branch>` | Pull from josephine |

### Reset / Undo

| Alias | Effect |
|-------|--------|
| `rhs` | `reset HEAD^ --soft` |
| `rhh` | `reset HEAD^ --hard` |
| `clean` | `git rm -r --cached .` (clear cache) |
| `chout <file>` | Discard changes in file |
| `ri [n]` | Interactive rebase last n commits (default 3) |
| `ric <id>` | Interactive rebase from a commit |
| `fpush` | Force push current branch |
| `dropc "<text>"` | Drop commits by message text (requires `git-filter-repo`) |
| `dropf <file>` | Remove a file completely from history (requires `git-filter-repo`) |

### Tags

| Alias | Usage | Effect |
|-------|-------|--------|
| `tag` | `git tag <name>` | Create local tag |
| `tags` | `git tags` | Push all tags to origin |
| `tago` | `git tago` | List remote tags |
| `tagdel` | `git tagdel <name>` | Delete local tag |
| `tagodel` | `git tagodel <name>` | Delete remote tag |

## Key Techniques

### Merge & conflicts

```bash
git merge -X theirs <branch>       # Accept all incoming changes
git checkout --theirs .             # Accept origin changes (during conflict)
git checkout --ours .               # Accept local changes (during conflict)
git checkout origin/<branch> -- <file>  # Restore a specific file from a branch
```

### Discard changes in a file

```bash
git checkout -- <file>
git chout <file>                    # Same via alias
```

### Gitignore — remove already-tracked files

```bash
git ls-files -ci --exclude-standard   # See tracked-but-ignored files
git rm --cached <file>
git rm --cached -r <directory>
git check-ignore -v <file>            # Show which rule matches
```

### Search commit history

```bash
git log --all --grep="text"
git grep "text" $(git rev-list --all)
```

### Change remote URL

```bash
git remote set-url origin <new-url>
git remote set-url origin git@github-cgalvisleon:<repo>.git
```

### Remove sensitive data

- **Local only**: `git rhs` or `git ri` (drop the commit interactively)
- **Already pushed**: `git ric <parent-id>` → drop → `git fpush`
- **Across many commits**: `git dropc "text"` or `git dropf <file>` → `git fpush` (requires `brew install git-filter-repo`)

> If already cloned by others, rotate/revoke the exposed credentials — force push doesn't erase what others downloaded.

## SSH Multi-Account Setup

```bash
ssh-keygen -t ed25519 -C "user@email.com" -f ~/.ssh/<name>
eval "$(ssh-agent -s)"
ssh -T git@github-personal          # Test the connection
```

`~/.ssh/config` pattern:

```
Host github-personal
  HostName github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/<personal-key>

Host github-work
  HostName github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/<work-key>
```

Remotes use the host alias: `git remote add origin git@github-personal:<repo>.git`
