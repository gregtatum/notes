| git                           | hg                         |
| ----------------------------- | -------------------------- |
| git show head                 | hg log -p -r tip           |
| git stash                     | hg shelve                  |
| git stash apply               | hg unshelve                |
| git co HASH FILE              | hg revert -r REV FILE      |
| git add -p                    | hg commit --interactive    |
| git cherry-pick               | hg graft -r 345 --base 234 |
| git diff XXX..XXX --name-only | hg status --rev 5a2753613b1b:728e2084c377 |

## Hide a commit:
hg prune REVISION

## Show hidden commits:
hg log --hidden

## Pull a commit from try:
hg pull try -r e2b9546e9469e43745a484112d1b9edca9041a74
