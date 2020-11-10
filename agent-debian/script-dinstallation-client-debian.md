# Script d'installation client Debian

```bash
wget https://sourceforge.net/projects/pandora/files/Pandora%20FMS%207.0NG/745/Debian_Ubuntu/pandorafms.agent_unix_7.0NG.745.deb/download
dpkg -i download

echo "agent_alias     DEBIAN9" >> /etc/pandora/pandora_agent.conf
sed -i 's/^server_ip\s*localhost.*/server_ip   192.168.66.10/g' /etc/pandora/pandora_agent.conf
sed -i 's/^#group.*/group  Servers/g' /etc/pandora/pandora_agent.conf
apt install libyaml-tiny-perl
service pandora_agent_daemon restart
```



