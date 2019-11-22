# Compiling a Latex PDF with GitHub Actions
This tutorial explains how to have a latex document automatically compile and be available whenever the master `.tex` 

Setup:
1. Create your repository.  For example, `https://github.com/MYUSERNAME/MYREPOSITORY.git`
2. Add in your latex file.  For example, `MYPATH/MYFILE.tex` resides in the path `MYPATH` relative to the root of the repository
  - Make sure you are not checking in the `.pdf` by adding `.pdf` to the `.gitignore`.
3. Create an orphan branch for the respository to hold the binaries.
  - This is easiest to do in a terminal, starting in a location *different* from where you normally work in your files.
  - Open a terminal (e.g. powershell in Windows, or bash in OSX/linux) and go to a location for a temporary repository.  Then execute
  ```bash
  git clone https://github.com/MYUSERNAME/MYREPOSITORY.git
  cd MYREPOSITORY/
  git checkout --orphan docs
  git rm -rf . 
  echo "# Compiled Documents" > README.md
  git add README.md
  git commit -a -m "Initial Commit"
  git push origin docs 
  ```
  - Delete the repository so you don't accidentally use it (e.g. with `rm -rf`)
4. On the github site for your repo, click on "Actions"
5. Click "setup a workflow yourself"
6. Copy the following code into it, replacing MYUSERNAME, MYREPOSITORY, MYPATH, MYFILE appropriately
```yaml
name: MYFILE build chain

on: 
  push:
    paths:
    - 'MYPATH/MYFILE.tex'

jobs:
  latex-job:
    runs-on: ubuntu-latest
    steps:
      
      - name: download paper repo
        uses: actions/checkout@v1
      - name: build pdf 
        uses: xu-cheng/latex-action@1.2.0
        with:
          root_file: MYFILE.tex
          working_directory: MYPATH 
      - name: commit pdf
        run: |
          git checkout docs 
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add MYPATH/MYFILE.pd
          git commit -m "Add changes" -a
      - name:  push pdf
        uses: ad-m/github-push-action@v0.5.0
        with: 
          branch: docs 
          force: false
          github_token: ${{ secrets.GITHUB_TOKEN }}
```
 7. Choose the "Commit", which should add the workflow into your repository
 8. After this, make a modification to the `MYFILE.tex` file, push it to the server, and it should trigger the action.
 9. The document is linked at XXXXX
