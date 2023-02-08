- once we reach lot of commits we can rebase it to a new start using this command
```bash
git rebase --root -i
```
and in the opened file for each commit except the first, change `pick` to `squash`. if u r using nano use `ctrl+\`  to find and replace all, further doubts --> [stack overflow](https://stackoverflow.com/questions/1657017/how-to-squash-all-git-commits-into-one)

- to display commits in a pretty manner
```bash
git log --pretty=oneline --abbrev-commit
```
