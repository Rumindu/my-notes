1. `ctrl+alt+f12` will freeze the machine. `ctrl+alt+f2` will fix it.
2. `lsof -i :4000` - can see the process which run on port 4000
	- From above command result is empty but still saying the port is already allocated type `sudo lsof -i :4000`
``` bash 
# Force kill the processes
sudo kill -9 2680 2688 # 2680 and 2688 are process IDs and -9 for Force kill
```
1. Delete file or directory
	1. if it is file `rm file_name`
	2. if it is directory `rm -r dir_name`
	3. If the directory contains files or sub-directories `rm -rf dir_name`
2. Extension manager for top bar customization
3. Install the .deb file `sudo apt install ./your_package_name.deb`