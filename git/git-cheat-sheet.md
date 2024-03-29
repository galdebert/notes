# git config

list the git configs
- `git config --list` 
- `git config --system --list` 
- `git config --global --list` 
- `git config --local --list` 

find/edit the config files
- `git config --system --edit` ex `C:\dev\git\etc\gitconfig`
- `git config --global --edit` ex `C:\Users\theuser\.gitconfig`
- `git config --local --edit`
 
# how to configure the git credential manager

- simply make sure you have `credential.helper=manager`
- run a git command that requires git credentials, the credential manager will ask for your user/password and will remember it

# git commit all

including untracked files
```
git add -A && git commit -m mymessage
```


<!------------------------------------------------------------------------------------------------->

# Normalize EOL to what git clone gives you

MAKE SURE ALL YOUR WIP IS COMMIT, and then:
```
git rm --cached -r .
git reset --hard
```


<!------------------------------------------------------------------------------------------------->

# smartgit: check diff of 2 previous versions of a file

- use Log in smartgit
- select 2 commits using CTRL
- select a file on the right
=> will show the diff of the file versions at those 2 commits 

# smartgit: when merging a file, check each side difference with the common base

Use the the super useful diff with base buttton


<!------------------------------------------------------------------------------------------------->

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

<!------------------------------------------------------------------------------------------------->

# submodules

<!------------------------------------------------------>
## How to "git clone" including submodules?

`git clone --recurse-submodules git://github.com/foo/bar.git`

> Is there any way to specify this behavior as default in your git repository,
> so that `git clone git://github.com/foo/bar.git` does `--recurse-submodules` automatically
> **Sadly, no.**

<!------------------------------------------------------>
## When a submodule was added to a repo you already cloned, how to initialize the submodule locally?

`git submodule update --init --recursive`

<!------------------------------------------------------>
## pull with submodules at their at their revisions stored in superproject

- option 1: `git pull && git submodule update --recursive`
- option 2: `git pull --recurse-submodules`
- option 3: `git config submodule.recurse true` so that `git pull` behaves automatically as `git pull --recurse-submodules`

> NOTE there is a lot of confusion about whether `git pull --recurse-submodules` either
> 1. pulls submodules at their at their **revisions stored in superproject**
> 2. or pulls the submodule **latest commit** in their master branch
>  
> https://git-scm.com/book/en/v2/Git-Tools-Submodules is very clear, **it's 1.**

<!------------------------------------------------------>
## pull all submodules to their latest revision of their master (or another) branch

NOTE IT'S MUCH SIMPLER TO MANUALLY CHECKOUT EACH SUBMODULE AT THE DESIRED COMMIT
- `cd MySubmodule`
- `git checkout branch-or-commit`
- `git pull`
- `cd ..`
- `git commit`
- `git push`

if we still want automatically do this on all submodules, use `git submodule update --remote`, it's equivalent to

for each sub in submodules
- `cd sub`
- `git checkout branch-or-commit`
- `git pull`
- `cd ..`

Read the section "Working on a Submodule" https://git-scm.com/book/en/v2/Git-Tools-Submodules
for more info about `git submodule update --remote` and stuff like `git config -f .gitmodules submodule.MySubmodule.branch dev`

## push with submodules 

When your submodule is on branch and that you use this submodule to commit changes, 
we MUST push the submodule new commits BEFORE pushing the superproject. To ensure this:

`git push --recurse-submodules=check`

`git config push.recurseSubmodules check` so that `git push` behaves automatically as `git push --recurse-submodules=check`


<!------------------------------------------------------>
## How to remove a submodule

Remove the submodule entry from .git/config

`git submodule deinit -f path/to/submodule`

Remove the submodule directory from the superproject's .git/modules directory

`rm -rf .git/modules/path/to/submodule`

Remove the entry in .gitmodules and remove the submodule directory located at path/to/submodule

`git rm -f path/to/submodule`


# How to create a private fork of a public repo

- https://junyonglee.me/github/How-to-make-forked-private-repository/
- https://stackoverflow.com/questions/10065526/github-how-to-make-a-fork-of-public-repository-private
- https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository
