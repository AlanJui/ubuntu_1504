Google Cloud Platform 記事本
======================

初學、試用，如何在 Google Cloud Platform 建置 Web App 。


# 安裝 Google Cloud SDK

在 Ubuntu 15.04 的電腦，安裝 Google Cloud SDK 。

安裝操作，__不要使用 Ubuntu 的安裝作法：
[https://cloud.google.com/sdk/#debubu](https://cloud.google.com/sdk/#debubu)__

而應改用 __Linux / OS X 的安裝作法：__

1. 在「終端機」執行下列指令。

  ```
  curl https://sdk.cloud.google.com | bash
	```

	__在安裝過程，當系統詢問 Google Cloud SDK 的安裝處時，就直接採用預設，不要修改。__

	預設路俓： ~/google-cloud-sdk

2. 在「終端機」執行以下指令，以便重新設定 Shell 使用的「系統環境變數」:

  ```
	exec -l $SHELL
  ```

3. 將使用者帳號加入 docker 群組

  將使用者帳號： alanjui ，將入群組: docker 。

  * 執行指令。

  ```
  sudo usermod -aG docker alanjui
  ```

  * 先「登出」，再「登入」，以便加入群組的設定生效。


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

  __gcloud config set project [PROJECT-ID]__

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



# 附帶參考

## 在 Mac 環境安裝 Google Cloud SDK

__安裝操作參考__

[https://cloud.google.com/sdk/](https://cloud.google.com/sdk/)

## 佈署 Web App 無法正常運作

執行以下佈署指令，結果卻發生異常：

__gcloud preview app deploy app.yaml --set-default__

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

以上的問題，似乎係因 Docker Daemon 無法正常運作所引起。

試用 Docker Tool for Mac OS X V1.8.1b ，結果，也無法順利啟動其預設的 Docker Container -- Default 。似乎 Docker 在 Mac 的運作，還不算穩定。
