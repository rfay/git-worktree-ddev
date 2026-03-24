# **Git Worktree for Multiple Versions of Same DDEV Project**
### with

<img src="images/ddev-logo.svg" alt="DDEV Logo" class="ddev-logo">

Presentation is at https://rfay.github.io/git-worktree-ddev/

---

## Check out Multiple Versions of a Repo


`git clone git@github.com:ddev/d11simple fancy-feature-1`

`git clone git@github.com:ddev/d11simple fancy-feature-2`
```

---

## Without `name` Every DDEV Project Has Name of directory

In `fancy-feature-1`, `https://fancy-feature-1.ddev.site`

---

## You can default this behavior with DDEV

`ddev config global --omit-project-name-by-default`

---

## Get database and files in a useful place

```
mkdir .tarballs
ddev export-db --file=.tarballs/db.sql.gz
```

`tar -C web/sites/default/files -czf .tarballs/files.tgz .`

---

## `git worktree` lets you do this with projects that share `.git`

In `~/workspace/D11SIMPLE`:

```bash
git clone git@github.com:ddev/d11simple
cd d11simple
git worktree add ../fancy-feature-1
git worktree add ../fancy-feature-2
```

Automatically creates a checkout with the branch name `fancy-feature-1` or `fancy-feature-2` that matches the directory name.

---

## Sample Layout

```
D11SIMPLE/
├── d11simple
├── fancy-feature-1
└── fancy-feature-2
```

---

## Import your db and files

```
cd fancy-feature-1
ddev start
ddev import-db --file=../.tarballs/db.sql.gz
ddev import-files --source=../.tarballs/files.tgz
```

---

## Remember the tools

`git worktree` shows you the options, but

```
git worktree add <path>  # Usually relative
git worktree list
git worktree remove <name>
```

---

## Summary

* Remove `name` from your project's `.ddev/config.yaml` and the project takes the name of directory it lives in
* Consider `ddev config global --omit-project-name-by-default`
* `git worktree add <path>`
* Load a database and/or files into the alternate project
* Presentation is at https://rfay.github.io/git-worktree-ddev/