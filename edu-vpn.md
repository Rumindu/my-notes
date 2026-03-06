# Make sure always tunnel apps through the VPN
![](assets/Pasted%20image%2020260306230723.png)
![](assets/Pasted%20image%2020260306230607.png)
![](assets/Pasted%20image%2020260306230813.png)
![](assets/Pasted%20image%2020260306231044.png)
- Uncheck Automatic metric and set Interface metric above 50. because VPN is usually get 5-25 value. so then it is always tunnelling through the VPN.
- Open PowerShell as Administrator and enter below command to confirmation.
``` bash 
Get-NetIPInterface | Sort-Object InterfaceMetric | Format-Table InterfaceAlias, InterfaceMetric, AddressFamily
```
![](assets/Screenshot%202026-03-06%20231811.png)
