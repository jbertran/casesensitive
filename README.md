## What is this?

This is an interesting side effect of Linux being case-sensitive, and MacOS/Windows not.
When a Mac/Windows user clones this project, its git status is automatically tainted
by `PROJECTS` being deleted.

```
$ git clone git@github.com:jbertran/casesensitive
[...]
$ cd casesensitive
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    PROJECTS

no changes added to commit (use "git add" and/or "git commit -a")
```

WTF? Let's stash this

```
$ git stash
Saved working directory and index state WIP on master: 75aadfd Add a `PROJECTS` file at the same level
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    projects/Makefile

no changes added to commit (use "git add" and/or "git commit -a")
```

???? What? Stash again?

```
$ git stash
Saved working directory and index state WIP on master: 75aadfd Add a `PROJECTS` file at the same level
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    PROJECTS

no changes added to commit (use "git add" and/or "git commit -a")
```

And so on.
Git may well have case-sensitive information, but it happily translates patches as-is for the file system,
and if the file system is case-insensitive, well...

A fun half hour figuring out this issue.
