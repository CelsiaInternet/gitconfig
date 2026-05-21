# Git config

## Configuración inicial

```bash
git config --global user.email "user@gmail.com"
git config --global user.name "Your Name"
git config --global init.defaultBranch main
```

Config local (Work):

```bash
git config --local user.email "user@company.com"
git config --local user.name "Your Name"
```

---

## Setup de aliases — macOS / Linux / Git Bash

Ejecutar una sola vez para registrar todos los aliases:

```bash
# Vista
git config --global alias.l "log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all"
git config --global alias.s "status -s -b"
git config --global alias.v "! git describe --tags --abbrev=0"
git config --global alias.b "! git describe --tags --abbrev=1"

# Ramas
git config --global alias.new "! git checkout -b $1"
git config --global alias.set "! git checkout $1"
git config --global alias.del "! git branch -D $1"
git config --global alias.rn "! git branch -m $1"
git config --global alias.main "! git branch -M main"
git config --global alias.lb "! git branch -v"
git config --global alias.lba "! git branch -a"
git config --global alias.lbr "! git branch -r"
git config --global alias.upstream "! git push --set-upstream origin $1"
git config --global alias.up "! git push -u origin"
git config --global alias.odel "! git push origin --delete $1 $2"
git config --global alias.orn "! git push origin --delete $1; git push origin $2"
git config --global alias.set-head "! git remote set-head origin"

# Pull
git config --global alias.get "! git pull origin $1"
git config --global alias.getall "! git pull origin"
git config --global alias.bring "! git pull origin $1"

# Commit + push (origin)
git config --global alias.prepare '! prepare() { git add . && git commit -m "Prepare:$1"; }; prepare'
git config --global alias.initial '! initial() { git add . && git commit -m "Initial:$1" && git push -u origin --all; }; initial'
git config --global alias.update '! update() { git add . && git commit -m "Update:$1" && git push -u origin; }; update'
git config --global alias.upd '! upd() { git add . && git commit -m "Update:$1" && git push -u origin; }; upd'
git config --global alias.backup '! backup() { git add . && git commit -m "Backup:$1" && git push -u origin; }; backup'
git config --global alias.feat '! feat() { git add . && git commit -m "Feat:$1" && git push -u origin; }; feat'
git config --global alias.review '! review() { git add . && git commit -m "Review:$1" && git push -u origin; }; review'
git config --global alias.fix '! fix() { git add . && git commit -m "Fix:$1" && git push -u origin; }; fix'
git config --global alias.bug '! bug() { git add . && git commit -m "Bug:$1" && git push -u origin; }; bug'
git config --global alias.deploy '! deploy() { git add . && git commit -m "Deploy:$1" && git push -u origin; }; deploy'
git config --global alias.down '! down() { git add . && git commit -m "Down:$1" && git push -u origin; }; down'
git config --global alias.rollback '! rollback() { git add . && git commit -m "Rollback:$1" && git push -u origin; }; rollback'
git config --global alias.merge '! merge() { git add . && git commit -m "Merge:$1" && git push -u origin; }; merge'

# Reset
git config --global alias.rhs "git reset HEAD^ --soft"
git config --global alias.rhh "git reset HEAD^ --hard"
git config --global alias.clean "git rm -r --cached ."
git config --global alias.chout "! git checkout -- $1"

# Rebase interactivo
git config --global alias.ri '! ri() { git rebase -i HEAD~${1:-3}; }; ri'
git config --global alias.ric '! ric() { git rebase -i $1; }; ric'
git config --global alias.fpush '! git push origin $(git rev-parse --abbrev-ref HEAD) --force'

# Borrar del historial (requiere: brew install git-filter-repo)
git config --global alias.dropc '! dropc() { git filter-repo --force --commit-callback "if b\"$1\" in commit.message: commit.drop()"; }; dropc'
git config --global alias.dropf '! dropf() { git filter-repo --path "$1" --invert-paths --force; }; dropf'

# Tags
git config --global alias.tag "! git tag $1"
git config --global alias.tags "! git push -u origin --tags"
git config --global alias.tago "! git ls-remote --tags origin"
git config --global alias.tagdel "! git tag -d $1"
git config --global alias.tagodel "! git push origin --delete $1"

# Meta
/
```

