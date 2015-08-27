Node 筆記
========

# 安裝 node 與 npm

1. 至官網下載 BIN 檔。

    注意：不是 .tar.gz 檔案，那是「原始程式碼檔案」;應該是 -x64.tar.gz 。

    參考指引： [How to Install Node.js on Ubuntu 14.04 / Install Node.js with Standard Binary Packages ](http://www.hostingadvice.com/how-to/install-nodejs-ubuntu-14-04/)

2. 執行安裝指令。
  ```
	cd ~/下載
	sudo tar -C /usr/local --strip-components 1 -xzf node-v0.12.7-linux-x86.tar.gz
  ```
3. 驗證

	* 步驟一：檢查連結

  ```
  ls -l /usr/local/bin/node
  ls -l /usr/local/bin/npm
  ```

  * 步驟二：確認軟體能夠執行

  ```
  node -v
  npm -v
  ```

# 安裝常用之 node 模組

## Rebuild 工具
```
sudo npm install -g node-gyp
```

## HTTP Server
```
sudo npm install -g http-server
```

## 測試工具 Mocha
```
sudo npm install -g mocha
```

## 測試工具 Karma
```
sudo npm install -g karma-cli
```

# 安裝 MongoDB

參考本指引中，另一篇筆記：「[安裝MongoDB](../MongoDB/安裝MongoDB.md)」作法。

# 安裝 Yeoman

## 安裝與 Yeoman 相關套件
```
sudo npm install -g yo bower grunt-cli gulp
```

## 安裝 Yeoman Generator

### 安裝 [Angular Fullstack Generator](https://github.com/DaftMonk/generator-angular-fullstack)

執行此工作之前，須先確認以下軟體已先完成安裝：

 * MongoDB

 * Ruby & SASS

1. 執行安裝指令
  ```
	sudo npm install -g generator-angular-fullstack
  ```
2. 驗證能夠正常執行

  執行下列指令，以驗證：
  ```
  cd ~/workspace/nodeJS  
  mkdir myApp101 && cd $_  
  yo angular-fullstack myApp101
  ```  
  
### 安裝 hottowel Generator

1. 執行 generator 安裝指令
  ```
	sudo npm install -g generator-hottowel
  ```

2. 驗證能夠正常執行

  * 建立 project 目錄
  
  ```
  mkdir -p ~/workspace/vs-code && cd $_
  mkdir helloWorld && cd $_  
  ```

  * 使用 hottowel generator 建立 project
  
  ```
  yo hottowel myApp101
  ```  

  * 執行 code 分析
  
  ```
  gulp vet
  ```  

  * 執行功能測試

  ```
  gulp serve-specs
  ```  

  * 執行開發中 App

  ```
  gulp serve
  ```  

  * 執行産品建製（build）

  ```
  gulp build
  ```  

  * 執行産品 App

  ```
  gulp serve-build
  ```  

## 安裝 mono

Visual Studio Code 除錯時，需要 mono runtime 軟體配合，故需安裝。

因為 Ubuntu 15.04 發行的套件軟體，其版本為 V3.2.8 ；但 Visual Studio Code 的最低限度要求為 V3.10.10 ，所以不能使用下列的指令直接安裝。

~sudo apt-get install mono-complete~

如果已安裝了錯誤的 mono 版本，請先執行以下的解除安裝指令，再安裝正確的新片本。

```
sudo apt-get uninnstall mono-complete
```

請改用 [Mono 官網](http://www.mono-project.com/docs/getting-started/install/linux/#debian-ubuntu-and-derivatives) 提供的版本，進行安裝作業。  

1. 取得官網 deb 套件的 GPG 公鑰。

  ```
  sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
  ```
  
2. 設定 Ubuntu 的套件來源

  ```
  echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
  ```

3. 更新 Ubuntu 套件來源清單

  ```
  sudo apt-get update
  ```

4. 安裝 mono 套件

  ```
  sudo apt-get uninnstall mono-complete
  ```

5. 驗證

  __mono --version__
  
  ```
  alanjui@SRV01:~/workspace/vs-code/helloWorld$ mono --version
  Mono JIT compiler version 4.0.3 (Stable 4.0.3.20/d6946b4 Tue Aug  4 09:43:57 UTC 2015)
  Copyright (C) 2002-2014 Novell, Inc, Xamarin Inc and Contributors. www.mono-project.com
    TLS:           __thread
    SIGSEGV:       altstack
    Notifications: epoll
    Architecture:  amd64
    Disabled:      none
    Misc:          softdebug
    LLVM:          supported, not enabled.
    GC:            sgen
  ```


# 異常處理

## 無法正常啟動 app ，有 Sass 相關錯誤狀況發生

![](../_imgs/grunt-serve-sass.png)

錯誤訊息告知：「You need to have Ruby and Sass Installed and in your PATH for this task to work」。

這種狀況發生的導因，通常是因為忘了安裝 Sass ；而 Sass 的安裝係透過 gem 這個套件管理軟體來完成。所以，遇此狀況時，須先檢查 Ruby, gem, Sass 的安裝是否已完成。

## 無法正常啟動 app ，有 MongoDB 相關錯誤狀況發生。

![](../_imgs/grunt-serve-mongodb-core-err.png)

依錯誤訊息判斷，應該是 mongoose 這模組出狀況了，故須重新安裝 mongoose 模組。

## 安裝 mongoose 模組，發生錯誤狀況

透過 npm install 安裝 mongoose 模組，結果無法順利安裝，有錯誤狀況發生。

1. 執行下列安裝指令：
  ```
  npm install mongoose
  ```

2. 發生如下所示之錯誤狀況：

  ![](../_imgs/npm-install-mongoose-err.png)

3. 依據錯誤訊息的反應，問題導因出在目錄的使用權限。使用指令 ls -ld 查詢該目錄的權限，發覺目錄的擁有者竟是 root ，而不是正常的 alanjui 。

  ![](../_imgs/npm_module_readable-stream.png)

4. 使用指令，變更目錄的擁有者為 alanjui 所有，以改正問題。
  ```
  sudo chown -R alanjui:alanjui /home/alanjui/.npm/readable-stream
  ```
  
## 懷疑 npm 模組在安裝的時候發生問題

執行 grunt serve 指令，卻發生 app 無法正常啟動的問題，懷疑在 npm install 階段，可能有 npm 的模組未正常完成安裝。

這種狀況可能發生的時機，譬如：透過 Yeoman Generator 在建置 project 的時候，卻忘了先安裝 node-gyp 的模組。

```
rm -rf node_modules && npm install
```
