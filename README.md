# PsHosts

.NET Library and Powershell Cmdlet Module that adds an API around modifying the hosts file on Windows. Supports tab completion for hostnames.

All destructive commands support `-whatif` and honor original formatting wherever possible.

![PsHosts in action](img/demo.gif?raw=true)

## Installation

Windows 10 users can simply install the module using the command below. For Windows 8.1 and below, [PsGet](http://psget.net/) can be used with the same command.

    PS C:\> Install-Module PsHosts

To install manually, download a release and unzip to $home\Documents\WindowsPowerShell\Modules\PsHosts

## Usage

The Cmdlets use the noun `HostEntry` and support the following verbs:

* Get
* Add
* Set
* Remove
* Enable
* Disable

General things to remember:

* **All destructive Cmdlets require admin elevation**
* The first parameter is always the hostname, which supports tab completion
* All Cmdlets support pipelining
* All destructive Cmdlets support `-whatif`

With that in mind, here are some samples:

```PowerShell
# List all entries
Get-HostEntry

# List matching entries
Get-HostEntry *.local
Get-HostEntry mysite.local

# Add an entry
Add-HostEntry mysite.local 127.0.0.1

# Change an entry's IP address
Set-HostEntry mysite.local 127.0.0.2

# Add a comment
Set-HostEntry mysite.local -Comment Excellent

# Rename a host
Get-HostEntry mysite.local | Set-HostEntry mysite2.local

# Disable (comment out) entries
Disable-HostEntry mysite.local

# Enable (uncomment) entries
Enable-HostEntry mysite.local

# Remove entries
Remove-HostEntry mysite.local

# Remove matching entries
Remove-HostEntry *.local

# Disable all loopback entries
Get-HostEntry | ?{$_.Address -eq "127.0.0.1"} | Disable-HostEntry
```