## Setup de aliases — Windows CMD

> Usar en **cmd.exe** o **PowerShell**. Diferencia con bash: comillas externas `"` y comillas internas escapadas con `\"`.
> Si usas **Git Bash en Windows**, usa el bloque anterior (es idéntico).

```cmd
REM Vista
git config --global alias.l "log --graph --abbrev-commit --decorate --date=relative --format=format:'%%C(bold blue)%%h%%C(reset) - %%C(bold green)(%%ar)%%C(reset) %%C(white)%%s%%C(reset) %%C(dim white)- %%an%%C(reset)%%C(bold yellow)%%d%%C(reset)' --all"
git config --global alias.s "status -s -b"
git config --global alias.v "! git describe --tags --abbrev=0"
git config --global alias.b "! git describe --tags --abbrev=1"

REM Ramas
git config --global alias.new "! git checkout -b $1"
git config --global alias.set "! git checkout $1"
git config --global alias.del "! git branch -D $1"
git config --global alias.rn "! git branch -m $1"
git config --global alias.main "! git branch -M main"
git config --global alias.lb "! git branch -v"
git config --global alias.lba "! git branch -a"
git config --global alias.lbr "! git branch -r"
git config --global alias.upstream "! git push --set-upstream origin $1"
git config --global alias.up "! git push -u origin"
git config --global alias.odel "! git push origin --delete $1 $2"
git config --global alias.orn "! git push origin --delete $1; git push origin $2"
git config --global alias.set-head "! git remote set-head origin"

REM Pull
git config --global alias.get "! git pull origin $1"
git config --global alias.getall "! git pull origin"
git config --global alias.bring "! git pull origin $1"

REM Commit + push (origin)
git config --global alias.prepare "! prepare() { git add . && git commit -m \"Prepare:$1\"; }; prepare"
git config --global alias.initial "! initial() { git add . && git commit -m \"Initial:$1\" && git push -u origin --all; }; initial"
git config --global alias.update "! update() { git add . && git commit -m \"Update:$1\" && git push -u origin; }; update"
git config --global alias.upd "! upd() { git add . && git commit -m \"Update:$1\" && git push -u origin; }; upd"
git config --global alias.backup "! backup() { git add . && git commit -m \"Backup:$1\" && git push -u origin; }; backup"
git config --global alias.feat "! feat() { git add . && git commit -m \"Feat:$1\" && git push -u origin; }; feat"
git config --global alias.review "! review() { git add . && git commit -m \"Review:$1\" && git push -u origin; }; review"
git config --global alias.fix "! fix() { git add . && git commit -m \"Fix:$1\" && git push -u origin; }; fix"
git config --global alias.bug "! bug() { git add . && git commit -m \"Bug:$1\" && git push -u origin; }; bug"
git config --global alias.deploy "! deploy() { git add . && git commit -m \"Deploy:$1\" && git push -u origin; }; deploy"
git config --global alias.down "! down() { git add . && git commit -m \"Down:$1\" && git push -u origin; }; down"
git config --global alias.rollback "! rollback() { git add . && git commit -m \"Rollback:$1\" && git push -u origin; }; rollback"
git config --global alias.merge "! merge() { git add . && git commit -m \"Merge:$1\" && git push -u origin; }; merge"

REM Reset
git config --global alias.rhs "git reset HEAD^ --soft"
git config --global alias.rhh "git reset HEAD^ --hard"
git config --global alias.clean "git rm -r --cached ."
git config --global alias.chout "! git checkout -- $1"

REM Rebase interactivo
git config --global alias.ri "! ri() { git rebase -i HEAD~${1:-3}; }; ri"
git config --global alias.ric "! ric() { git rebase -i $1; }; ric"
git config --global alias.fpush "! git push origin $(git rev-parse --abbrev-ref HEAD) --force"

REM Borrar del historial (requiere: brew install git-filter-repo)
git config --global alias.dropc "! dropc() { git filter-repo --force --commit-callback \"if b\\\"$1\\\" in commit.message: commit.drop()\"; }; dropc"
git config --global alias.dropf "! dropf() { git filter-repo --path \"$1\" --invert-paths --force; }; dropf"

REM Tags
git config --global alias.tag "! git tag $1"
git config --global alias.tags "! git push -u origin --tags"
git config --global alias.tago "! git ls-remote --tags origin"
git config --global alias.tagdel "! git tag -d $1"
git config --global alias.tagodel "! git push origin --delete $1"

REM Meta
git config --global alias.aliases "! printf 'Vista:      l  s  v  b\nRamas:      new  set  del  rn  main  lb  lba  lbr  upstream  up  odel  orn  set-head\nPull:       get  getall  bring\nCommit:     prepare  initial  update  upd  backup  feat  review  fix  bug  deploy  down  rollback  merge\nReset:      rhs  rhh  clean  chout  ri  ric  fpush  dropc  dropf\nTags:       tag  tags  tago  tagdel  tagodel\n'"
```

