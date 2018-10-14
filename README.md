# Tips and things always forget about git

## Delete branches

```sh
# Delete local branch
git branch -delete feature/name # or
git branch -d feature/name

# Delete local branch (regardless of its push and merge status)
git branch --delete --force feature/name # or
git branch -D feature/name

# Delete remote branch (or tag)
git push origin --delete feature/name # or
git push origin :feature/name
```
