
1. taskmanager asking admin privilage
```
sfc /scannow
```
if it doesn't help use this [link](https://www.thewindowsclub.com/catroot-catroot2-folder-reset-windows)
```
net stop cryptsvc

md %systemroot%\system32\catroot2.old

xcopy %systemroot%\system32\catroot2 %systemroot%\system32\catroot2.old /s

//Next, delete all the contents of the catroot2 folder.

net start cryptsvc
```

2. 