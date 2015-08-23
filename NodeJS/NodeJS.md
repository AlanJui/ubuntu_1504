Node 筆記
========

# 安裝 node 與 npm

1. 至官網下載 BIN 檔。

    注意：不是 .tar.gz 檔案，那是「原始程式碼檔案」;應該是 -x64.tar.gz 。

    參考指引： [How to Install Node.js on Ubuntu 14.04 / Install Node.js with Standard Binary Packages ](http://www.hostingadvice.com/how-to/install-nodejs-ubuntu-14-04/)

2. 執行安裝指令。

		cd ~/下載
		sudo tar -C /usr/local --strip-components 1 -xzf node-v0.12.7-linux-x86.tar.gz

3. 驗證

	* 步驟一：檢查連結

			ls -l /usr/local/bin/node
			ls -l /usr/local/bin/npm

  * 步驟二：確認軟體能夠執行
			node -v
			npm -v

# 安裝常用之 node 模組

## Rebuild 工具

		sudo npm install -g node-gyp

## HTTP Server

		sudo npm install -g http-server

# 安裝 MongoDB

參考本指引中，另一篇筆記：「[安裝MongoDB](../MongoDB/安裝MongoDB.md)」作法。

# 安裝 Yeoman

## 安裝與 Yeoman 相關套件

		sudo npm install -g yo bower grunt-cli gulp

## 安裝 Yeoman Generator

### 安裝 [Angular Fullstack Generator](https://github.com/DaftMonk/generator-angular-fullstack)

執行此工作之前，須先確認以下軟體已先完成安裝：
		
 * MongoDB
	 
 * Ruby & SASS

1. 執行安裝指令

		sudo npm install -g generator-angular-fullstack

2. 驗證能夠正常執行

  執行下列指令，以驗證：
		
			cd ~/workspace/nodeJS
			mkdir myApp101 && cd $_
			yo angular-fullstack myApp101

### 安裝 hottowel Generator


# 異常處理

## 無法正常啟動 app ，有錯誤訊息告知：「You need to have Ruby and Sass Installed and in your PATH for this task to work」	

這種狀況發生的導因，通常是因為忘了安裝 Sass ；而 Sass 的安裝係透過 gem 這個套件管理軟體來完成。所以，遇此狀況時，須先檢查 Ruby, gem, Sass 的安裝是否已完成。


## 無法正常啟動 app ，有錯誤訊息告知：「You need to have Ruby and Sass Installed and in your PATH for this task to work」	

依錯誤訊息判斷，應該是 mongoose 這模組出狀況了，故須重新安裝 mongoose 模組。

## 透過 npm install 安裝 mongoose 模組，結果無法順利安裝，有錯誤狀況發生

XXXX


## 懷疑 npm 模組在安裝的時候發生問題

執行 grunt serve 指令，卻發生 app 無法正常啟動的問題，懷疑在 npm install 階段，可能有 npm 的模組未正常完成安裝。

這種狀況可能發生的時機，譬如：透過 Yeoman Generator 在建置 project 的時候，卻忘了先安裝 node-gyp 的模組。

		rm -rf node_modules && npm install 
		
	