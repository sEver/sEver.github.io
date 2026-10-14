# Running native VMs on Windows with Sandbox and Hyper-V

## Sandbox

This is the instant, fast, very light virtual system that uses parts of the host system to build its system image. 
It's always run from a fresh, clean state, with no permanence whatsoever. You can configure it to have shared directories 
with the host system, and to run certain commands (installing your tools) upon start. 

See [documentation for sandbox](https://learn.microsoft.com/en-us/windows/security/application-security/application-isolation/windows-sandbox/windows-sandbox-configure-using-wsb-file)

## Hyper-V 

This is a Windows-Native virtualization layer, that allows you to run multiple virtual machines with their own persistent 
virtual hard drives, and have them running in the background, even if you're not "connected" to them.

With `Quick Create` you can create a Win 10 or Win 11 machine from a Windows image that will be auto-downloaded.
Supposedly these systems are evaluation versions and should stop working after 90 days. Will see. 

By default Hyper-V manager installs the machines on C drive, you might want to change that in options. 
Hyper-V Manager => right panel => Hyper-V Settings => Virtual Machines and Virtual Hard Disks. 

You can also enable `Nested Virtualization` to allow the guest systems to run WSL - Windows Linux Subsystem.
This is done by `Powershell` commands in the host system:
```
PS D:\> Set-VMProcessor -VMName YOUR_VM_NAME -ExposeVirtualizationExtensions $true
```
Spoofing of MAC addresses on the virtual switch is also needed:
```
PS D:\> Get-VMNetworkAdapter -VMName YOUR_VM_NAME | Set-VMNetworkAdapter -MacAddressSpoofing On
```
See [documentation for nested virtualization](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/enable-nested-virtualization)
