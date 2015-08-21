安裝及設定 MongoDB
=================

# 安裝 MongoDB 套件

參考指引： [Install MongoDB From Tarball ](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-linux/)


(1) 下載 BIN 檔案。
```
curl -O https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.5.tgz
```

(2) 解壓縮。
```
tar -zxvf mongodb-linux-x86_64-3.0.5.tgz
```

(3) 將完成解壓縮的目錄，搬到欲安裝的路徑下。
```
mkdir -p ~/Applications/MongoDB
cp -R -n mongodb-linux-x86_64-3.0.5/ ~/Applications/MongoDB
```

(4) 設定CLI執行時所需的環境變數PATH
```
sudo gedit ~/.bashrc
```

設定內容：
```
# MongoDB
export PATH=/home/alanjui/Applications/MongoDB/mongodb-linux-x86_64-3.0.5/bin:$PATH

```

(5) 重啟終端機的環境設定變更
```
alanjui@SRV01:~$ source ~/.bashrc

alanjui@SRV01:~$ echo $PATH
/home/alanjui/Applications/MongoDB/mongodb-linux-x86_64-3.0.5/bin:/home/alanjui/SDK/jdk1.7.0_79/bin:/home/alanjui/SDK/jdk1.7.0_79/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
```

# 執行 MongoDB

(1) 建立資料庫目錄（Data Directory）。

```
sudo mkdir -p /data/db
```

/data目錄的權限設定：
```
alanjui@SRV01:~$ ls -al /data/
總計 12
drwxr-xr-x  3 root root 4096  8月 21 18:21 .
drwxr-xr-x 25 root root 4096  8月 21 18:21 ..
drwxr-xr-x  2 root root 4096  8月 21 18:21 db
```

未建「資料庫目錄」就直接啟動 mongod ，會發生如下的異常狀況：
```
alanjui@SRV01:~$ mongod
2015-08-21T18:16:15.455+0800 I STORAGE  [initandlisten] exception in initAndListen: 29 Data directory /data/db not found., terminating
2015-08-21T18:16:15.455+0800 I CONTROL  [initandlisten] dbexit:  rc: 100
alanjui@SRV01:~$
```

(2) 設定資料庫目錄的使用權限。

(2-1) 透過「使用者及群組」，新增一「mongodb」群組, 並將「alanjui」帳號加入該群組中。

(2-2) 設定 mongodb 群祖擁有資料庫目錄的「讀/寫」使用權限。

```
sudo chown -R root:mongodb /data

alanjui@SRV01:~$ ls -l /data/
總計 4
drwxr-xr-x 2 root mongodb 4096  8月 21 18:21 db

```

(3) 啟動 mongod

```
mongod
```

===========================================================

參考指引： [Install MongoDB on Ubuntu](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/)

(1) 安裝「Ubuntu 軟體中心」需要的GPG Key
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
```

(2) 設定軟體套件的 List File

```
alanjui@SRV01:~$ echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
deb http://repo.mongodb.org/apt/ubuntu vivid/mongodb-org/3.0 multiverse

alanjui@SRV01:~$ gedit /etc/apt/sources.list.d/mongodb-org-3.0.list
```

注意：如下所示的官方的安裝指引，不可使用。因為「$(lsb_release -sc」的執行結果，會填入「vidid」，這將造成無法讀到套件的問題。因為官方不支援 Vivid 。 ：
```
echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
deb http://repo.mongodb.org/apt/ubuntu vivid/mongodb-org/3.0 multiverse
```


(3) 建立套件的資料庫

```
sudo apt-get update
```

(4) 安裝套件

```
sudo apt-get install -y mongodb-org
```
