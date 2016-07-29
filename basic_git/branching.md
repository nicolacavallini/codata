# Branching
Move on from the previus example and create a little bit of history.
```
$ echo "some modification" >> first.txt 
mac-venier:git_ex_0 nicola$ git commit -a -m "second commit"
[master 402aff8] second commit
 1 file changed, 1 insertion(+)
```
Notice we used `git commit -a -m "second commit"`. `-a` adds the modifications in the working directory directly to the staging area.
```
$ echo "a little bit of history repeating" >> first.txt 
mac-venier:git_ex_0 nicola$ git commit -a -m "third commit"
[master e82e559] third commit
 1 file changed, 1 insertion(+)
```
Explore the history we created with `git log`, or better with:
 ```
$ git log --oneline --decorate --all --graph
* e82e559 (HEAD, master) third commit
* 402aff8 second commit
* f8e26ec first commit
 ```
Notiche that the `HEAD` points to `master`. Create a new branch.
```
$ git branch test
$ git branch
* master
  test
 ```
 `HEAD` the current reference is still on master. The command to move in between branches is `git cehckout`. It moves the head and updates the files accordingly.
 ```
$ git checkout test
Switched to branch 'test'
$ git branch
  master
* test
```
Create some history in both test and master, then log it.
```
$ vim first.txt 
$ git commit -a -m "first commit on test"
[test a276498] first commit on test
 1 file changed, 2 insertions(+), 1 deletion(-)
$ git checkout master
Switched to branch 'master'
$ vim first.txt 
$ git commit -a -m "fourth commit"
[master 6088a8d] fourth commit
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git log --oneline --decorate --all --graph
* 6088a8d        (HEAD, master) fourth commit
| * a276498      (test) first commit on test
|/  
* e82e559        third commit
* 402aff8        second commit
* f8e26ec        first commit
$ git checkout test
Switched to branch 'test'
$ git log --oneline --decorate --all --graph
* 6088a8d        (master) fourth commit
| * a276498      (HEAD, test) first commit on test
|/  
* e82e559        third commit
* 402aff8        second commit
* f8e26ec        first commit
```