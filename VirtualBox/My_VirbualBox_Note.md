# 設定檔：
## Virtual Box App:

```
  ~/.config/VirtualBox/VirtualBox.xml
```

## Virtual Machine Setup:

```
  ~/VirtualBox VMs/Win-02/WIN-02.vbox
```

## Virtual Hard Disk Location:

```
  /media/alanjui/NAS01/VMs/Virtual-Box/Win-02
```

# 管理工具
  儘可能別直接編輯設定檔，而是改用 VBoxManager ，這個由 VirtualBox 提供的管理工具，進行 VirtualBox 的管理工偏。

  Use VBoxManage or the VirtualBox Manager GUI to make changes.

## 指令 clonehd

```
  VBoxManage clonehd /source/path/source.vdi /target/path/target.vdi

  $ vboxmanage clonehd Vista.vdi WIN02-HD1.vdi

  0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
  Clone medium created in format 'VDI'. UUID: 6ae16c6a-14ae-4520-b721-d66a6f0542ea
```

## 指令 closemedium
  使用 VBoxManage clonehd 指令欲複製虛擬硬碟，結果無法正常執行。

  這問題的導因係，虛碟硬碟的存放路徑，某層的「目錄」被「更名」。

  $ VBoxManage clonehd Vista.vdi Win02-HD1.vdi

  VBoxManage: error: Cannot register the hard disk '/media/alanjui/NAS01/VMs/Virtual-Box/Win-02/Vista.vdi' {d644a111-e1d4-4469-8ce8-8f1fdb232e99} because a hard disk '/media/alanjui/LAB1-HD2/VMs/Virtual-Box/Win-02/Vista.vdi' with UUID {d644a111-e1d4-4469-8ce8-8f1fdb232e99} already exists VBoxManage: error: Details: code NS_ERROR_INVALID_ARG (0x80070057), component VirtualBoxWrap, interface IVirtualBox, callee nsISupports VBoxManage: error: Context: "OpenMedium(Bstr(pszFilenameOrUuid).raw(), enmDevType, enmAccessMode, fForceNewUuidOnOpen, pMedium.asOutParam())" at line 177 of file VBoxManageDisk.cpp

vboxmanage closemedium disk d644a111-e1d4-4469-8ce8-8f1fdb232e99

## 指令 showvminfo

```
vboxmanage showvminfo Win7
```

# 參考
## Vista.vdi

```
  d644a111-e1d4-4469-8ce8-8f1fdb232e99
      /media/alanjui/LAB1-HD2/VMs/Virtual-Box/Win-02/Vista.vdi

  <HardDisk uuid="{04db9002-64e3-42c6-8f8e-5cfd8d8cf4ac}" location="/media/alanjui/NAS01/VMs/Virtual-Box/Win-02/WIN-02.vdi" format="VDI" type="Normal"/>

  <HardDisk uuid="{d644a111-e1d4-4469-8ce8-8f1fdb232e99}" location="/media/alanjui/NAS01/VMs/Virtual-Box/Win-02/Vista.vdi" format="VDI" type="Normal"/>
```

## closemedium disk 指令無法正常執行

```
$ vboxmanage closemedium disk 30535e65-a804-4cd7-8116-fea90a2102a4

VBoxManage: error: Medium '/media/alanjui/LAB1-HD2/VMs/Virtual-Box/Win7/Win7.vdi' cannot be closed because it is still attached to 1 virtual machines VBoxManage: error: Details: code VBOX_E_OBJECT_IN_USE (0x80bb000c), component MediumWrap, interface IMedium, callee nsISupports VBoxManage: error: Context: "Close()" at line 1551 of file VBoxManageDisk.cpp
```
