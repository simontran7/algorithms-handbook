# Git

## Setup

1. Fork the official repository
2. Clone my fork
```bash
git clone <my fork's SSH remote URL>
```
3. Add the upstream
```bash
git remote add upstream <official repository's SSH remote URL>
```

## Start new work

````bash
git checkout main
git fetch upstream
git rebase upstream/main
git push origin main
git checkout -b feature/<name>
````

## Daily work

```bash
git add <files>

git commit

git push origin feature/<name>
```

Commit message format:
```
<scope>: <what changed>

<why the change was made or extra context>

<Key: value>
```

## Sync with main before merging

```bash
git fetch upstream
git rebase -i upstream/main # squash and rebase in one step
git push --force-with-lease origin feature/<name>
```

`rebase -i` opens an editor listing your commits. Change `pick` to `squash` (or `s`) on any commit you want folded into the one above it.

> [!NOTE]
> `--force-with-lease` is safer than `--force` since it refuses if someone else pushed since your last fetch.

### If rebase hits a conflict

```bash
# check conflicted files:
git status

# fix the conflict in your editor, then:
git diff --check # check for leftover conflict markers
git add <resolved files>
git rebase --continue

# to bail out entirely:
git rebase --abort
```



