# MongoDB 安裝及設定作業

## 安裝 MongoDB 套件

`特別注意`：MongoDB 官網特別聲明，對於 Ubuntu 這個平台，僅只支援 LTS 版本。

所以，下述的操作方法係 Ubuntu 15.04, 15.10 專用的安裝用法。

參考指引： [Install MongoDB From Tarball ](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-linux/)


 1. 下載 BIN 檔案。

    ```
    $ cd ~/_tmp

    $ curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.2.1.tgz
    ```

 2. 解壓縮。

    ```
    $ tar -zxvf mongodb-linux-x86_64-2.6.11.tgz
    ```

 3. 將完成解壓縮的目錄，搬到欲安裝的路徑下。

    ```
    $ mkdir -p ~/Applications/MongoDB

    $ cp -R -n mongodb-linux-x86_64-2.6.11/* ~/Applications/MongoDB
    ```

 4. 設定環境變數PATH

    使用 ZSH Shell：

    ```
    $ gedit ~/.zshrc
    ```

    使用 Bash Shell：

    ```
    $ gedit ~/.bashrc
    ```

    設定內容：

    ```
    # MongoDB
    export PATH=/home/alanjui/Applications/MongoDB/bin:$PATH

    ```

 5. 重啟環境設定

    令環境變數 PATH 立即生效，無需重啟「終端機」。

    ```
    $ source ~/.zshrc

    $ echo $PATH
    ```

 6. 建立資料庫目錄（Data Directory）。

    ```
    $ sudo mkdir -p /data/db
    ```

    【註】：

    存放資料庫的「目錄路徑」，若未先建立，就直接啟動 mongod ，將致如下的「異常狀況」發生：

    ```
    $ mongod

    2015-08-21T18:16:15.455+0800 I STORAGE  [initandlisten] exception in initAndListen: 29 Data directory /data/db not found., terminating
    2015-08-21T18:16:15.455+0800 I CONTROL  [initandlisten] dbexit:  rc: 100
    ```

 7. 設定 MongoDB 設定檔

    ```
    $ sudo gedit /etc/mongod.conf
    ```

    設定 `dbPath` 為： /data/db （原先設定為： `/var/lib/mongodb` ）

    ```
    storage:
     dbPath: /data/db

    ```

 8. 設定資料庫目錄的使用權限。

    (1) 歡察目錄的「擁有者」及「權限」設定：

    ```
    $ ls -al /data/
    總計 12
    drwxr-xr-x  3 root root 4096  8月 21 18:21 .
    drwxr-xr-x 25 root root 4096  8月 21 18:21 ..
    drwxr-xr-x  2 root root 4096  8月 21 18:21 db
    ```

    (2) 變更目錄的「擁有者」：

    ```
    $ sudo chown -R `id -u` /data/db

    $ ls -l /data

    總計 4
    drwxr-xr-x 2 alanjui mongodb 4096  8月 21 18:21 db

    ```

    【註】：

    上述作法，只適合用於「開發者作業」。

    比較正規的作法，應先新增一群組： `mongodb` ，再將 `<使用者帳號>` 加入 mongodb 群組中。

    對於資料庫目錄（`/data/db`），群祖需擁有「讀/寫」使用權限（755）。


  9. 啟動 mongod

    ```
    mongod
    ```
