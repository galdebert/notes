# git commit all

including untracked files
```
git add -A && git commit -m mymessage
```


<!-------------------------------------------------------------------------------------------------------->

# Normalize EOL to what git clone gives you

MAKE SURE ALL YOUR WIP IS COMMIT, and then:
```
git rm --cached -r .
git reset --hard
```


<!-------------------------------------------------------------------------------------------------------->

# smartgit: check diff of 2 previous versions of a file

- use Log in smartgit
- select 2 commits using CTRL
- select a file on the right
=> will show the diff of the file versions at those 2 commits 

# smartgit: when merging a file, check each side difference with the common base

Use the the super useful diff with base buttton


<!-------------------------------------------------------------------------------------------------------->

# Create a patch for a list a commits

https://stackoverflow.com/questions/2217452/in-git-how-do-i-create-a-single-patch-for-the-last-2-revisions

## Produce 2 patch files:
`git format-patch HEAD~2..HEAD`

## Produce 1 patch files without the format-patch's per-commit metadata:
`git diff HEAD~2..HEAD > my-patch.diff`

## Produce 1 patch files with the format-patch's per-commit metadata, but applying the patch will create 2 commits.
`git format-patch HEAD~2..HEAD --stdout > moveonnavmeshfix.patch`

## it's often easier to use merge --squash
```
git checkout my-destination-branch
git merge --squash my-branch-with-tons-of-little-commits
git commit
```
or
```
git merge --squash my-commit-id
```

<!-------------------------------------------------------------------------------------------------------->

# submodules

<!------------------------------------------------------>
## How to "git clone" including submodules?

https://stackoverflow.com/questions/3796927/how-to-git-clone-including-submodules

`git clone --recurse-submodules git://github.com/foo/bar.git`

> Is there any way to specify this behavior as default in your git repository, so that less-informed cloners will automatically get an initialized submodule?
> Sadly, no. (Not that I know of, at least.)

<!------------------------------------------------------>
## When a submodule was added to a repo you already clones, how to initialize the submodule locally?

`git submodule update --init --recursive`

<!------------------------------------------------------>
## pull the submodules to their current submodule commits

`git submodule update --recursive`

<!------------------------------------------------------>
## pull the submodules to their branch latest commmit (why would you do that??...)

`git pull --recurse-submodules`

https://git-scm.com/docs/gitmodules

`submodule.<name>.ignore`
Defines under what circumstances git status and the diff family show a submodule as modified. The following values are supported:

`dirty`
All changes to the submodule’s work tree will be ignored, only committed differences between the HEAD of the submodule and its recorded state in the superproject are taken into account.

<!------------------------------------------------------>
## How to remove a submodule

Remove the submodule entry from .git/config

`git submodule deinit -f path/to/submodule`

Remove the submodule directory from the superproject's .git/modules directory

`rm -rf .git/modules/path/to/submodule`

Remove the entry in .gitmodules and remove the submodule directory located at path/to/submodule

`git rm -f path/to/submodule`
