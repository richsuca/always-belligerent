# Use a branch, with full branch history

[Complete setup first](git-notes.md)

Steps  
1. Create branch
2. Make changes in branch
3. Sync changes to master

## Create branch
create branch
```
~/git_test$ git branch experiment
```

switch to branch
```
~/git_test$ git checkout experiment
Switched to branch 'experiment'
```

## Make changes in branch
make some change
```
~/git_test$ echo "Guava" >> testfile
```

stage & commit
```
~/git_test$ git add testfile
~/git_test$ git commit -m "added Guava"
[experiment 5be5e66] added Guava
 1 file changed, 1 insertion(+)
```

make more changes
```
~/git_test$ echo "Papaya" >> testfile
```

stage & commit
```
~/git_test$ git add testfile
~/git_test$ git commit -m "added Papaya"
[experiment b80104c] added Papaya
 1 file changed, 1 insertion(+)
```
 
see commit history
```
~/git_test$ git log
commit b80104cb8827519be383c297317ac9f901ad2b07 (HEAD -> experiment)
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:13:09 2020 -0400

    added Papaya

commit 5be5e6644009c5cf8f1697b0b11c806838693944
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:12:23 2020 -0400

    added Guava
```

## Sync changes to master
switch back to _master_ branch
```
~/git_test$ git checkout master
Switched to branch 'master'
```

merge the changes from _experiment_ branch to _master_
```
~/git_test$ git merge experiment
Updating 8d4a02f..b80104c
Fast-forward
 testfile | 2 ++
 1 file changed, 2 insertions(+)
```

verify file contents
```
~/git_test$ cat testfile
Banana
Kiwi
Dragon Fruit
Guava
Papaya
```

see commit log (note that it includes full branch commit history)
```
~/git_test$ git log
commit b80104cb8827519be383c297317ac9f901ad2b07 (HEAD -> master, experiment)
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:13:09 2020 -0400

    added Papaya

commit 5be5e6644009c5cf8f1697b0b11c806838693944
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:12:23 2020 -0400

    added Guava
```
