# Git Experiment: Branch / Merge / Mergesquash

Experiment tests the workflow where there is a master branch, user checks
out feature branch from master branch. User commits work to feature branch.
Work continues in parallel in master branch. User on feature branch merges
master `32700`, does a push to GitHub. Finally `32703` on master, merges
in feature branch with `--squash`, and commits the commit message.


```
32680  echo "#1" >> 1
32681  git add -A && git commit -m "#1"
32682  echo "#2" >> 1
32683  git commit -am "#2"
32684  git push origin master

32685  git checkout -b feature
32686  echo "#a" >> a
32687  git add -A && git commit -m "#a"
32688  echo "#b" >> a
32689  git commit -am "#b"
32690  git push origin feature

32691  git checkout master
32692  echo "#3" >> 1
32693  git commit -am "#3"
32694  echo "#4" >> 1
32695  git commit -am "#4"
32696  git push origin master

32697  git checkout feature
32698  echo "#c" >> a
32699  git commit -am "#c"
32700  git merge master
32701  git push origin feature

32702  git checkout master
32703  git merge feature --squash
32705  git commit -am "#5"
32706  git push origin master
```

## Final History log
1. #5 - `git merge feature --squash` (includes #c, #b, #a)
1. #4
1. #3
1. #2
1. #1
