# SSH 安裝與設定作業

## 安裝

    ```
    $ sudo apt-get install openssh-server openssh-client
    ```
## 設定

    ```
    $ sudo gedit /etc/ssh/sshd_config
    ```

    【設定內容】：

    ```
    ......
    ......
    ......

    # What ports, IPs and protocols we listen for
    Port 22

    # Authentication:
    LoginGraceTime 120
    PermitRootLogin no

    # Users
    AllowUsers user1 user2
    ```

## 重啟服務

    ```
    $ sudo service ssh status
    ```

## 驗證


    ```
    $ ssh localhost

    $ ssh-keygen

    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/alanjui/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /home/alanjui/.ssh/id_rsa.
    Your public key has been saved in /home/alanjui/.ssh/id_rsa.pub.
    The key fingerprint is:
    04:73:ed:f7:cf:40:dc:50:ed:38:75:6c:da:98:51:38 alanjui@SRV01
    The key's randomart image is:
    +---[RSA 2048]----+
    |      o ..     =+|
    |       +  .   E *|
    |        ..   . #.|
    |       .  . . O +|
    |        S  . o . |
    |              o  |
    |               + |
    |                o|
    |                 |
    +-----------------+

    $ ls -l .ssh/id_rsa*

    -rw------- 1 alanjui alanjui 1679  8月 22 01:48 .ssh/id_rsa
    -rw-r--r-- 1 alanjui alanjui  395  8月 22 01:48 .ssh/id_rsa.pub

    ```



## SSH 相關之目錄與檔案

### Server Site

Server Site 的設定檔：
/etc/ssh/sshd_config


### Client Site

  * Client Site 的設定檔

    ~/.ssh/config

  * 存放 ssh key 的目錄

    ~/.ssh

  * SSH Server 公鑰存放處

    ~/.ssh/known_hosts

## SSH Server 基本操作

  * 啟動
  ```
  sudo service ssh start
  ```

  * 檢查目前狀態
  ```
  sudo service ssh status
  ```

## SSH Client 端連線設定

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
