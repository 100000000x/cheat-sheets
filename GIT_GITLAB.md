# Git Gitlab

_Stakeholder->ProductOwner->Team Lead->Developer_  
_Diff3/Git is for secure and multi user text file comparison sha chains. Agile is for segmentation of product development stages with more than one developer_  
_Everyone tinkers reversibly, documented, and securely with local and remote SOP precommits, registries, security checks_  

_five working areas in set up git folders/repositories: [working (stash/stash pop) stash] (add filename/reset HEAD) [staging] (git commit) [local] (git push) [remote]_  
_branches: sub sha chains of differences within a repository_  
_logs: search for certain diffs in the sha chains_  
_tags: extra diff chains for set up git folders/repositories for finished version units_  
_commits: reversible additions to a sha chain_  

_commit early, often, with consistent messages, and void of securitry and other misc files_  

git gitlab links
```
https://git-scm.com/docs
https://gitlab.com/gitlab-org/gitlab  
https://pre-commit.com/
http://ndpsoftware.com/git-cheatsheet.html
https://swcarpentry.github.io/git-novice/ ﻿
https://firstaidgit.io/
https://gitexplorer.com/
https://learngitbranching.js.org/
```
git set up
```
apt install git-all
~/.gitconfig

[user]
    name = user
    email = user@email.com

[core]
    editor = vim
```
retroactively ignore files
```
echo *.log >> .gitignore
git rm --cached *.log
rm 'instance.log'
git commit -m "Remove log files"
git check-ignore -v files
```
pre-commit hooks
```
pipenv install pre-commit
pre-commit install
pre-commit run --all-files
.pre-commit-config.yaml
repos:
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v2.5.0
    hooks:
    -   id: check-yaml
    -   id: end-of-file-fixer
    -   id: trailing-whitespace
-   repo: https://github.com/psf/black
    rev: 19.10b0
    hooks:
    -   id: black
```
git work area basics
```
git init foldername
git clone --depth -b remoteurl
git status
git add -p -e filename
git diff filename
git log --pretty=oneline --staged --cached -- --word-diff
git checkout --filename
git commit -m --dry-run --short
git reset filename
git rm filename
git stash list branch show pop list drop drop stash@{hash}
```
git branches basics
```
git branch -a branch_name
git checkout -b branch_name
git merge from branch_name
git merge hotfix
git checkout branch_name
git branch -D branch_name
```
git log
```
git log -n 10 --after="YYYY-MM-DD" --before="YYYY-MM-DD" --author = "name" --grep = "term" -S"string" --oneline --graph --decorate
git reflog
```
git tags
```
git tag
git tag -a tagname sha -m
git push origin 0.0.1
git tag -d tagname
git tag -d 0.6.1
git push origin :0.6.1
```
