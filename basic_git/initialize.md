# Initialise our project.
Initialise the `git` repository.
```
$ git init
Initialized empty Git repository in /Users/nicola/mhpc_tmp/git_ex_0/.git/
```
Explore the `.git` directory.
```
$ tree .git/ | more
.git/
├── HEAD
├── branches
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── prepare-commit-msg.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```
See whath's the status:
```
$ git status
On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```
Let's add something.
```
$ echo "ciao" > first.txt
$ echo "ciao" >> first.txt
$ echo "ciao belli" >> first.txt
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	first.txt

nothing added to commit but untracked files present (use "git add" to track)
```
`git` is telling us that it has nevere seen the file `first.txt`. Now add it and see what happens.
```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   first.txt
```
*Changes to be committed* means that the file is known to git. Now try to explore the directory.
```
$ tree .git/ | more
.git/
├── HEAD
├── branches
├── config
├── description
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── prepare-commit-msg.sample
│   └── update.sample
├── index
├── info
│   └── exclude
├── objects
│   ├── 90
│   │   └── 4fbfa62ccd558fb7ef9eb52ffe47c91be39d2b
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags

10 directories, 15 files
```
The file `first.txt` is now stored by git. Modify it and check again the status.
```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   first.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   first.txt
```
Part of our file is still in the staging area. The modification we made is in the working directory. To see this strange effect ask 'git' the difference.
```
$ git diff
diff --git a/first.txt b/first.txt
index 904fbfa..38f9d0e 100644
--- a/first.txt
+++ b/first.txt
@@ -1,2 +1,3 @@
 ciao
 ciao belli
+new line
```
Now add the changes and commit.
```
$ git add first.txt 
$ git commit -m "first commit "
[master (root-commit) f8e26ec] first commit
 1 file changed, 3 insertions(+)
 create mode 100644 first.txt
```
`git` is telling us that:
 - we are on master branch.
 - this is a special commit, the `root` one.
 - we have an identifier of our commit.
 - Standard unix permissions.

![alt text](./pics/lifecycle.png)