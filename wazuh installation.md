## ubuntu guest addition:
```
sudo apt install open-vm-tools open-vm-tools-desktop -y
```
```
sudo reboot
```

## Wazuh installation:

```
apt install curl
```
```
apt install default-jdk -y
```
```
curl -sO https://packages.wazuh.com/4.8/wazuh-install.sh
```
```
bash wazuh-install.sh -a
```
Or add -o to overwrite
```
bash wazuh-install.sh -a -o
```
## Ubuntu start:
```
sudo systemctl status wazuh-dashboard
```
```
sudo systemctl start wazuh-dashboard
```
```
sudo systemctl status wazuh-indexer
```
```
sudo systemctl restart wazuh-indexer
```

## Windows 10 agent

```
Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.8.2-1.msi -OutFile ${env:tmp}\wazuh-agent.msi; msiexec.exe /i ${env:tmp}\wazuh-agent.msi /q WAZUH_MANAGER='192.168.0.106' WAZUH_AGENT_GROUP='default' WAZUH_AGENT_NAME='host-win10'
```
```
NET START WazuhSvc
```

## Linux Debian agent
```
wget https://packages.wazuh.com/4.x/apt/pool/main/w/wazuh-agent/wazuh-agent_4.8.2-1_amd64.deb && sudo WAZUH_MANAGER='192.168.0.106' WAZUH_AGENT_NAME='m2' dpkg -i ./wazuh-agent_4.8.2-1_amd64.deb
```
