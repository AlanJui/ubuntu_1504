# 安裝 Samba

  1. 安裝套件

  ```
  $ sudo apt-get install -y samba samba-common python-glade2 system-config-samba
  ```

  2. 進行設定

  ```
  $ sudo cp -pf /etc/samba/smb.conf /etc/samba/smb.conf.bak

  $ sudo gedit /etc/samba/smb.conf
  ```

  3. 新增使用者

  ```
  $ sudo smbpasswd -a alanjui

  [sudo] password for alanjui:
  New SMB password:
  Retype new SMB password:
  Added user alanjui.


  $ sudo smbpasswd -e alanjui

  Enabled user alanjui.
  alanjui@SRV01:~$
  ```

  4. 重新啟動Samba Service

  ```
  $ sudo service smbd restart
  $ sudo service smbd status
  ```
