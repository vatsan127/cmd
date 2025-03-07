## _init_

```
git init 
```

```
git add <files>
```

```
git commit -m "first commit"
```

```
git branch -M master
```

```
git remote add origin https://github.com/vatsan127/producer-events.git
```

```
git push -u origin master
```

---

## _logs_

```
git log --oneline
```

---

## _cherry-pick_

```
git cherry-pick -m 1 <commit-ID>
```

---

## _amend_

edit Last Commit message

```
git commit --amend -m "new Commit message"
```

add current changes to previous commit

```
git commit --amend --no-edit
```

---

## _commit_

revert last commit

```
git revert HEAD
```

move the commit to Unstage

```
git  reset --soft HEAD~<number_Of_commits>
```

reset the changes to HEAD

```
git reset --hard
```

---

## _alias_

create alias

```
git config --global alias.rm "reset --hard"
```

search existing Alias

```
git config --get-regexp '^alias\.'
```

remove an alias

```
git config --global --unset alias.alias_name
```

Alias created Locally

```
git config --global alias.st "status" &&
git config --global alias.co "checkout" &&
git config --global alias.get "pull origin" &&
git config --global alias.set "push origin" &&
git config --global alias.unstage "reset --" &&
git config --global alias.rh "reset --hard" &&
git config --global alias.cp "cherry-pick -m 1" &&
git config --global alias.cm "commit -m" 
```

---