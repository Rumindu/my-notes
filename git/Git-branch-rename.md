To rename a Git branch in your terminal, use the following commands:

**Rename current branch:**

git branch -m new-branch-name
``` bash 
git branch -m new-branch-name
```
**Rename a different branch:**

git branch -m old-branch-name new-branch-name

``` bash
git branch -m old-branch-name new-branch-name
```

If the branch is pushed to remote, update the remote:

``` bash
# Delete the old branch from remote
git push origin :old-branch-name #equal to git push origin --delete old-branch-name
git push origin new-branch-name
git push --set-upstream origin new-branch-name
#Can be combine both 2nd and 3rd commands
#Here -u flag is the shorthand for --set-upstream
git push -u origin new-branch-name
```
Replace `old-branch-name` and `new-branch-name` with your desired names.