SSH 安裝與設定
============

# 與 SSH 相關之目錄與檔案

## Server Site

Server Site 的設定檔：
/etc/ssh/sshd_config


## Client Site

  * Client Site 的設定檔

    ~/.ssh/config

  * 存放 ssh key 的目錄

    ~/.ssh

  * SSH Server 公鑰存放處

    ~/.ssh/known_hosts

# SSH Server 基本操作

  * 啟動
  ```
  sudo service ssh start
  ```

  * 檢查目前狀態
  ```
  sudo service ssh status
  ```

# Client 端連線設定

將 Cleint 端送交的「公鑰檔案」（.pub）以「添加」作法，放入 ~/.ssh/authorized_keys 檔案中。

示範：

1. 在 Client 端電腦，使用「終端機」執行下列指令，將公鑰放到 SSH Server 端的 home 目錄中：
  ```
  MAC2012:~ AlanJui$ cd ~/.ssh
  MAC2012:.ssh AlanJui$ scp id_rsa_JuZhengZhong.pub alanjui@192.168.99.10
  ```

2. 在 SSH Server 端電腦，使用「終端機」執行下列指令，將 Client 端的公鑰檔，添加到 authorized_keys 檔案中：
  ```
  alanjui@SRV01:~$ cd ~/.ssh
  alanjui@SRV01:~/.ssh$ cat ../id_rsa_JuZhengZhong.pub >> authorized_keys
  ```

3. 在 Client 端電腦，使用「終端機」執行下列指令，驗證已能連上 SSH Server

  ```
  MAC2012:~ AlanJui$ ssh juzhengzhong@192.168.99.10
  juzhengzhong@192.168.99.10's password:
  Welcome to Ubuntu 15.04 (GNU/Linux 3.19.0-26-generic x86_64)

   * Documentation:  https://help.ubuntu.com/

  Last login: Mon Aug 24 11:36:54 2015 from 192.168.99.110
  juzhengzhong@SRV01:~$ exit
  logout
  Connection to 192.168.99.10 closed.
  MAC2012:~ AlanJui$
  ```
