SSH

# Install

```
$ sudo apt-get install openssh-server openssh-client
```

# Setup

```
$ sudo gedit /etc/ssh/sshd_config
```

Setup:
```

# What ports, IPs and protocols we listen for
Port 22

# Authentication:
LoginGraceTime 120
PermitRootLogin no

# Users
AllowUsers user1 user2
```

# Restart service

```
$ sudo service ssh status
``

# Verify

```
$ ssh localhost
```



alanjui@SRV01:~$ ssh-keygen
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

alanjui@SRV01:~$ ls -l .ssh/id_rsa*
-rw------- 1 alanjui alanjui 1679  8月 22 01:48 .ssh/id_rsa
-rw-r--r-- 1 alanjui alanjui  395  8月 22 01:48 .ssh/id_rsa.pub
alanjui@SRV01:~$
