
REF:

[Install RVM (Ruby Version Manager) in Ubuntu via PPA](http://www.webupd8.org/2014/11/how-to-install-rvm-ruby-version-manager.html)

(1) To add Rael's PPA and install RVM in Ubuntu (and derivatives), use the following commands:
```
sudo apt-add-repository ppa:rael-gc/rvm
sudo apt-get update
sudo apt-get install rvm
```

>Creating group 'rvm'

>Installing RVM to /usr/share/rvm/
Installation of RVM in /usr/share/rvm/ is almost complete:

>  * First you need to add all users that will be using rvm to 'rvm' group,
    and logout - login again, anyone using rvm will be operating with `umask u=rwx,g=rwx,o=rx`.

>  * To start using RVM you need to run `source /etc/profile.d/rvm.sh`
    in all your open shell windows, in rare cases you need to reopen all shell windows.


(2) Setup for run rvm under terminal
```
$ source /etc/profile.d/rvm.sh
```

(3) Restart your session (logout and login).

執行安裝指令： __rvm install ruby__

```
alanjui@SRV01:~$ rvm install ruby
Searching for binary rubies, this might take some time.
No binary rubies available for: ubuntu/15.04/x86_64/ruby-2.2.1.
Continuing with compilation. Please read 'rvm help mount' to get more information on binary rubies.
Checking requirements for ubuntu.
Requirements installation successful.
Installing Ruby from source to: /usr/share/rvm/rubies/ruby-2.2.1, this may take a while depending on your cpu(s)...
ruby-2.2.1 - #downloading ruby-2.2.1, this may take a while depending on your connection...
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:--  0:00:01 --:--:--     0Warning: Failed to create the file ruby-2.2.1.tar.bz2.part:
Warning: 拒絕不符權限的操作
curl: (23) Failed writing body (0 != 999)
There was an error(23).
Checking fallback: http://ftp.ruby-lang.org/pub/ruby/2.2/ruby-2.2.1.tar.bz2
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0Warning: Failed to create the file ruby-2.2.1.tar.bz2.part:
Warning: 拒絕不符權限的操作
curl: (23) Failed writing body (0 != 4007)
There was an error(23).
Failed download
There has been an error fetching the ruby interpreter. Halting the installation.

```

重新開機，再執行安裝指令。

![操作畫面](file:///_imgs/螢幕快照 2015-08-22 11:32:25.png)