---

## Referencia de aliases

### Vista

| Alias | Uso     | Descripción       |
| ----- | ------- | ----------------- |
| `l`   | `git l` | Log gráfico       |
| `s`   | `git s` | Estado corto      |
| `v`   | `git v` | Última versión    |
| `b`   | `git b` | Versión abreviada |

### Ramas

| Alias      | Uso                       | Descripción         |
| ---------- | ------------------------- | ------------------- |
| `new`      | `git new <rama>`          | Crear rama          |
| `set`      | `git set <rama>`          | Cambiar rama        |
| `del`      | `git del <rama>`          | Borrar rama local   |
| `rn`       | `git rn <rama>`           | Renombrar rama      |
| `main`     | `git main`                | Renombrar a main    |
| `lb`       | `git lb`                  | Listar ramas        |
| `lba`      | `git lba`                 | Listar todas        |
| `lbr`      | `git lbr`                 | Listar remotas      |
| `pb`       | `git pb <rama>`           | Publicar rama       |
| `odel`     | `git odel <rama>`         | Borrar rama origin  |
| `orn`      | `git orn <vieja> <nueva>` | Renombrar en origin |
| `set-head` | `git set-head`            | Actualizar HEAD     |

### Pull

| Alias    | Uso                | Descripción       |
| -------- | ------------------ | ----------------- |
| `get`    | `git get <rama>`   | Pull desde origin |
| `getall` | `git getall`       | Pull todo origin  |
| `bring`  | `git bring <rama>` | Pull rama origin  |

### Commit + Push — origin

| Alias      | Uso                    | Descripción     |
| ---------- | ---------------------- | --------------- |
| `prepare`  | `git prepare "<msg>"`  | Commit sin push |
| `initial`  | `git initial "<msg>"`  | Commit inicial  |
| `update`   | `git update "<msg>"`   | Commit update   |
| `upd`      | `git upd "<msg>"`      | Commit update   |
| `backup`   | `git backup "<msg>"`   | Commit backup   |
| `feat`     | `git feat "<msg>"`     | Commit feat     |
| `review`   | `git review "<msg>"`   | Commit review   |
| `fix`      | `git fix "<msg>"`      | Commit fix      |
| `bug`      | `git bug "<msg>"`      | Commit bug      |
| `deploy`   | `git deploy "<msg>"`   | Commit deploy   |
| `down`     | `git down "<msg>"`     | Commit down     |
| `rollback` | `git rollback "<msg>"` | Commit rollback |
| `merge`    | `git merge "<msg>"`    | Commit merge    |

### Reset

