# Git

## Init

Start a new repository and push it to a remote.

```sh
git init
git add <files>
git commit -m "first commit"
git branch -M master
git remote add origin https://github.com/vatsan127/producer-events.git
git push -u origin master
```

---

## Inspect

Show commit history, one line per commit.

```sh
git log --oneline
```

---

## Amend

Edit the last commit message.

```sh
git commit --amend -m "new commit message"
```

Add current changes to the previous commit.

```sh
git commit --amend --no-edit
```

---

## Undo

Move the last N commits back to unstaged (keep the changes).

```sh
git reset --soft HEAD~<number_of_commits>
```

Reset all changes back to HEAD (discard the changes).

```sh
git reset --hard
```

Revert the last commit with a new commit.

```sh
git revert HEAD
```

---

## Cherry-pick

Apply a specific commit onto the current branch.

```sh
git cherry-pick -m 1 <commit-ID>
```

---

## Alias

### Manage

Create an alias.

```sh
git config --global alias.rm "reset --hard"
```

Search existing aliases.

```sh
git config --get-regexp '^alias\.'
```

Remove an alias.

```sh
git config --global --unset alias.alias_name
```

### Full setup

Full global config and aliases in one block.

```sh
git config --global user.email "vatsan127@gmail.com" && \
git config --global user.name "vatsan127" && \
git config --global alias.st "status" && \
git config --global alias.co "checkout" && \
git config --global alias.get "pull origin" && \
git config --global alias.set "push origin" && \
git config --global alias.unstage "reset --" && \
git config --global alias.rh "reset --hard" && \
git config --global alias.cp "cherry-pick -m 1" && \
git config --global alias.cm "commit -m"
```
