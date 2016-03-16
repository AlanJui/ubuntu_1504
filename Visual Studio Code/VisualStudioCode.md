# 安裝 Visual Studio Code 作業

## 安裝 Visual Studio Code



## 安裝 mono

Visual Studio Code 雖是「Editor」；但支援 node 程式除錯（debug）功能。

但此除錯功能，在 Linux 平台作業時，需配合 mono runtime 才能執行。

且其版本需在「V3.10.10」以上， Visual Studio Code 的除錯功能才能運作。

### 注意 mono runtime 版本

雖然 Ubuntu 的「軟體中心」，提供 mono runtime 套件，看似可以安裝。

但......

因為 Ubuntu 15.04 發行的套件，版本為 V3.2.8 ；無法滿足 Visual Studio Code 最低限度的要求為，所以不能透過「軟體中心」或是「apt-get 指令」直接安裝。

  ~sudo apt-get install mono-complete~

若是不慎已安裝，可透過以下的指令，先解除安裝：

  ```
  $ sudo apt-get uninnstall mono-complete
  ```

### 安裝 mono runtime 套件

以下說明，如何使用 [Mono 官網](http://www.mono-project.com/docs/getting-started/install/linux/#debian-ubuntu-and-derivatives) 提供的版本，進行 mono runtime 安裝作業。  

  1. 取得官網 deb 套件的 GPG 公鑰

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