| Alias   | Uso                   | Descripción                                        |
| ------- | --------------------- | -------------------------------------------------- |
| `rhs`   | `git rhs`             | Reset soft HEAD^                                   |
| `rhh`   | `git rhh`             | Reset hard HEAD^                                   |
| `clean` | `git clean`           | Limpiar caché                                      |
| `chout` | `git chout <archivo>` | Descartar cambios                                  |
| `ri`    | `git ri [n]`          | Rebase interactivo últimos n commits (default 3)   |
| `ric`   | `git ric <id>`        | Rebase interactivo desde un commit                 |
| `fpush` | `git fpush`           | Force push a la rama activa                        |
| `dropc` | `git dropc "<texto>"` | Borra commits que contengan el texto del historial |
| `dropf` | `git dropf <archivo>` | Borra un archivo completo del historial            |

### Tags

| Alias     | Uso                    | Descripción        |
| --------- | ---------------------- | ------------------ |
| `tag`     | `git tag <nombre>`     | Crear tag local    |
| `tags`    | `git tags`             | Publicar tags      |
| `tago`    | `git tago`             | Listar tags origin |
| `tagdel`  | `git tagdel <nombre>`  | Borrar tag local   |
| `tagodel` | `git tagodel <nombre>` | Borrar tag origin  |

### Meta

| Alias     | Uso           | Descripción                           |
| --------- | ------------- | ------------------------------------- |
| `aliases` | `git aliases` | Lista todos los aliases por categoría |

---

## Técnicas

### Merge y conflictos

```bash
git merge <rama>
git merge -X theirs <rama>     # Acepta todos los cambios de <rama>
git rebase origin/<rama>

git checkout --theirs .        # Acepta cambios de origin
git checkout --ours .          # Acepta cambios locales
git checkout --theirs <file>
git checkout --ours <file>

git rhs   # Reset soft: deshace commit, conserva cambios
git rhh   # Reset hard: deshace commit y cambios

git reset <id> --soft
git reset <id> --hard
```

### Descartar cambios en un archivo

```bash
git checkout -- <file>
git checkout origin/<rama> -- <file>
```

### Gitignore — quitar archivos ya rastreados

```bash
git ls-files -ci --exclude-standard    # Ver archivos ignorados pero rastreados
git rm --cached <file>
git rm --cached -r <directorio>
git check-ignore -v <file>             # Verificar regla que lo ignora
```

### Borrar commits con datos sensibles

**Caso 1 — Commit aún NO está en GitHub (solo local)**

```bash
git rhs        # Reset soft: deshace el commit, conserva los cambios en staging
git rhh        # Reset hard: deshace el commit y descarta los cambios

git ri         # Rebase interactivo últimos 3 commits (usa "drop" para eliminar)
git ri 5       # Rebase interactivo últimos 5 commits
```

**Caso 2 — Commit YA está en GitHub**

```bash
git log --oneline              # Identificar el commit a eliminar
git ric <id-commit-anterior>   # Rebase interactivo desde ese punto (usa "drop")
git fpush                      # Force push a la rama activa (reescribe el historial remoto)
```

**Caso 3 — Dato sensible en múltiples commits (requiere: brew install git-filter-repo)**

```bash
# Eliminar commits que contengan un texto en el mensaje
git dropc "texto-sensible"

# Eliminar un archivo completo del historial
git dropf archivo-secreto.txt
git fpush
```

> **Importante:** Si el commit ya estaba en GitHub y otros lo clonaron, revoca o rota las credenciales expuestas — el `--force` no borra lo que otros ya descargaron.

### Historial — buscar commits

```bash
git log --all --grep="texto"
git grep "texto" $(git rev-list --all)
```

### Remoto — cambiar URL

```bash
git remote set-url origin <nueva-url>
git remote set-url origin git@github-work:CompanyOrg/<repo>.git
```

---

## SSH — múltiples cuentas

```bash
ssh-keygen -t ed25519 -C "user@gmail.com" -f ~/.ssh/<name>
eval "$(ssh-agent -s)"
ssh -T git@github-personal

# Agregar remote con host alias
git remote add origin git@github-personal:<repo>.git
git remote add origin git@github-work:<repo>.git
```

Archivo `~/.ssh/config`:

```
Host github-personal
  HostName github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/<name>

Host github-work
  HostName github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/<name>
```
