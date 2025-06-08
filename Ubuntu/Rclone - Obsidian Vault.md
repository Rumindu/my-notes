# Rclone Google Drive Setup for Ubuntu

_Created: June 7, 2025_  
_Purpose: Access Obsidian vault stored in Google Drive from Ubuntu machine_

## Overview

This guide provides step-by-step instructions to mount Google Drive on Ubuntu using rclone, enabling simultaneous access to Obsidian vaults across Windows and Ubuntu machines.

## Prerequisites

- Ubuntu machine with internet connection
- Google account with Google Drive access
- Obsidian vault stored in Google Drive
- Terminal access with sudo privileges

## Step 1: Install Rclone

```bash
# Update package list
sudo apt update

# Install rclone
sudo apt install rclone

# Verify installation
rclone version
```

## Step 2: Configure Google Drive Connection

```bash
# Start rclone configuration
rclone config
```

### Interactive Configuration Steps:

1. **Create new remote**: Type `n` + Enter
2. **Name**: Enter `gdrive` (or preferred name)
3. **Storage type**: Type `drive` + Enter (for Google Drive)
4. **Client ID**: Press Enter (leave blank)
5. **Client Secret**: Press Enter (leave blank)
6. **Scope**: Type `1` (full access to all files)
7. **Root folder ID**: Press Enter (leave blank)
8. **Service account file**: Press Enter (leave blank)
9. **Advanced config**: Type `n` (No)
10. **Auto config**: Type `y` (Yes)
11. **Browser authentication**: Sign in and grant permissions
12. **Team drive**: Type `n` (No, unless using Google Workspace)
13. **Confirm**: Type `y` to confirm configuration
14. **Quit**: Type `q` to exit

## Step 3: Test Connection

```bash
# List files in Google Drive root
rclone ls gdrive:

# List directories only
rclone lsd gdrive:

# Check for Obsidian vault
rclone ls gdrive: | grep -i obsidian
```

## Step 4: Create Mount Points

```bash
# Create directory for mounting Google Drive
mkdir -p ~/GoogleDrive

# Optional: Create specific Obsidian vault directory
mkdir -p ~/ObsidianVault
```

## Step 5: Mount Google Drive

### Basic Mount Commands:

```bash
# Foreground mount (for testing)
rclone mount gdrive: ~/GoogleDrive --vfs-cache-mode writes

# Background mount (daemon mode)
rclone mount gdrive: ~/GoogleDrive --vfs-cache-mode writes --daemon

# Performance-optimized mount (recomended one)
rclone mount gdrive: ~/GoogleDrive --vfs-cache-mode full --vfs-cache-max-size 1G --daemon
```

## Step 6: Verify Mount

```bash
# Check if mount is working
ls ~/GoogleDrive

# Find Obsidian vault
find ~/GoogleDrive -name "*obsidian*" -type d
find ~/GoogleDrive -name "*.md" | head -5
```

## Step 7: Automation Scripts (No need if you are setting Auto-Mount on Startup)

### Create automatic Mount Script (`~/mount-gdrive.sh`)
``` bash 
#create mount script
nano ~/mount-gdrive.sh
```

```bash
#!/bin/bash

MOUNT_POINT="$HOME/GoogleDrive"
REMOTE_NAME="gdrive"

# Check if already mounted
if mountpoint -q "$MOUNT_POINT"; then
    echo "Google Drive already mounted at $MOUNT_POINT"
    exit 0
fi

# Create mount point if it doesn't exist
mkdir -p "$MOUNT_POINT"

# Mount Google Drive
echo "Mounting Google Drive..."
rclone mount "$REMOTE_NAME:" "$MOUNT_POINT" \
    --vfs-cache-mode writes \
    --vfs-cache-max-age 100h \
    --vfs-read-chunk-size 128M \
    --vfs-read-chunk-size-limit off \
    --daemon

# Wait for mount to complete
sleep 3

# Verify mount
if mountpoint -q "$MOUNT_POINT"; then
    echo "✅ Google Drive successfully mounted at $MOUNT_POINT"
    ls "$MOUNT_POINT" | head -5
else
    echo "❌ Failed to mount Google Drive"
    exit 1
fi
```

``` bash 
# Make the script executable
chmod +x ~/mount-gdrive.sh

# Run the executable scripts
./mount-gdrive.sh
```

### Create Unmount Script Script (`~/unmount-gdrive.sh`)

``` bash 
#create unmount script
nano ~/unmount-gdrive.sh
```

```bash
#!/bin/bash

MOUNT_POINT="$HOME/GoogleDrive"

# Check if mounted
if ! mountpoint -q "$MOUNT_POINT"; then
    echo "Google Drive is not mounted"
    exit 0
fi

# Unmount
echo "Unmounting Google Drive..."
fusermount -u "$MOUNT_POINT"

# Verify unmount
if ! mountpoint -q "$MOUNT_POINT"; then
    echo "✅ Google Drive successfully unmounted"
else
    echo "❌ Failed to unmount Google Drive"
    exit 1
fi
```

``` bash 
# Make the script executable
chmod +x ~/unmount-gdrive.sh

# Run the executable scripts
./unmount-gdrive.sh
```

#### Testing the Scripts

```bash
# Test mount script
# Run with full path from anywhere
~/mount-gdrive.sh

# Verify mount worked
ls ~/GoogleDrive
mount | grep GoogleDrive

# Test unmount script
# Run with full path from anywhere
~/unmount-gdrive.sh

# Verify unmount worked
mount | grep GoogleDrive
```

## Step 8: Auto-Mount on Startup

### Create Systemd Service:

