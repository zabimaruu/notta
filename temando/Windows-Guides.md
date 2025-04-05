
# Windows Guides

## SSH Server

1 - Install *OpenSSH*
	Using *Scoop* `scoop bucket add main` && `scoop install main/openssh`
	Using *Winget* `winget install -e --id Microsoft.OpenSSH.Beta`
	Using *Choco* `choco install openssh --pre `
2 - Add *Windows Firewall Rule* to accept incoming *SSH connection on port 22*
	Navigate to *Control Panel > Windows Defender Firewall > Advance Settings > Inbound Rules > New Rule*
	Creating rule
		*Rule type: **Port***
		*Protocol and Ports: **TCP | Port 22***
		*Action: **Allow the connection***
		*Name: **Name_It***
3 - Check status of *ssh-agent*
	`Get-Service -Name *ssh*`
	It will be most likely disabled
4 - Start service at startup/boot 
	*Note: Start **Terminal/Powershell as Administrator***
	Check service status `Get-Service -Name *ssh*`
	Start *sshd*
		`Start-Service sshd`
		`Set-Service -Name sshd -StartupType 'Automatic'`
	Start *ssh-agent*
		`Start-Service -Name 'ssh-agent'`
		`Set-Service -Name 'ssh-agent' -StartupType 'Automatic'`
	