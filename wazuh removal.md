# Wazuh Removal Precess from Ubuntu

To completely remove Wazuh from your system, you must uninstall its components and clean up associated files, logs, and configurations. Here's a step-by-step guide:
## 1. Stop Wazuh Services

Stop the Wazuh services to ensure they are not running during the uninstallation process.
```
sudo systemctl stop wazuh-manager
sudo systemctl stop wazuh-api
sudo systemctl stop filebeat
```
## 2. Uninstall Wazuh Components

Depending on your installation method, use the appropriate commands:
If Installed via Package Manager (e.g., DEB or RPM):

### On Ubuntu/Debian:
```
sudo apt remove --purge wazuh-manager wazuh-api wazuh-agent filebeat
sudo apt autoremove --purge
```

### On CentOS/Red Hat:

```
sudo yum remove wazuh-manager wazuh-api wazuh-agent filebeat
```

If Installed via Source or Custom Scripts:

Navigate to the Wazuh installation directory (default is `/var/ossec`) and remove it:
```
sudo rm -rf /var/ossec
```

## 3. Clean Configuration Files and Logs

Delete logs and configurations that may still be present:
```
sudo rm -rf /etc/wazuh*
sudo rm -rf /var/log/wazuh*
sudo rm -rf /etc/filebeat
sudo rm -rf /var/lib/filebeat
```

Check for any additional related files or services:
```
sudo find / -name "*wazuh*" -exec rm -rf {} \;
```

## 4. Remove Wazuh User (Optional)

If Wazuh created a user during installation, you can remove it:
```
sudo userdel -r wazuh
```

## 5. Check and Clean Firewall Rules (if configured)

If you modified your firewall for Wazuh, remove its rules:

Example (if using ufw):
```
sudo ufw delete allow 1514
sudo ufw delete allow 55000
```
Example (if using iptables):
```
sudo iptables -D INPUT -p tcp --dport 1514 -j ACCEPT
sudo iptables -D INPUT -p tcp --dport 55000 -j ACCEPT
```
## 6. Verify Removal

Ensure no Wazuh services or files remain:

Check running services:
```
sudo systemctl list-units --type=service | grep wazuh
```
Check for remaining files:
```
sudo find / -name "*wazuh*"
```

## 7. Restart the System (Optional)

Rebooting ensures all changes take effect:

```
sudo reboot
```
After completing these steps, Wazuh will be fully removed from your system.
