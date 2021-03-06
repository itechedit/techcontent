<properties
	pageTitle="使用 Resource Manager 和 PowerShell 管理 VM | Azure"
	description="使用 Azure Resource Manager 与 PowerShell 来管理虚拟机。"
	services="virtual-machines-windows"
	documentationCenter=""
	authors="davidmu1"
	manager="timlt"
	editor=""
	tags="azure-resource-manager"/>  


<tags
	ms.service="virtual-machines-windows"
	ms.workload="na"
	ms.tgt_pltfrm="vm-windows"
	ms.devlang="na"
	ms.topic="article"
	ms.date="09/27/2016"
	wacn.date="03/28/2017"
	ms.author="davidmu"/>  


# 使用 Resource Manager 与 PowerShell 来管理 Azure 虚拟机

## 安装 Azure PowerShell
 
有关安装最新版本的 Azure PowerShell、选择订阅和登录帐户的信息，请参阅[如何安装和配置 Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs)。

## 设置变量

本文中的所有命令都需要虚拟机所在资源组的名称以及要管理的虚拟机的名称。将 **$rgName** 的值替换为包含虚拟机的资源组的名称。将 **$vmName** 的值替换为 VM 的名称。创建变量。

    $rgName = "resource-group-name"
    $vmName = "VM-name"

## 显示有关虚拟机的信息

获取虚拟机信息。
  
    Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName

它会返回与此示例类似的内容：

    ResourceGroupName        : rg1
    Id                       : /subscriptions/{subscription-id}/resourceGroups/
                               rg1/providers/Microsoft.Compute/virtualMachines/vm1
    Name                     : vm1
    Type                     : Microsoft.Compute/virtualMachines
    Location                 : chinaeast
    Tags                     : {}
    AvailabilitySetReference : {
                                  "id": "/subscriptions/{subscription-id}/resourceGroups/
                                  rg1/providers/Microsoft.Compute/availabilitySets/av1"
                               }
    Extensions               : []
    HardwareProfile          : {
                                  "vmSize": "Standard_A0"
                               }
    InstanceView             : null
    NetworkProfile           : {
                                  "networkInterfaces": [
                                    {
                                      "properties.primary": null,
                                      "id": "/subscriptions/{subscription-id}/resourceGroups/
                                      rg1/providers/Microsoft.Network/networkInterfaces/nc1"
                                    }
                                  ]
                               }
    OSProfile                : {
                                  "computerName": "vm1",
                                  "adminUsername": "myaccount1",
                                  "adminPassword": null,
                                  "customData": null,
                                  "windowsConfiguration": {
                                    "provisionVMAgent": true,
                                    "enableAutomaticUpdates": true,
                                    "timeZone": null,
                                    "additionalUnattendContents": [],
                                    "winRM": null
                                  },
                                  "linuxConfiguration": null,
                                  "secrets": []
                               }
    Plan                     : null
    ProvisioningState        : Succeeded
    StorageProfile           : {
                                  "imageReference": {
                                    "publisher": "MicrosoftWindowsServer",
                                    "offer": "WindowsServer",
                                    "sku": "2012-R2-Datacenter",
                                    "version": "latest"
                                  },
                                  "osDisk": {
                                    "osType": "Windows",
                                    "encryptionSettings": null,
                                    "name": "osdisk",
                                    "vhd": {
                                      "Uri": "http://sa1.blob.core.chinacloudapi.cn/vhds/osdisk1.vhd"
                                    }
                                    "image": null,
                                    "caching": "ReadWrite",
                                    "createOption": "FromImage"
                                  }
                                  "dataDisks": [],
                               }
    DataDiskNames            : {}
    NetworkInterfaceIDs      : {/subscriptions/{subscription-id}/resourceGroups/
                                rg1/providers/Microsoft.Network/networkInterfaces/nc1}

## 停止虚拟机

停止正在运行的虚拟机。

    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName

系统会提示进行确认：

    Virtual machine stopping operation
    This cmdlet will stop the specified virtual machine. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
        
输入 **Y** 以停止虚拟机。

几分钟后，将返回类似于下面示例的内容：

    StatusCode : Succeeded
    StartTime  : 9/13/2016 12:11:57 PM
    EndTime    : 9/13/2016 12:14:40 PM

## 启动虚拟机

如果已停止，请启动虚拟机。

    Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName

几分钟后，将返回类似于下面示例的内容：

    StatusCode : Succeeded
    StartTime  : 9/13/2016 12:32:55 PM
    EndTime    : 9/13/2016 12:35:09 PM

如果想要重新启动已在运行虚拟机，请使用下文所述的 **Restart-AzureRmVM**。

## 重新启动虚拟机

重新启动正在运行的虚拟机。

    Restart-AzureRmVM -ResourceGroupName $rgName -Name $vmName

它会返回与此示例类似的内容：

    StatusCode : Succeeded
    StartTime  : 9/13/2016 12:54:40 PM
    EndTime    : 9/13/2016 12:55:54 PM

## 删除虚拟机

删除虚拟机。

    Remove-AzureRmVM -ResourceGroupName $rgName -Name $vmName

> [AZURE.NOTE] 可以使用 **-Force** 参数跳过确认提示。

如果没有使用 -Force 参数，系统会提示进行确认：

    Virtual machine removal operation
    This cmdlet will remove the specified virtual machine. Do you want to continue?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

它会返回与此示例类似的内容：

    RequestId  IsSuccessStatusCode  StatusCode  ReasonPhrase
    ---------  -------------------  ----------  ------------
                              True          OK  OK

## 更新虚拟机

本示例演示如何更新虚拟机的大小。
        
    $vmSize = "Standard_A1"
    $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    $vm.HardwareProfile.vmSize = $vmSize
    Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
    
它会返回与此示例类似的内容：

    RequestId  IsSuccessStatusCode  StatusCode  ReasonPhrase
    ---------  -------------------  ----------  ------------
                              True          OK  OK
                              
有关虚拟机的可用大小列表，请参阅 [Sizes for virtual machines in Azure](/documentation/articles/virtual-machines-windows-sizes/)（Azure 中的虚拟机大小）。

## 后续步骤

如果部署出现问题，请参阅[使用 Azure 门户预览排除资源组部署故障](/documentation/articles/resource-manager-deployment-operations/)

<!---HONumber=Mooncake_Quality_Review_1202_2016-->