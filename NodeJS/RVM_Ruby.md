
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

```
rvm install ruby
```
