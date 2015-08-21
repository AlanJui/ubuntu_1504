# Ubuntu 15.04

# Git 簽名

```
alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.email "alanjui.1960@gamil.com"

alanjui@SRV01:~/workspace/Ubuntu_1504$ git config --global user.name "Alan Jui"
```

# 首次納管

```
echo "# Ubuntu 15.04" >> README.md
git init
git add .
git commit -m "first commit"
git remote add origin git@github.com:AlanJui/ubuntu_1504.git
git push -u origin master
```
