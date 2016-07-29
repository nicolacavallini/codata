#  Merging
## Fast Forward
Initialise a first commit on a sample file.
```
$ git init
$ vim first.txt
$ git add first.txt 
$ git commit -m "first"
[master 2d0a6f1] first
 1 file changed, 3 insertions(+), 5 deletions(-)
```
Suppose you need to test a new feature before merging  it.
```
$ git checkout -b test_new
Switched to a new branch 'test_new'
$ vim first.txt
$ git add first.txt
$ git commit -m "added test"
[test_new 14727a5] added test
 1 file changed, 1 insertion(+)
```
```
$ git log --oneline --decorate --graph --all
* c6e3c04 (HEAD, test) added test
* 2f6bf57 (master) first
```
```
$ git checkout master
Switched to branch 'master'
$ git merge test
Updating 2f6bf57..c6e3c04
Fast-forward
 first.txt | 1 +
 1 file changed, 1 insertion(+)
```
```
$ git branch -D test
Deleted branch test (was c6e3c04).
$ git log --oneline --decorate --graph --all
* c6e3c04 (HEAD, master) added test
* 2f6bf57 first
```
## Recursive
```
$ git init
Initialized empty Git repository in /Users/nicola/tmp/test_git/merging/fast_forward/.git/
```

```
vim first.txt
git add first.txt
```
```
$ git commit -m "first commit"
[master (root-commit) 573d299] first commit
 1 file changed, 3 insertions(+)
 create mode 100644 first.txt
```
```
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
```
correct a previously edited line.
```
$ vim first.txt
$ git add first.txt
$ git commit -m "correction on hotfix" 
[hotfix 82d4d56] correction on hotfix
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```
$ git checkout master
Switched to branch 'master'
```
append some stext
```
$ echo "some text" >> first.txt 
$ git commit -m "second on master"
[master c0391db] second on master
 1 file changed, 3 insertions(+)
```
The two branches have a common anchestor. 
```
* 8b24e7c (HEAD, master) continue editing
| * 82d4d56 (hotfix) correction on hotfix
|/  
* 1f00a79 first
```
```
$ git merge hotfix
Auto-merging first.txt
Merge made by the 'recursive' strategy.
 first.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```
$ git branch -D hotfix
Deleted branch hotfix (was 0667956).
$ git log --oneline --decorate --graph --all
*   cdb63c9 (HEAD, master) Merge branch 'hotfix'
|\  
| * 0667956 hotfix
* | 34466e1 second
|/  
* 77e8c12 first
```
## Conflict
```
$ git checkout -b correction
Switched to a new branch 'correction'
$ vim first.txt
$ git add first.txt
$ git commit -m "corrected one line"
][correction 4dcce33] corrected one line
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```
$ git checkout master
Switched to branch 'master'
$ vim first.txt
$ git add first.txt
$ git commit -m "edited the same line"
[master dc119bc] edited the same line
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```
$ git merge correction
Auto-merging first.txt
CONFLICT (content): Merge conflict in first.txt
Automatic merge failed; fix conflicts and then commit the result.
```
```
che bello
scrivere cose
<<<<<<< HEAD
senza senso o forse si, sono convinto  che non ne abbia
=======
senza senso o forse si, ma in realta penso di no
>>>>>>> correction
aggiungiamo un test
aggiungiamone un altro
continuo a lavorare
```
```
$ git add first.txt 
Nicolas-MacBook-Air:fast_forward nicola$ git commit 
[master d32360c] Merge branch 'correction'
```
```
Merge branch 'correction'

# Conflicts:
#       first.txt
#
# It looks like you may be committing a merge.
# If this is not correct, please remove the file
#       .git/MERGE_HEAD
# and try again.


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# All conflicts fixed but you are still merging.
```
## Stash
```
git stash save "message"
git stash list
git stash apply stash@{0}
```