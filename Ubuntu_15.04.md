Ubuntu 15.04 安裝筆記
=====================

# 安裝 fcitx 中文輸入法

  1. 執行「語言支援」

  2. $ sudo apt-get install fcitx-table-cangjie5

  3. 登出，再登入

  3. 使用「文字輸入」，加入「倉頡、拚音」。

# 設定 Screen Shot

  1. Ubuntu Search / 螢幕擷圖

  2. 鎖定在啟動欄

# 設定工作區

  1. Ubuntu Search / 外觀（Appearance）

  2. 運作方式／啟用工作區：勾選

# 安裝 Chrome Web Browser  

  使用 .deb 檔案安裝

# 安裝 VisualStudio Code

  1. 解開壓縮檔到 ~/Applications

  2. 設定 link ，令 Terminal 也能啟動 code :
      ```
      $ sudo ln -s ~/Applications/VSCode-linux-x64/Code /usr/local/bin/code
      ```

# 設定 IP

  1. 設定「有線網路」使用靜態IP：192.168.99.10

  2. 登出再登入，以重新啟動 NIC

# 安裝 Samba

  1. 以指令安裝  
  ```
    $ sudo apt-get install samba
  ```

  2. 修改設定檔
  
     使用編輯器軟體，修改「設定檔」。
     
  ```
    $ sudo code /etc/samba/smbd.conf
  ```

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