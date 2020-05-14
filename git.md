# Git and Github Tutorials
These tutorials and links are intended for the git-impaired who want to work with a GUI whenever possible.
For tools,
- [Github Desktop](https://desktop.github.com/) gives almost everything you need
- [GitKraken](https://www.gitkraken.com/git-client) is the best GUI to do more advanced git operations
  - Some things on private repositories require "Pro"
  - Can get pro for free with https://education.github.com/toolbox and then click on the gitkraken icon
- [VSCode GitHub Extension](https://github.com/ubcecon/tutorials/blob/master/vscode.md#general-packages-and-setup) provides an excellent interface for github
  - In particular, it provides clean ways to initiate PRs related to a specific issue, etc.

## Creating Branches and PRs

## Rebasing a PR/branch onto master
If you want to get all of the commits on master that happened since you branched applied to yours.
  - In GitKraken, you grab your branch name onto the master branch, and choose "Rebase XXX onto master"
  - [Interactive Rebase](https://support.gitkraken.com/working-with-repositories/interactive-rebase/) lets you pick specific commits

## Merging
  - The github website is usually where you want to merge PRs if there are no conflicts
  - Otherwise, GitKraken has easy merge support, and good conflict editing: https://support.gitkraken.com/working-with-repositories/branching-and-merging/

## Stash and Pop
- git has a stack where you can keep uncommited changes that you want to move between branches or git operations
- GitKraken allows you to do this with the "Stash" and "Pop" button
  - Anything in the "Unstaged Files" for example, can be put into the stash, then you can remove it from the stack with "Pop".
  
## Creating a Purgatory Branch
You can move files to this branch that you don't want to permanently delete, but also don't want in your main branch.  The orphan branch means it is completely disconnected from your primary branches.
- *Create the branch* With a terminal of any sort (e.g. in vscode) in the main repository
```bash
git checkout --orphan purgatory
git rm -rf . 
echo "# Abandon hope all ye who enter here" > README.md
git add README.md
git commit -a -m "Initial Commit"
git push origin purgatory 
```
- To move files there, at any point
  - Copy the files you want to remove from your main branch to your OS
  - Delete them from the branch and commit
  - Switch the branch to "purgatory" in Github desktop/vscode/gitkraken, move in the file, and commit and push
  - Go back to your main branch
- To recover files, just switch branches
