$env:Path="$env:Path;C:\Program Files\OpenSSH\" #or specific SSH directory if installed elsewhere

Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SessionManager\Environment' -Name PATH -Value $env:Path

enable-sshremoting


Microsoft and the PowerShell team provide excellent documentation on setting up remoting via SSH. These
are the basic steps:

Install PowerShell Core

https://github.com/PowerShell/PowerShell/releases

As of Windows 10 version 1809 and Windows Server 2019, OpenSSH is an optional feature that can
be installed directly from within Windows. Per the Microsoft documentation, "To install OpenSSH,
start Settings then go to Apps > Apps and Features > Manage Optional Features." Older versions of Windows can install via https://github.com/PowerShell/Win32-OpenSSH/releases
Configure PATH so that PowerShell can find SSH binaries

Configure SSHD to use the PowerShell binary as a subsystem
	Add the following line to the configuration of sshd_config file in $env:ProgramData\ssh
	Subsystem powershell <path_to_pwsh.exe> -sshs -NoLogo -NoProfile
	Within this file, enable PubKeyAuthentication if key-based authentication is preferred
	PubkeyAuthentication yes

Restart the SSHD service
$env:Path="$env:Path;C:\Program Files\OpenSSH\" #or specific SSH directory

if installed elsewhere
Set-ItemProperty -Path 'Registry::HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\SessionManager\Environment' -Name PATH -Value $env:Path

Restart-Service sshd
