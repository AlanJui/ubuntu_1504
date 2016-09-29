Ubuntu 15.04 安裝筆記
=====================

# 設定 IP

  1. 設定「有線網路」使用靜態IP
      - IP: 192.168.66.10/24
      - Default Gateway: 192.168.66.1

  2. 登出再登入，以重新啟動 NIC


# 安裝常用系統工具

  × wget
  × git
  * tree

  ```
  ＄ sudo apt-get install wget git-core
  ```

# 安裝 fcitx 中文輸入法

  1. 執行「語言支援」

  2. 執行安裝指令

  ```
  $ sudo apt-get install fcitx-table-cangjie5

  $ sudo apt-get install fcitx-googlepinyin
  ```

  3. 登出，再登入

  4. 使用「文字輸入」設定：加入「倉頡、Google拚音」輸入法。

# 設定 Screen Shot

  1. Ubuntu Search / 螢幕擷圖

  2. 鎖定在啟動欄

# 啟用「工作區」

  1. Ubuntu Search / 外觀（Appearance）

  2. 運作方式／啟用工作區：勾選

# 安裝常用文字編輯器（Editor）

  × atom
  × Sublime Text 3
  × Visual Studio

## 安裝 Visual Studio Code

  1. 解開壓縮檔到 ~/Applications

  2. 設定 link ，令 Terminal 也能啟動 code :
      ```
      $ sudo ln -s ~/Applications/VSCode-linux-x64/Code /usr/local/bin/code
      ```

# 安裝Oh-my-zsh


# 安裝 Chrome Web Browser  

  使用 .deb 檔案安裝

# 自動掛載第二台硬碟

 - 第一顆硬碟（500GB)： /dev/sda
 - 第二顆硬碟（2TB)： /dev/sdb

 1. 驗證上述兩顆硬碟皆存在：
 
```
    $ ls /dev/sd*
```

 2. 驗證第二顆硬碟的容量
 
```
    $ sudo fdisk -l /dev/sdb
```

 3. 查第二顆硬碟的UUID

    查 /dev/sdb 的 UUID

```
  $ sudo blkid
```

 4. 編輯設定檔 /etc/fstab

```
  $ sudo gedit /etc/fstab
```

    加入內容：
 ```
 # External Disk
 UUID=9279ede9-49f6-44fe-b481-261500f67675	/NAS1   ext4    defaults		0		2
 ```
  
    完整的設定內容：
```
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/sda3 during installation
UUID=328f484d-11f6-4135-ba2b-0ad26916dfd8 /               ext4    errors=remount-ro 0       1
# /boot was on /dev/sda1 during installation
UUID=d949a31c-0426-486d-a8a4-53a8d825ed5c /boot           ext4    defaults        0       2
# /home was on /dev/sda4 during installation
UUID=fb7971a1-2fb7-48d9-8131-05cd840c9143 /home           ext4    defaults        0       2
# swap was on /dev/sda5 during installation
UUID=9d5873a4-fa56-4a3b-bf3c-9b769e266097 none            swap    sw              0       0
# External Disk
UUID=9279ede9-49f6-44fe-b481-261500f67675 /NAS1           ext4	  defaults	  0       2
 ```

 5. 設定掛載點
 
    設定第二顆硬碟，掛載於目錄路徑： /NAS1。
 
 ```
  $ sudo mkdir /NAS1
 ```   

 6. 第一次手動掛載硬碟

```
  $ sudo mount /NAS1
```

    或

```
  $ sudo mount -a
```

 7. 驗證已成功掛載
 
```
  $ sudo df -h
```

```
alanjui@Srv-01:/NAS1$ df -h
檔案系統        容量  已用  可用 已用% 掛載點
udev            7.8G     0  7.8G    0% /dev
tmpfs           1.6G  9.8M  1.6G    1% /run
/dev/sda3        47G  4.6G   40G   11% /
tmpfs           7.8G   61M  7.8G    1% /dev/shm
tmpfs           5.0M  4.0K  5.0M    1% /run/lock
tmpfs           7.8G     0  7.8G    0% /sys/fs/cgroup
/dev/sdb1       1.8T  841G  901G   49% /NAS1
/dev/sda1       945M   55M  825M    7% /boot
/dev/sda4       388G  1.1G  368G    1% /home
tmpfs           1.6G  116K  1.6G    1% /run/user/1000
tmpfs           1.6G  4.0K  1.6G    1% /run/user/108


alanjui@Srv-01:/NAS1$ sudo blkid
/dev/sda1: UUID="d949a31c-0426-486d-a8a4-53a8d825ed5c" TYPE="ext4" PARTUUID="7b5d65b9-01"
/dev/sda3: UUID="328f484d-11f6-4135-ba2b-0ad26916dfd8" TYPE="ext4" PARTUUID="7b5d65b9-03"
/dev/sda4: UUID="fb7971a1-2fb7-48d9-8131-05cd840c9143" TYPE="ext4" PARTUUID="7b5d65b9-04"
/dev/sda5: UUID="9d5873a4-fa56-4a3b-bf3c-9b769e266097" TYPE="swap" PARTUUID="7b5d65b9-05"
/dev/sdb1: LABEL="NAS" UUID="9279ede9-49f6-44fe-b481-261500f67675" TYPE="ext4" PARTUUID="3c9b9d09-01"

```


# 安裝 Samba

https://github.com/AlanJui/ubuntu_1504/blob/master/Samba/Samba.md

# 安裝文泉驛正黑體

剛安裝完 Ubuntu 15.04 時，印象中系統有內附中文字型：「文泉驛正黑」。但不知為何後來竟不見了，系統內附的中文字型只有：細明、楷書；卻沒有我個人喜歡的「黑體」（不知是否因為套件版本更新，被去掉了）。
  ＊細明體： AR PL UMing TW
  ＊楷書體： AR PL UKai TW

遇到上述的問題時，可在「終端機」透過以下的指令，將「文泉驛正黑」中文字型，再安裝到作業系統中。

```
  $ sudo apt-get install ttf-wqy-zenhei

  $ sudo fc-cache -v
```

【註】：在 Ubuntu 內附的「字型檢視程式」中，「文泉驛正黑」中文字型的「字型名稱」為：WenQuanYi Zen Hei 。﻿
