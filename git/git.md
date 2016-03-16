# git 安裝及使用

## SSH 安裝及設定

1. 安裝 ssh

  ```
  $ sudo apt-get install openssh-server openssh-client
  ```

2. 製作 ssh 公私鑰對

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

## git 基本操作

### 建立個人識別

  ```
  alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.email "alanjui.1960@gamil.com"

  alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.name "Alan Jui"
  ```

  __註：未先建立個人識別，就直 接執行 commit 指令，將遭遇如下所示的錯誤狀況。__

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

### 首次納管

建立容器並存入遠端容器（GitHub）。

 1. 建立 README 檔案

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ echo "# Ubuntu 15.04" >> README.md
    ```

 2. 建立容器

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git init
    Initialized empty Git repository in /home/alanjui/workspace/Ubuntu_1504/.git/
    ```

 3. 將所有待簽入的檔案，設定成 staged 狀態

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git add .
    ```

 4. 簽入容器

    (1) 執行簽入指令： commit

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

    (2) 指令未能完成執行，是因為尚未在 git 建立個人識別。故以下列指令，先完成個人識別建立。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.email "alanjui.1960@gamil.com"

    alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.name "Alan Jui"
    ```

    (3) 完成個人識別建立後，再度簽入。

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

 5. 存入遠端容器

    (1) 執行置入指令：  __git push -u origin master__

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

    __註：指令執行未能成功，是因個人的 Public ssh key 未在 GitHub 完成註冊__

    (2) 待完成註冊後，再執行指令。

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

### 再次納管

添加新的檔案：或是檔案變更了內容後，再次納管到容器。

 1. 檢查容器中各檔案的納管狀態。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    	git/

    nothing added to commit but untracked files present (use "git add" to track)
    ```

 2. 將納管狀態為：「未追蹤（untracked）」的檔案，設成「已確認（committed）」狀態。、

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

## git 異常狀況處理

### 無法執行 push 指令，因為有別人先 push

 1. 執行 push 指令，卻發現執行結果異常。

    (1) 檢查納管狀態

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

    	modified:   NodeJS/RVM_Ruby.md
    	modified:   git/git.md

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

    	modified:   NodeJS/RVM_Ruby.md

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    	NodeJS/_imgs/
    	_imgs/
    ```

    (2) 將納管狀態為：「已變更（modified）」的檔案，設成「已確認（committed）」狀態。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git add NodeJS/RVM_Ruby.md _imgs/ NodeJS/_imgs/
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

    	modified:   NodeJS/RVM_Ruby.md
    	new file:   "NodeJS/_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    	new file:   "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    	modified:   git/git.md
    ```

    (3) 將納管狀態為：「已確認（committed）」的檔案，成立新版本。檔案的納管狀態，會被設成「已納管（staged）」狀態。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "加入Ruby安裝操作"
    [master 69b6df8] 加入Ruby安裝操作
     4 files changed, 80 insertions(+), 1 deletion(-)
     create mode 100644 "NodeJS/_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
     create mode 100644 "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    ```

    (4) 再次檢查容器中各檔案的納管狀態

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is ahead of 'origin/master' by 1 commit.
      (use "git push" to publish your local commits)
    nothing to commit, working directory clean
    ```

    (5) 執行 push 指令，將本端容器己納管的項目，存入遠端容器。結果，卻發生指令執行異常。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git push origin master
    To git@github.com:AlanJui/ubuntu_1504.git
     ! [rejected]        master -> master (fetch first)
    error: failed to push some refs to 'git@github.com:AlanJui/ubuntu_1504.git'
    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
    ```

 2. 執行 pull 指令，解決衝突問題。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git pull
    Warning: Permanently added the RSA host key for IP address '192.30.252.128' to the list of known hosts.
    remote: Counting objects: 7, done.
    remote: Compressing objects: 100% (4/4), done.
    remote: Total 7 (delta 4), reused 6 (delta 3), pack-reused 0
    Unpacking objects: 100% (7/7), done.
    From github.com:AlanJui/ubuntu_1504
       2393073..e2e5f08  master     -> origin/master
    Merge made by the 'recursive' strategy.
     Styles.css      | 337 +++++++++++++++++++++++++++++++++++++++++++++++++++++++-
     Ubuntu_15.04.md |  11 +-
     2 files changed, 343 insertions(+), 5 deletions(-)
    ```

    **註：在指令執行的過程中，會出现一個對話畫面，要求使用者說明為何要將「遠端容器」併入的理由。**

 3. 檢查容器中各檔案的納管狀態。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is ahead of 'origin/master' by 2 commits.
      (use "git push" to publish your local commits)
    nothing to commit, working directory clean
    ```

 4. 再次執行 push 指令。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git push origin master
    Counting objects: 10, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (9/9), done.
    Writing objects: 100% (10/10), 629.32 KiB | 0 bytes/s, done.
    Total 10 (delta 3), reused 0 (delta 0)
    To git@github.com:AlanJui/ubuntu_1504.git
       e2e5f08..cd521bb  master -> master
    ```

### 檢查遠端容器是否己有版本異動

 1. 使用指令進行檢查。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git fetch
    remote: Counting objects: 3, done.
    remote: Compressing objects: 100% (1/1), done.
    remote: Total 3 (delta 1), reused 3 (delta 1), pack-reused 0
    Unpacking objects: 100% (3/3), done.
    From github.com:AlanJui/ubuntu_1504
       305705d..da02040  master     -> origin/master
    ```

 2. 確認己有版本異動，使用指令與遠端容器進行同步。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git pull
    Updating 305705d..da02040
    Fast-forward
     .gitignore | 1 +
     1 file changed, 1 insertion(+)

  ```

    * 若是遠端容器沒有版本異動，檢查指令的執行結果會是一空白行，如下所示：

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git fetch
    ```

