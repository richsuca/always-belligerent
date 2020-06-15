# Use a branch, without branch history
This is similar to [Use a branch, with full branch history](git-branch.md), the only difference is during sync from _experiment_ to _master_, we don't copy over _commit history_. We create one comment for the entire change.

## Make changes in branch, and commit
```
~/git_test$ git checkout experiment
Switched to branch 'experiment'

~/git_test$ echo "Mango" >> testfile
~/git_test$ git add testfile
~/git_test$ git commit -m "added Mango"
[experiment cb19233] added Mango
 1 file changed, 1 insertion(+)

~/git_test$ echo "Grapes" >> testfile
~/git_test$ git add testfile
~/git_test$ git commit -m "added Grapes"
[experiment b376551] added Grapes
 1 file changed, 1 insertion(+)

~/git_test$ git log
commit b376551cf08b5495a97f240c0b0d9458f34e577c (HEAD -> experiment)
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:15:53 2020 -0400

    added Grapes

commit cb1923307183601654b7ff4ae2f76e947484f200
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:15:19 2020 -0400

    added Mango

commit b80104cb8827519be383c297317ac9f901ad2b07 (master)
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

use _--squash_ to merge changes but don't commmit
```
~/git_test$ git merge --squash experiment
Updating b80104c..b376551
Fast-forward
Squash commit -- not updating HEAD
 testfile | 2 ++
 1 file changed, 2 insertions(+)
``` 

check status of file after merge
```
~/git_test$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   testfile
```

verify contents
```
~/git_test$ cat testfile
Banana
Kiwi
Dragon Fruit
Guava
Papaya
Mango
Grapes
```

commit the merge
```
~/git_test$ git commit -m "Added Mango, Grapes"
[master 7091669] Added Mango, Grapes
 1 file changed, 2 insertions(+)
``` 

check commit history, you will just see one commit for the merge
```
~/git_test$ git log
commit 7091669240071e15fe123cf8c521087c447ccb79 (HEAD -> master)
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:17:55 2020 -0400

    Added Mango, Grapes

commit b80104cb8827519be383c297317ac9f901ad2b07
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:13:09 2020 -0400

    added Papaya

commit 5be5e6644009c5cf8f1697b0b11c806838693944
Author: richsu <richard.hsu@gmail.com>
Date:   Mon Jun 15 11:12:23 2020 -0400

    added Guava
```
