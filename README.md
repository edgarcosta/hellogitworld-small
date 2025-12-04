# original clone
```
WD=/Users/edgarcosta/projects/subrepo
cd $WD
git clone git@github.com:edgarcosta/hellogitworld.git big
cd big
git branch -M main
git push -u origin main
git remote add small git@github.com:edgarcosta/hellogitworld-small.git


# Split
```
git subrepo init src -r small -b main --method=rebase
git log -n3 --oneline --graph                                           ✔
* fd19712 (HEAD -> main) git subrepo push src
* db2cb4e git subrepo init --remote=small --branch=main src
* 0eec97c (origin/master, origin/main, origin/HEAD) add logs
git log -n1                                                             ✔
commit fd197123b34fb7454ae615c91e392c759bc3c725 (HEAD -> main)
Author: Edgar Costa <edgarc@mit.edu>
Date:   Thu Dec 4 16:14:38 2025 +1100

    git subrepo push src

    subrepo:
      subdir:   "src"
      merged:   "be0ae27"
    upstream:
      origin:   "small"
      branch:   "main"
      commit:   "be0ae27"
    git-subrepo:
      version:  "0.4.9"
      origin:   "https://github.com/ingydotnet/git-subrepo"
      commit:   "8bbc88c"
```


# Mixed commit


## On big add file1 and src/file2

```
cd $WD/big
date > file1 ; sleep 1; date > src/file2
git add file1 src/file2
git commit -m "files with dates"
git subrepo push src
git log -n2 --oneline                                               INT ✘
d072cca (HEAD -> main) git subrepo push src
3a26b4e files with dates
############ not yet pushed
(date ; cat src/file2) | sponge src/file2
git commit -m "more dates" src/file2
git log -n2 --oneline
d03ee89 (HEAD -> main) more dates
d072cca (origin/main) git subrepo push src
 ```


## On small modify src/file2 and update src/README.md
```
cd $WD/small
git pull
git log -n1 --oneline                                                 ✔
9ec63a7 (HEAD -> main, origin/main) files with dates
date >> file2
git commit -m "new date and README" file2 README.md
git push
git log -n2 --oneline
ce9e9d1 (HEAD -> main, origin/main) new date and README
9ec63a7 files with dates
```


## On big get the changes

```
git subrepo pull src
git log -n3 --oneline --graph                                      ✔  3s
* 9751b1c (HEAD -> main) git subrepo pull src
* d03ee89 more dates
* d072cca (origin/main) git subrepo push src
```

# How do I get rid of the squash?


