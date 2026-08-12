
# VPN və RemoteAccess rolunu quraşdırmaq üçün stabil skript

Install-WindowsFeature RSAT-RemoteAccess-PowerShell, DirectAccess-VPN, Routing -IncludeManagementTools
Set-Service -Name RemoteAccess -StartupType Automatic
Start-Service -Name RemoteAccess
Install-RemoteAccess -VpnType Vpn

# VPN üçün zəruri portların açılması
New-NetFirewallRule -DisplayName "VPN-PPTP" -Direction Inbound -LocalPort 1723 -Protocol TCP -Action Allow
New-NetFirewallRule -DisplayName "VPN-L2TP" -Direction Inbound -LocalPort 500,4500 -Protocol UDP -Action Allow
