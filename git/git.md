git 安裝及使用
===========

# SSH

(1) 安裝 ssh

```
$ sudo apt-get install openssh-server openssh-client
```

(2) 製作 ssh key pair

```
alanjui@SRV01:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/alanjui/.ssh/id_rsa): /home/alanjui/.ssh/srv01_alanjui
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/alanjui/.ssh/srv01_alanjui.
Your public key has been saved in /home/alanjui/.ssh/srv01_alanjui.pub.
The key fingerprint is:
ed:68:21:96:7a:4d:e4:58:53:38:70:c2:ff:59:6d:97 alanjui@SRV01
The key's randomart image is:
+---[RSA 2048]----+
|     .o....      |
|      .oo.       |
|       .+.   .  .|
|       *.o  . oE.|
|      = S..o . . |
|     o + +o      |
|    . . + .      |
|     . .         |
|                 |
+-----------------+
alanjui@SRV01:~$
```

# git

## 建立個人識別
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.email "alanjui.1960@gamil.com"

alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.name "Alan Jui"
```

註：未建立個人識別，執行commit會遇見的錯誤狀況-
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "First commit"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'alanjui@SRV01.(none)')

```
## 建立 git 館並放入 GitHub

(1) 建立 README 檔案
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ echo "# Ubuntu 15.04" >> README.md
```

(2) 建立 git 館
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git init
Initialized empty Git repository in /home/alanjui/workspace/Ubuntu_1504/.git/
```

(3) 將所有待簽入的檔案，設定成 staged 狀態
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git add .
```

(4) 簽入 git 館
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "First commit"

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got
  'alanjui@SRV01.(none)')
```

上述指令執行失敗，因為尚未在 git 建立個人識別。

```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.email "alanjui.1960@gamil.com"

alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.name "Alan Jui"
```

建立個個識別後，再度簽入。
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "First commit"[master (root-commit) f6b8fec] First commit
 30 files changed, 2486 insertions(+)
 create mode 100755 .DS_Store
 create mode 100755 ._.DS_Store
 create mode 100755 Google Cloud/.DS_Store
 create mode 100755 Google Cloud/._.DS_Store
 create mode 100755 "Google Cloud/._Google Cloud Platform \350\250\230\344\272\213\346\234\254.md"
 create mode 100755 "Google Cloud/Google Cloud Platform \350\250\230\344\272\213\346\234\254.md"
 create mode 100755 Google Cloud/Styles.css
 create mode 100644 Google Cloud/_tmp_Ubuntu/ErrorMsg.md
 create mode 100644 "MongoDB/\345\256\211\350\243\235MongoDB.md"
 create mode 100644 Network/SSH.md
 create mode 100644 "Network/\345\246\202\344\275\225\346\211\213\345\213\225\345\256\211\350\243\235\347\266\262\350\267\257.md"
 create mode 100644 NodeJS/NodeJS.md
 create mode 100644 NodeJS/RVM_Ruby.md
 create mode 100644 README.md
 create mode 100755 Samba/.DS_Store
 create mode 100755 Samba/._.DS_Store
 create mode 100755 Samba/Samba.md
 create mode 100755 Samba/smb.conf
 create mode 100644 Samba/smb.conf.v0.1
 create mode 100755 Samba/smb.conf.v0.2a
 create mode 100644 Samba/smb.conf.v0.3
 create mode 100755 Styles.css
 create mode 100755 "Ubuntu  15.04 \344\270\255\346\226\207\345\255\227\351\253\224.odt"
 create mode 100755 Ubuntu_15.04.md
 create mode 100755 VirtualBox/My_VirbualBox_Note.md
 create mode 100644 VirtualBox/VirtualBox.xml.backup
 create mode 100644 VirtualBox/Win-Vista.vbox.backup
 create mode 100644 VirtualBox/Win10.vbox.backup
 create mode 100644 VirtualBox/Win7.vbox.backup
 create mode 100644 atom/styles.less.v0.1
```

(5) 置入遠端 git 館

執行置入指令：  __git push -u origin master__
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git push -u origin master
The authenticity of host 'github.com (192.30.252.129)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.252.129' (RSA) to the list of known hosts.
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

指令執行未成功，因個人的 Public ssh key 未在 GitHub 完成註冊

待完成註冊後，再執行指令。
```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git push -u origin master
Warning: Permanently added the RSA host key for IP address '192.30.252.131' to the list of known hosts.
Counting objects: 42, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (37/37), done.
Writing objects: 100% (42/42), 37.36 KiB | 0 bytes/s, done.
Total 42 (delta 9), reused 0 (delta 0)
To git@github.com:AlanJui/ubuntu_1504.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

## 加入 git

```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git push -u origin master
Warning: Permanently added the RSA host key for IP address '192.30.252.131' to the list of known hosts.
Counting objects: 42, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (37/37), done.
Writing objects: 100% (42/42), 37.36 KiB | 0 bytes/s, done.
Total 42 (delta 9), reused 0 (delta 0)
To git@github.com:AlanJui/ubuntu_1504.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git/

nothing added to commit but untracked files present (use "git add" to track)
```

```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git add .

alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "加入 git 安裝、設定及操作"[master 2393073] 加入 git 安裝、設定及操作
 1 file changed, 175 insertions(+)
 create mode 100644 git/git.md

alanjui@SRV01:~/workspace/Ubuntu_1504$ git push origin master
Warning: Permanently added the RSA host key for IP address '192.30.252.130' to the list of known hosts.
Counting objects: 4, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 2.39 KiB | 0 bytes/s, done.
Total 4 (delta 1), reused 0 (delta 0)
To git@github.com:AlanJui/ubuntu_1504.git
   02ed0a1..2393073  master -> master

alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```
