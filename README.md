flaming-adventure
=================

Testing auto PR merging on local command line.

## master change

Advance the mainline.


## The general idea



```bash
# $1 = branch name

git checkout dev  # Start on dev.
git pull origin dev  # Make sure it's up to date.
git fetch origin  # Make sure we have all available branches.
git checkout $1  # Switch to the feature branch in question.

if [ branch does not extend from dev's tip ]
	git rebase dev  # Rebase the branch on top of dev.
	git push origin $1 -f  # Force the rebased branch back to origin.
fi

git checkout dev  # Switch back to dev to prepare for merging.
git merge --no-ff $1  # Merge in the feature, but don't just fast forward. (Gives us the nice "bubble" in the commit history.)


git push origin dev  # Push the merge to Github. (Should close the PR but not delete the branch.)
git branch -d $1  # Delete the local (now-merged) branch.
git branch -d origin/$1  # Delete the local copy of the remote branch.
#git push origin :$1  # Delete the remote branch(?)
```

## License

MIT