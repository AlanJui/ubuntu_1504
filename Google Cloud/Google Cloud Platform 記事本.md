Google Cloud Platform 記事本
---------------------------

初學、試用，如何在 Google Cloud Platform 建置 Web App 。


# 建置環境

## 在 Google Gloud 平台建立一個 Project

使用電腦，透過 Google Developers Console 建立一個 Project 。

（1）先在 Google Developers Console 註冊，建立一個使用者帳號。

（2）登入 Google Developers Console 。

（3）執行「Create Project」指令，以建立一個 Project。
		記錄 Project ID

## 在開發電腦安裝 Google Cloud SDK

用來開發的電腦，依據其作業系統，安裝 Google Cloud SDK 。 

### Mac 環境：

安裝操作：
[https://cloud.google.com/sdk/](https://cloud.google.com/sdk/)

### Ubuntu 環境： 

安裝操作：
[https://cloud.google.com/sdk/#debubu](https://cloud.google.com/sdk/#debubu)


# 異常狀況紀錄

# Mac 環境

## 佈署時無法正常運作

執行初次佈署指令： gcloud preview app deploy app.yaml --set-default ，卻是發生異常結果。

```
MAC2012:1-hello-world AlanJui$ gcloud preview app deploy app.yaml --set-default
You are about to deploy the following modules:
 - clear-storm-104403/default (from [/Users/AlanJui/1-hello-world/app.yaml])
     Deployed URL: [https://clear-storm-104403.appspot.com]

Do you want to continue (Y/n)?

Beginning deployment...
Verifying that Managed VMs are enabled and ready.
If this is your first deployment, this may take a while...done.

ERROR: (gcloud.preview.app.deploy) Couldn't connect to the docker daemon.
MAC2012:1-hello-world AlanJui$
```

# Ubuntu 環境

## 佈署時無法正常運作

同 Mac ，一樣無法正常佈署，但狀況有兩種：

### 狀況一：使用一般 Linux 的方法，完成 SDK 的安裝：

得到同 Mac 的「異常狀況」。

### 狀況二：使用 Ubuntu 專用的方法，完成 SDK 的安裝：

```
alanjui@SRV01:~/workspace/Google-Cloud/myApp101$ gcloud preview app deploy app.yaml --set-default
You do not currently have this command group installed.  Using it
requires the installation of components: [preview]
You cannot perform this action because this Cloud SDK installation is
managed by an external package manager.  If you would like to get the
latest version, please see our main download page at:

https://developers.google.com/cloud/sdk/

ERROR: (gcloud) The component manager is disabled for this installation
alanjui@SRV01:~/workspace/Google-Cloud/myApp101$

```

問題的導因，似乎是指 SDK 套件中的某些元件沒安裝，故而透過「Ubuntu軟體中心」，安裝了如下的原件：

 * Configuration for ubuntu on Google Engine: gce-cloud-config
 * Google daemon for configuring instances: gce-daemon
 * Bundle image for use on Google Compute Engine: gce-imagebundle
 * Google Compute Engine Start-up scripts: gce-stargup-scripts
 
> 