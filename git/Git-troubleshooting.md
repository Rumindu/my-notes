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