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

  1. 查第二台硬碟的UUID

  ```
  $ sudo blkid
  ```

  查 /dev/sdb 的 UUID

  2. 編輯設定檔 /etc/fstab

  ```
  $ sudo gedit /etc/fstab
  ```

  加入內容：
  ```
  # NAS01
  UUID=9279ede9-49f6-44fe-b481-261500f67675	/media		ext4    defaults		0		2
  ```

  3. 第一次手動掛載硬碟

  ```
  $ sudo mount /media
  ```

# 安裝 Samba

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
