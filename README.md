---
description: 'Auteurs: Richard Chassot & Mehdi Karoui'
---

# Besoins techniques Pandora

### OS

<table>
  <thead>
    <tr>
      <th style="text-align:left">Software</th>
      <th style="text-align:left">Requirements</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Operating System</td>
      <td style="text-align:left">
        <ul>
          <li>Windows Server (2003 or higher)</li>
          <li>RedHat Enterprise (RHEL) 7.X</li>
          <li>CentOS 7.X (recommended)</li>
          <li>SLES 11 SP1 or higher</li>
          <li>OpenSUSE 11.X or higher</li>
          <li>Debian 5, 6, 7 or higher</li>
          <li>Ubuntu 11 or higher</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>FreeBSD 9.X and 10.X</li>
          <li>Solaris 10/OpenSolaris</li>
        </ul>
      </td>
      <td style="text-align:left">Pandora FMS does not give official support in these platforms</td>
    </tr>
  </tbody>
</table>

### Ports nécessaires

| Port | Protocol | Service/Process | Descripction | Address |
| :--- | :--- | :--- | :--- | :--- |
| 80 | TCP | Pandora FMS Console | IP management | Browser -&gt; Pandora FMS Console Server |
| 80 | TCP | Pandora FMS Console \(API Communication\) | Use of API/CLI feature | Browser/Server that starts the query -&gt; Pandora FMS Console Server |
| 80 | TCP | Metaconsole | Communication between Metaconsole and Nodes | Metaconsole server -&gt; Node Server Node Server -&gt; Metaconsole server |
| 162 | UDP | Pandora FMS Server | Trap reception | Trap generator device -&gt; Pandora FMS Server |
| 443 | TCP | Pandora FMS Console \(API Communication\) | Use of API/CLI feature | Browser/Server that starts the query -&gt; Pandora FMS Console Server |
| 443 | TCP | Metaconsole | Communication between Metaconsole and Nodes | Metaconsole server -&gt; Node server Node server -&gt; Metaconsole server |
| 3306 | TCP | Pandora FMS Console and Server | DB connection | Pandora FMS Console Server -&gt; Pandora FMS Database Server Pandora FMS Server -&gt; Pandora FMS Database Server |
| 3306 | TCP | Metaconsole | Communication between Metaconsole and DB Nodes | Metaconsole server -&gt; DB Nodes Server Node Server -&gt; Metaconsole BBDD Server |
| 4444 | TCP | Pandora FMS Server | Connection with Selenium GRID | Pandora FMS Server -&gt; Selenium Server |
| 9995 | UDP | Pandora FMS Server | Receiving Netflow probes | nfcapd Server -&gt; Pandora FMS Server |
| 10514 | TCP | Pandora FMS Console and Server | Log storage management with Logstash | Logstash Server -&gt; Pandora FMS Server |
| 41121 | TCP | Pandora FMS Agents | Tentacle Communication | Software Agent Server Agent -&gt; Pandora FMS Server |
| 80 | TCP | Pandora FMS Server | Web monitoring for WUX server | Pandora FMS Server -&gt; Server to monitor |
| 161 | UDP | Pandora FMS Console and Server | Monitoring via SNMP Polling | Pandora FMS Server -&gt; Server to monitor |
| 443 | TCP | Pandora FMS Server | Web monitoring for WUX server | Pandora FMS Server -&gt; Server to monitor |
| ICMP | ICMP | Console and Pandora FMS Server | Web monitoring for WUX server | Pandora FMS Server -&gt; Server to monitor |

### Dimensionnement du serveur

| Hardware | SMALL: up to 500 agents or 5000 modules | MEDIUM: up to 2000 agents or 10000 modules | BIG: For more than 4000 agents\* |
| :--- | :--- | :--- | :--- |
| CPU | 1 core at 2 GHz | 2 cores at 2,5 GHz | 4 cores at 3 GHz |
| RAM | 4 GB | 8 GB | 16 GB |
| Hard drive | 7200 rpm | 15K rpm or SSD | SSD |
| Disk Space | 20GB minimum 40GB recommended | 60GB minimum 120GB recommended | 120GB minimum 250GB recommended |

###  Services nécessaires à l'utilisation de Pandora

| Service | Utilité |
| :--- | :--- |
| MariaDB | Gestion de la BDD |
| PHP | Utilisation de l'interface web |
| Pandora\_console | Interface web de gestion du serveur de monitoring |
| Pandora\_server | Traitement des informations reçues par les agents collecteurs |



