- If git pull or vs code is sync failed this may be a cause.
``` bash 
# Set pull strategy to merge for this repository
git config pull.rebase false
```
- Reset GitHub credential for HTTPS code push in windows 
	- Go to **Control Panel > User Accounts > Credential Manager**. 
  - Select **Windows Credentials**.
  - Look for entries under "Generic Credentials" related to `git:https://github.com` or `github.com`.![](assets/Pasted%20image%2020250720195812.png)
  - Expand them and click "Remove".
- If remote branch couldn't find it in VS code branch list, fetch the remote branch first and then checkout it
  - eg- if branch name is "asd" which doesn't appear in vs code first
	`git fetch origin asd`
	then 
	`git checkout asd`