# Split tree
git subtree split --prefix=src -b src-split
git remote add src git@github.com:edgarcosta/hellogitworld-src.git
git push src src-split:main
git branch -D src-split

# Re add src as subtree
git switch master
git rm -r src
git commit -m "Remove src to re-add as subtree"
git fetch src main
git subtree add --prefix=src src main

# Do a commit on the monorepo

## commit
echo "#1" > src/README.md
git add src/README.md
git commit -m "adding README"

## push changes
git push
git subtree push --prefix=src src main


# Update standalone
git pull
git commit -am "instructions"
git push