### 已納管的檔案改名

在 RVM_Ruby.md 檔案內放入圖片。圖片的檔案在先前己納管，後來因為覺得命名不妥，將檔案名稱變更成 RVM.png 。

 1. 檢查容器內各檔案納管狀態。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

    	modified:   NodeJS/RVM_Ruby.md
    	deleted:    "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    	modified:   git/git.md

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

    	_imgs/RVM.png

    no changes added to commit (use "git add" and/or "git commit -a")
    ```

 2. 將圖片新名稱的檔案，用 git add 指令，將檔案的納管狀態，設成「己追蹤」。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git add NodeJS/RVM_Ruby.md _imgs/RVM.png alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

    	modified:   NodeJS/RVM_Ruby.md
    	new file:   _imgs/RVM.png

    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

    	deleted:    "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    	modified:   git/git.md
    ```

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ ls _imgs/
    RVM.png  螢幕快照 2015-08-22 11:32:25.png
    ```

 3. 將圖片的舊檔案，以 git rm 指令，指定不再納管。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git rm  _imgs/螢幕快照\ 2015-08-22\ 11\:32\:25.png
    rm '_imgs/螢幕快照 2015-08-22 11:32:25.png'
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)

    	modified:   NodeJS/RVM_Ruby.md
    	new file:   _imgs/RVM.png
    	deleted:    "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

    	modified:   git/git.md
    ```

 4. 將變更檔案名稱的結果納管。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git commit -m "在 RVM 放入操作畫面圖片"
    [master d7436b2] 在 RVM 放入操作畫面圖片
     3 files changed, 1 insertion(+), 1 deletion(-)
     create mode 100644 _imgs/RVM.png
     delete mode 100644 "_imgs/\350\236\242\345\271\225\345\277\253\347\205\247 2015-08-22 11:32:25.png"
    ```

    __檢查資料夾，可發覺圖片的舊檔案已被刪除。__

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ ls _imgs/
    RVM.png

    alanjui@SRV01:~/workspace/Ubuntu_1504$ git status
    On branch master
    Your branch is ahead of 'origin/master' by 1 commit.
      (use "git push" to publish your local commits)
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

    	modified:   git/git.md

    no changes added to commit (use "git add" and/or "git commit -a")
    ```

 5. 將容器的己納管項目，存入遠端容器。

    ```
    alanjui@SRV01:~/workspace/Ubuntu_1504$ git push origin master
    Counting objects: 6, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (6/6), 180.81 KiB | 0 bytes/s, done.
    Total 6 (delta 2), reused 0 (delta 0)
    To git@github.com:AlanJui/ubuntu_1504.git
       da02040..d7436b2  master -> master
    ```
