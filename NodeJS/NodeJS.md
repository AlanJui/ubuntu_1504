Node 筆記
========

# 安裝 node 與 npm

(1) 至官網下載 BIN 檔。

注意：不是 .tar.gz 檔案，那是「原始程式碼檔案」;應該是 -x64.tar.gz 。

參考指引： [How to Install Node.js on Ubuntu 14.04 / Install Node.js with Standard Binary Packages ](http://www.hostingadvice.com/how-to/install-nodejs-ubuntu-14-04/)

(2) 執行安裝指令。
```
$ cd ~/下載
$ sudo tar -C /usr/local --strip-components 1 -xzf node-v0.12.7-linux-x86.tar.gz

```
(3) 驗證

步驟一：檢查連結
```
$ ls -l /usr/local/bin/node
$ ls -l /usr/local/bin/npm
```

步驟二：確認軟體能夠執行
```
$ node -v
$ npm -v
```

# 安裝 MongoDB

# 安裝 Yeoman

## 安裝與 Yeoman 相關套件

```
$ sudo npm install -g yo bower grunt-cli gulp
```

## 安裝 Yeoman Generator

### 安裝 [Angular Fullstack Generator](https://github.com/DaftMonk/generator-angular-fullstack)

(1) 執行安裝指令

```
$ sudo npm install -g generator-angular-fullstack
```

(2) 驗證能夠正常執行

執行此工作之前，須先確認以下軟體已先完成安裝：
 - MongoDB
 - SASS & Ruby

```
$ cd ~/workspace/nodeJS

$ mkdir myApp101 && cd $_

$ yo angular-fullstack myApp101


```

### 安裝 hottowel Generator
