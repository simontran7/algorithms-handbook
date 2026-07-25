# Git

## Setting Up

- Initialize an existing directory as a Git repository

```text
git init
```

- Clone a specified remote repository

```text
git clone <remote repository url>
```

- Specifies the remote repository for your local repository.

```text
git remote add origin <remote repository url>
```

## Staging

- Show modified files in working directory, and files staged for your next commit

```text
git status
```

- Add a file as it looks now to your next commit

```text
git add <file 1> ... <file N>
```

- Unstage a file while retaining the changes in working directory

```text
git restore --staged <file 1> ... <file N>
```

## Committing

- Commit the staged content as a new commit snapshot

```text
git commit 
```

> [!NOTE]
> Scoped commit message style:
> ```text
> <scope>: <what changed>
> 
> <why the change was made or extra context>
> 
> <Key: value>
> ```

- Modify the previous commit's message

```text
git commit --amend -m "<new commit message>"
```

- Squashing commits

```text
git rebase -i <remote>/<branch>
```

Your text editor will pop up with a file looking as follows:

```
pick <hash> <message>
pick <hash> <message>
pick <hash> <message>
...
squash <hash> <message>
```

Change all the `pick` to squash except the first line as follows:

```
pick <hash> <message>
squash <hash> <message>
squash <hash> <message>
...
squash <hash> <message>
```

Save and close the file. 

Then, another text editor window will open which will let you combine the commit messages from all of the commits into a single commit message.

## Branching

- Display local branches

```text
git branch
```

- Display remote branches

```text
git branch -r 
```

- Create a branch 

```text
git branch <branch>
```

- Rename a branch

```text
git branch -m <branch to rename> <new branch name>
```

- Switch to a branch

```text
git switch <branch>
```

- Delete a branch

```text
git branch -d <branch>
```

- Delete a branch with unmerged changes

```text
git branch -D <branch>
```

- Delete a remote branch

```text
git push origin --delete <remote branch>
```

## Inspecting & Comparing

- Show the commit history for the current branch

```text
git log
```

- Show a condensed commit history as a graph, including all branches

```text
git log --oneline --graph --all
```

- Show unstaged changes in the working directory

```text
git diff
```

- Show staged changes (what will go into the next commit)

```text
git diff --staged
```

- Show the difference between two branches or commits

```text
git diff <branch or commit A> <branch or commit B>
```

- Show who last modified each line of a file, and in which commit

```text
git blame <file>
```

- Show the details and changes of a specific commit

```text
git show <commit>
```

- Move the `HEAD` pointer to a commit

```text
git switch --detach <commit> or HEAD<relative reference>
```

> [!NOTE]
> Checking out a commit causes the `HEAD` pointer to be in a detached head state, where any commits won't belong to any branches, and will be lost when you switch away (unless you run `git switch -c <new branch>` first to keep them).

## Merging & Rebasing

- Merge a branch into the current branch

```text
git merge <from branch>
```

- Replay the current branch's commits on top of a target branch

```text
git rebase <from branch>
```

> [!NOTE]
> Squashing is done inside an interactive rebase: mark commits with `squash` (or `s`) to combine them into the commit above.

- Abort a merge or rebase that has conflicts and return to the previous state

```text
git merge --abort
git rebase --abort
```

> [!NOTE]
> When to use rebase vs merge:
> - Updating your private stuff from upstream: rebase 
> - Landing your stuff into shared branches: merge

## Stashing 

- Save all staged and unstaged changes

```text
git stash
```

- List stack-order of stashed file changes

```text
git stash list
```

- Show a summary of the files changed in the most recent stash 

```text
git stash show stash@{<index>}
```

- Write the most recent stash back to working copy and removes it from the top of the stash stack

```text
git stash pop
```

- Write the most recent stash back to working copy and does *not* remove it from the top of the stash stack

```text
git stash apply
```

- Discard the changes from top of stash stack

```text
git stash drop
```

## Undoing Things

- Move the current branch back to a commit, keeping changes staged (`--soft`), unstaged (`--mixed`) — the default — or discarding them entirely (`--hard`)

```text
git reset [--soft | --mixed | --hard] <commit>
```

- Create a new commit that reverses the changes of a previous commit

```text
git revert <commit>
```

## Syncing

- Download commits and branches from the remote without changing your working directory

```text
git fetch <remote>
```

- Fetch from the remote and rebase the current branch's local commits on top of the remote branch, instead of merging

```text
git pull --rebase
```

## Pushing

- Push a branch to the remote 

```text
git push <remote> <branch>
```

- Push a branch that you've never pushed before to the remote

```text
git push -u origin <branch>
```