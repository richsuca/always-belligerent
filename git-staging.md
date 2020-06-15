## Use staging area
GIT's _staging_ area gives you a simple, convenient way to save changes but you can only undo to the last staged version

[Complete setup first](git-notes.md)

add text to a testfile
```
~/git_test$ echo "Apple" > testfile
```

stage it (save copy of file to staging area)
```
~/git_test$ git add testfile
```

overwrite the text
```
~/git_test$ echo "Orange" > testfile
~/git_test$ cat testfile
Orange
```

revert file to last staged (saved) version
```
~/git_test$ git checkout -- testfile
~/git_test$ cat testfile
Apple
```
