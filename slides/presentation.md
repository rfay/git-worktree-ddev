# **Git Worktree for Multiple Versions of Same DDEV Proje ct**
### with

<img src="images/ddev-logo.svg" alt="DDEV Logo" class="ddev-logo">

---

## Check out Multiple Versions of a Repo

* `git clone git@github.com:ddev/d11simple site1`
* `git clone git@github.com:ddev/d11simple site2`

---

## Without `name` Every DDEV Project Has Name of directory

In `site1`, `https://site1.ddev.site`

---

## You can Default This behavior with DDEV

`ddev config global --omit-project-name-by-default`

---

## Get database and files in a useful place

```
mkdir .tarballs
ddev export-db --file=.tarballs/db.sql.gz
tar -C web/sites/default/files -czf .tarballs/files.tgz .
```

--- 

## `git worktree` lets you do this with projects that share `.git`

`git worktree add ~/tmp/site3`

Automatically creates a checkout with the branch name `site3`

```
cd ~/tmp/site3
ddev start
ddev import-db --file=~/workspace/d11simple/.tarballs/db.sql.gz
ddev import-files --source=~/workspace/d11simple/.tarballs/files.tgz
```
---

## Remember the tools

`git worktree` shows you the options, but

```
git worktree add <path> 
git worktree list
git worktree remove <name>
```

## Summary

* Remove `name` from your project's `.ddev/config.yaml` and the project takes the name of directory it's in
* Consider `ddev config global --omit-project-name-by-default`
* `git worktree add <path>`
* Load a database and/or files into the alternate project