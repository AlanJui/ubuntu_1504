# 硬碟安裝及設定作業

## 自動掛載第二台硬碟

  1. 查第二台硬碟的UUID

  ```
  $ sudo blkid
  ```

  查 /dev/sdb 的 UUID

  2. 編輯設定檔 /etc/fstab

  ```
  $ sudo gedit /etc/fstab
  ```

  加入內容：
  ```
  # NAS01
  UUID=9279ede9-49f6-44fe-b481-261500f67675	/media		ext4    defaults		0		2
  ```

  3. 第一次手動掛載硬碟

  ```
  $ sudo mount /media
  ```
