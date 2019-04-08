# Quick create visual machine by powershell scripts

## Meet minimum requirements
- Kubernetes Master（1 Node）
- Kubernetes Minions（3 Nodes）
    - SQL Big Data Cluster - Master Node(1 Node)
    - SQL Big Data Cluster - Worker Node(2 Nodes)
> P.S. Each Node minimum resource: 1 CPU/Core; 12GB Memory; 32GB Disk

## Prepare resources
| ID | Name | URL | Remark |
| --- | --- | --- | --- |
| 1 | Windows 10 or Windows Server 2016 Later | [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/) | Provide Hyper-V |
| 2 | CentOS 7 | [CentOS Project](https://www.centos.org/) | Provide Node OS |

## PowerShell Sample Scripts
```powershell
# Defined Parameters
$VMName = "VMNodeName"
$ISOImage = "D:\ISO\CentOS-7-x86_64-DVD-1810.iso"
$VHDXPath = "E:\BDCVM\$VMName\$VMName.vhdx"
$VMPath = "E:\BDCVM\$VMName\"
$VMGeneration = 1
$BootDevice = "CD"
$ProcessorCount = 8
$MemorySize = 12GB
$VMVHDSize = 128GB
$CheckpointType = "Standard"
$AutomaticCheckpointsEnabled = 0
$SwitchName = "SwitchName"

# New a visual machine
New-VM -Name $VMName `
    -BootDevice $BootDevice `
    -Generation $VMGeneration `
    -NewVHDPath $VHDXPath `
    -NewVHDSizeBytes $VMVHDSize `
    -Path $VMPath `
    -SwitchName $SwitchName

# Setting visual machine parameters
Set-VM -Name $VMName `
    -ProcessorCount $ProcessorCount `
    -StaticMemory `
    -MemoryStartupBytes $MemorySize `
    -CheckpointType $CheckpointType `
    -AutomaticCheckpointsEnabled $AutomaticCheckpointsEnabled

# Mount OS Image
Set-VMDvdDrive -VMName $VMName `
    -ControllerNumber 1 `
    -ControllerLocation 0 `
    -Path $ISOImage
```
> ![](.\graphics\01.png)

