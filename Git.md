# Git

## Branches

### Deleting 
 
git branch -d feature/login
git push origin --delete feature/login

## Remove a Git init

Just delete the .git file: ``rm -rf .git`` 

## Recover deleted branched with git reflog

1 - Checkout the branch you originally branched from
2 - type 'git reflog'
3 - Find the SHA number referencing a commit to the deleted branch
4 - type 'git checkout -b <branch> <sha>'

## Rename Git branch

When on the branch:

git branch -m new-name
git push origin -u new-name

When on a different branch:

git branch -m old-name new-name
git push origin :old-name new-name