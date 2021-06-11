## Github Actions Tricks

## Compiling a Latex PDF with GitHub Actions
This tutorial explains how to have a latex document automatically compile and be available whenever the master `.tex` 

Setup:
1. Create and come your your repository, and clone it in vscode or your favorite editor
2. Add in your latex file.  For example, `docs/rough_notes.tex` resides in the path `docs` relative to the root of the repository.  You can change that if you wish.
  - Make sure you are not checking in the `.pdf` or intermediate compilation files by adding `docs/rough_notes.pdf` etc. to the `.gitignore`.
3. Create an orphan branch for the repository to hold the binaries.  The easiest way is in the terminal in vscode with the repo opened.
  ```bash
  git checkout --orphan gh_actions_builds
  git rm -rf . 
  echo "# Compiled Documents" > README.md
  git add README.md
  git commit -a -m "Initial Commit"
  git push origin gh_actions_builds 
  ```
  - In vscode, switch to the `main` branch instead.
4. If you want to protect that branch from accidental removal, go to the github page for the repo, go to `Settings/Branches` and then add a rule for `gh_actions_builds`.  No need to change any settings.
4. On the github site for your repo, click on "Actions"
5. Click "setup a workflow yourself"
6. Copy the following code into it, globally replacing `rough_notes` with your own latex filename, and `docs` with the relative path if necessary.
```yaml
name: latex rough_notes

on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
    paths:
    - 'docs/rough_notes.tex'

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

jobs:
  latex-job:
    runs-on: ubuntu-latest
    steps:
      
      - name: download paper repo
        uses: actions/checkout@v1
      - name: build pdf 
        uses: xu-cheng/latex-action@v2
        with:
          root_file: rough_notes.tex
          working_directory: docs 
      - name: stash pdf
        run: |
          mv docs/rough_notes.pdf $HOME # cache the file
      - name: checkout gh_actions_builds branch
        uses: actions/checkout@v1
        with:
          ref: gh_actions_builds
      - name: commit pdf
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          mv $HOME/rough_notes.pdf $(pwd) # bring it back 
          git add rough_notes.pdf
          git commit -m "Add changes"
      - name:  push pdf
        uses: ad-m/github-push-action@v0.5.0
        with: 
          branch: gh_actions_builds 
          force: false
          github_token: ${{ secrets.GITHUB_TOKEN }}
```
 7. Choose the "Commit", which should add the workflow into your repository
 8. After this, make a modification to the `rough_notes.tex` file, push it to the server, and it should trigger the action.
 9. Add a link to the document in the `README.md` of the repo if you wish, with text like
```md
  [Rough Notes](https://github.com/MYUSERNAME/MYREPOSITORY/blob/gh_actions_builds/rough_notes.pdf)
```
