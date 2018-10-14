# Tips and things always forget about git

## Delete branches

```sh
# Delete local branch
$ git branch -delete feature/name # or
$ git branch -d feature/name

# Delete local branch (regardless of its push and merge status)
$ git branch --delete --force feature/name # or
$ git branch -D feature/name

# Delete remote branch (or tag)
$ git push origin --delete feature/name # or
$ git push origin :feature/name
```

## Update author info

```sh
# bare clone the repo
$ git clone --bare https://github.com/user/repo.git
$ cd repo.git

# rewrite author info (update OLD_EMAIL, CORRECT_NAME & CORRECT_EMAIL before run it)
$ git filter-branch --env-filter '
OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags

# Push the corrected history to remote
$ git push --force --tags origin 'refs/heads/*'
```

## Manually merge a GitHub PR

Create a PR in GitHub to merge branch `release\1.0.0` back to `master`

```sh
git checkout release/1.0.0
git pull
git submodule update --init

git checkout master
git pull

git merge --no-ff release/1.0.0
git push origin master
```

## Amending the last commit

To change the last commit, you can simply commit again, using the `--amend` flag:

```sh
git commit --amend -m "New and correct message"
```

