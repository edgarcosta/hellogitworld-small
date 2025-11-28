# Create subtree

## Save history before split

```
git push origin master_before_split
```

## Split tree

```
git subtree split --prefix=src -b src-split
git remote add src git@github.com:edgarcosta/hellogitworld-src.git
git push src src-split:main
git branch -D src-split
```

## Re add src as subtree

```
git switch master
git rm -r src
git commit -m "Remove src to re-add as subtree"
git fetch src main
git subtree add --prefix=src src main
```

# Day to day life

Some of these things should be done with hooks

## Do a commit on the monorepo

### pull changes
```
git pull
git subtree pull --prefix=src src main
```
the last one creates a merge commit

### commit
```
echo "#1" > src/README.md
git add src/README.md
git commit -m "adding README"
```

### push changes
```
git push
git subtree push --prefix=src src main
```




## Do a commit on the standalone
```
git pull
....
git commit -am "instructions"
git push
```

Now see the changes in the monorepo
```
git subtree pull --prefix=src src main
git log -n 4 --oneline
git push
git subtree push --prefix=src src main
```


# Update monorepo
# Pull changes
git subtree pull --prefix=src src main
git log -n 4 --oneline