```bash
sudo nano /etc/systemd/system/rclone-gdrive@.service
```

### Service Configuration:

```ini
[Unit]
Description=RClone Google Drive Mount for %i
After=network-online.target
Wants=network-online.target

[Service]
Type=notify
User=%i
Group=%i
ExecStartPre=/bin/mkdir -p /home/%i/GoogleDrive
ExecStart=/usr/bin/rclone mount gdrive: /home/%i/GoogleDrive --vfs-cache-mode full --vfs-cache-max-size 1G
ExecStop=/bin/fusermount -u /home/%i/GoogleDrive
Restart=always
RestartSec=10
Environment=PATH=/usr/local/bin:/usr/bin:/bin

[Install]
WantedBy=default.target
```

### Enable Service:

```bash
# After creating the service file, run these commands:

# Reload systemd configuration
sudo systemctl daemon-reload

# Enable auto-start at boot
sudo systemctl enable rclone-gdrive@$USER.service

# Start the service now
sudo systemctl start rclone-gdrive@$USER.service

# Check if it's working
sudo systemctl status rclone-gdrive@$USER.service
```

### Service Management Commands:

```bash
# Start the service
sudo systemctl start rclone-gdrive@$USER.service

# Stop the service
sudo systemctl stop rclone-gdrive@$USER.service

# Restart the service
sudo systemctl restart rclone-gdrive@$USER.service

# Enable auto-start at boot
sudo systemctl enable rclone-gdrive@$USER.service

# Disable auto-start at boot
sudo systemctl disable rclone-gdrive@$USER.service

# Check service status
sudo systemctl status rclone-gdrive@$USER.service

# View recent logs
journalctl -u rclone-gdrive@$USER.service --no-pager -n 20

# Follow logs in real-time
journalctl -u rclone-gdrive@$USER.service -f
```

## Step 9: Install Obsidian on Ubuntu

```bash
# Download Obsidian AppImage
wget https://github.com/obsidianmd/obsidian-releases/releases/latest/download/Obsidian-1.4.16.AppImage

# Make executable
chmod +x Obsidian-*.AppImage

# Move to system location
sudo mv Obsidian-*.AppImage /usr/local/bin/obsidian

# Launch Obsidian
obsidian
```

### Create Desktop Entry:

```bash
nano ~/.local/share/applications/obsidian.desktop
```

```ini
[Desktop Entry]
Name=Obsidian
Exec=/usr/local/bin/obsidian
Icon=obsidian
Type=Application
Categories=Office;
```

## Step 10: Configure Obsidian Vault

1. **Launch Obsidian**
2. **Click "Open folder as vault"**
3. **Navigate to**: `~/GoogleDrive/YourObsidianVaultFolder`
4. **Select your vault folder**

## Troubleshooting

### Common Commands:

```bash
# Check if rclone is running
ps aux | grep rclone

# Check mount status
mount | grep rclone

# View service logs
journalctl -u rclone-gdrive@$USER.service -f

# Manual mount with verbose output
rclone mount gdrive: ~/GoogleDrive --vfs-cache-mode writes -v

# Force unmount
sudo umount -f ~/GoogleDrive
# or
fusermount -u ~/GoogleDrive
```

### Performance Issues:

- Increase cache size: `--vfs-cache-max-size 2G`
- Use full cache mode: `--vfs-cache-mode full`
- Adjust chunk size: `--vfs-read-chunk-size 32M`

## Performance Optimization

### High-Performance Mount Command:

```bash
rclone mount gdrive: ~/GoogleDrive \
    --vfs-cache-mode full \
    --vfs-cache-max-size 2G \
    --vfs-cache-max-age 1h \
    --vfs-read-chunk-size 32M \
    --buffer-size 32M \
    --daemon
```

## Security Considerations

- **Authentication**: Uses OAuth 2.0 for secure Google account access
- **Permissions**: Rclone only requests necessary Google Drive permissions
- **Local Access**: Mounted files have standard Linux file permissions
- **Network**: All transfers use HTTPS encryption

## Useful Commands

### Daily Operations:

```bash
# Mount Google Drive
~/mount-gdrive.sh

# Unmount Google Drive
~/unmount-gdrive.sh

# Check mount status
mountpoint ~/GoogleDrive

# Sync vault manually (if needed)
# This is uni direction sync. Only applied changes of Google drive to local setup backup
rclone sync ~/GoogleDrive/ObsidianVault ~/local-backup/ObsidianVault
```

## References

- **Rclone Official Documentation**: [https://rclone.org/](https://rclone.org/)
- **Google Drive Backend**: [https://rclone.org/drive/](https://rclone.org/drive/)
- **Mount Command Reference**: [https://rclone.org/commands/rclone_mount/](https://rclone.org/commands/rclone_mount/)
- **VFS Caching Guide**: [https://rclone.org/commands/rclone_mount/#vfs-file-caching](https://rclone.org/commands/rclone_mount/#vfs-file-caching)
- **Obsidian Linux Installation**: [https://help.obsidian.md/Getting+started/Download+and+install+Obsidian#Linux](https://help.obsidian.md/Getting+started/Download+and+install+Obsidian#Linux)

## Notes

- **Backup Important**: Always backup your vault before making changes
- **Internet Required**: Google Drive mount requires internet connection
- **Sync Conflicts**: Be careful when editing same files simultaneously on different machines
- **Performance**: Large vaults may benefit from local caching
- **Updates**: Check for Obsidian and rclone updates periodically

---

_Last Updated: June 7, 2025_  
_Status: Active Configuration_  
_Next Review: Monthly_
