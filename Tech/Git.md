- once we reach lot of commits we can rebase it to a new start using this command
```bash
git rebase --root -i
```
and in the opened file for each commit except the first, change `pick` to `squash`. if u r using nano use `ctrl+\`  to find and replace all, further doubts --> [stack overflow](https://stackoverflow.com/questions/1657017/how-to-squash-all-git-commits-into-one)

- to display commits in a pretty manner
```bash
git log --pretty=oneline --abbrev-commit
```

- we cant use ssh-git on company systems because ssh-agent service is disabled in services.msc, we cant enable it since no admin rights

> **Steps to generate ssh-git keys correctly

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
-- once done check ssh-agent service is on [further](https://unix.stackexchange.com/questions/464574/ssh-add-returns-with-error-connecting-to-agent-no-such-file-or-directory)
```powershell
#check
Get-Service | ?{$_.Name -like '*ssh-agent*'} | select -Property Name, StartType, Status

# if not ok start and set service to manual
Set-Service -Name ssh-agent -StartupType Manual

```
-- once everything is ok add ur keys to ssh-agent like
```bash
ssh-add <path to the key>
```
-- use this config for git (create a file named config in .ssh dir)
```config
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_ed25519
Port 443
```
