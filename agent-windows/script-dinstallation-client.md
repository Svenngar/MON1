# Script d'installation client Windows

Téléchargement du client :

```text
$source = "https://sourceforge.net/projects/pandora/files/Pandora%20FMS%207.0NG/745/Windows/Pandora%20FMS%20Windows%20Agent%20v7.0NG.745_x86_64.exe/download"
$destination = "C:\Users\Administrator\Downloads\Pandora FMS Windows Agent v7.0NG.745_x86_64.exe"
$fichier = New-Object System.Net.WebClient
$fichier.DownloadFile($source, $destination)
```

Installation silencieuse du client :

```text
$argument="/S --ip 192.168.66.10 --group Servers --alias WINCORE01"
start-process -FilePath $Destination -ArgumentList $argument
```

Script complet:

```text
$source = "https://sourceforge.net/projects/pandora/files/Pandora%20FMS%207.0NG/745/Windows/Pandora%20FMS%20Windows%20Agent%20v7.0NG.745_x86_64.exe/download"
$destination = "C:\Users\Administrator\Downloads\Pandora FMS Windows Agent v7.0NG.745_x86_64.exe"
$fichier = New-Object System.Net.WebClient
$fichier.DownloadFile($source, $destination)
$argument="/S --ip 192.168.66.10 --group Servers --alias WINCORE01"
start-process -FilePath $Destination -ArgumentList $argument
```

