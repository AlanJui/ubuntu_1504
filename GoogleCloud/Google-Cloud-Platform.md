Google Cloud Platform 記事本
======================

初學、試用，如何在 Google Cloud Platform 建置 Web App 。


# 安裝 Google Cloud SDK

在用來開發的電腦，依據其作業系統，安裝 Google Cloud SDK 。

## Ubuntu 環境：

安裝操作：

__不要使用 Ubuntu 的安裝作法：
[https://cloud.google.com/sdk/#debubu](https://cloud.google.com/sdk/#debubu)__

改用 Linux / OS X 的安裝作法：

1. Download and install Google Cloud SDK by running the following command in your shell or Terminal:

  ```
  curl https://sdk.cloud.google.com | bash
	```

	__安裝過程，系統詢問 GCloud SDK 的安裝處，使用預設，不要修改。__

	預設路俓： ~/google-cloud-sdk

2. Restart your shell:

  ```
	exec -l $SHELL
  ```

## Mac 環境：

安裝操作：
[https://cloud.google.com/sdk/](https://cloud.google.com/sdk/)


# 在 Google Developers Console 建立 Project

使用電腦，透過 Google Developers Console 建立一個 Project 。

1. 先在 Google Developers Console 註冊，建立一個使用者帳號。

2. 登入 Google Developers Console 。

3. 執行「Create Project」指令，以建立一個 Project。

	__記錄 Project ID__

4. 設定帳單啟用 (Enable billing)

  https://console.developers.google.com/project/_/settings?_ga=1.263068556.1032602830.1440057453

# 佈署 App

待完成 NodeJS App 的開發後，可開始佈署。

1. 簽入 Google Cloud Platform

  __gcloud auth login__

  ```
  alanjui@SRV01:~/workspace/Google-Cloud/1-hello-world$ gcloud auth login
  Your browser has been opened to visit:

    https://accounts.google.com/o/oauth2/auth?redirect_uri=http%3A%2F%2Flocalhost%3A8085%2F&prompt=select_account&response_type=code&client_id=32555940559.apps.googleusercontent.com&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fuserinfo.email+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcloud-platform+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fappengine.admin+https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fcompute&access_type=offline

	已在目前的瀏覽器工作階段開啟新視窗。
	Saved Application Default Credentials.

	You are now logged in as [alanjui.1960@gmail.com].
	Your current project is [my-app101-1044].  You can change this setting by running:
	  $ gcloud config set project PROJECT_ID
	```

2. 更新 Google Cloud SDK 元件

  __gcloud components update__

		```
		alanjui@SRV01:~/workspace/Google-Cloud/1-hello-world$ gcloud components update app

		All components are up to date.
		```

3. 設定 Google Console Project ID

  __gcloud config set project <<PROJECT-ID>>__

	```
	alanjui@SRV01:~/workspace/Google-Cloud/1-hello-world$  gcloud config set project  myapp001-1049
	```

4. 執行佈署指令

  __gcloud preview app deploy app.yaml --set-default__

	```
	alanjui@SRV01:~/workspace/Google-Cloud/1-hello-world$ gcloud preview app deploy app.yaml --set-default
	You are about to deploy the following modules:
	 - myapp001-1049/default (from [/home/alanjui/workspace/Google-Cloud/1-hello-world/app.yaml])
	     Deployed URL: [https://myapp001-1049.appspot.com]

	Do you want to continue (Y/n)?  

	Beginning deployment...
	Verifying that Managed VMs are enabled and ready.
	If this is your first deployment, this may take a while...done.

	Provisioning remote build service.
	Created [https://www.googleapis.com/compute/v1/projects/myapp001-1049/global/firewalls/allow-gae-builder].
	NAME              NETWORK SRC_RANGES RULES    SRC_TAGS TARGET_TAGS
	allow-gae-builder default 0.0.0.0/0  tcp:2376          gae-builder
	Copying certificates for secure access. You may be prompted to create an SSH keypair.
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Warning: Permanently added '104.154.67.229' (ECDSA) to the list of known hosts.
	Building and pushing image for module [default]
	Updating module [default]...|Deleted [https://www.googleapis.com/compute/v1/projects/myapp001-1049/zones/us-central1-f/instances/gae-builder-vm-20150826t192821].
	Updating module [default]...done.
	Deployed module [default] to [https://myapp001-1049.appspot.com]
	```



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
