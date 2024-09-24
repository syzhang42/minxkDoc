### 一、创建一个好用的wsl

```
1、获取所有分发
wsl --list --online

2、安装
wsl install --distribution Ubuntu-20.04

3、默认root
cd C:\Users\xxxx\AppData\Local\Microsoft\WindowsApps
ubuntu2004.exe config --default-user root

4、拷贝到d盘
wsl --export Ubuntu-20.04 d:\wsl\ubuntu-2004.tar
wsl --unregister Ubuntu-20.04
wsl --import ubuntu-2004 D:\wsl\ubuntu-2004 D:\wsl\ubuntu-2004.tar

5、换源
cd /etc/apt
mv sources.list sources.list.bak
vi sources.list

sudo apt update

6、安装go 
wget https://dl.google.com/go/go1.23.0.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.23.0.linux-amd64.tar.gz
vim ~/.profile
export PATH=$PATH:/usr/local/go/bin
source ~/.profile

7、修改 go env
go env -w  GOPROXY='https://goproxy.cn,direct'

8、安装git 配置git免密
配置：
git config --global user.email "xxxx@xxxxxxx.com"
git config --global user.name "xxxx"
公钥：
ssh-keygen -t rsa -C "xxxx@xxxxxxx.com"
免密
vim  ~/.gitconfig
[user]
        email = xxxx@xxx.com
        name = xxxx
[http "https://github.com"]
        proxy = https://127.0.0.1:7890
[https "https://github.com"]
        proxy = https://127.0.0.1:7890
[core]
        editor = vim
[url "git@git.xxxxxxx.com:"]
        insteadOf = https://git.xxxxxxx.com/
        
9、安装gcc g++ 内部一般使用4.8.5
apt install gcc-4.8 g++-4.8
4.8.5不是ubuntu20.04默认版本，需要自行创建软连接
cd /usr/bin 
ln -s gcc-4.8* gcc
ln -s g++-4.8* g++

10、机器免密
ssh-keygen
# 复制到 master1 主机
scp root@node-2:~/.ssh/id_rsa.pub /home
# 写入到 authorized_keys 中
cat /home/xxxx/id_rsa.pub >> ~/.ssh/authorized_keys


11、安装cmake  3.15.3
./bootstrap
make -j 4
make install
```

### 二、源

```
ubuntu
# See http://help.ubuntu.com/community/UpgradeNotes for how to upgrade to
# newer versions of the distribution.
deb http://mirrors.ustc.edu.cn/ubuntu/ focal main restricted
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal main restricted

## Major bug fix updates produced after the final release of the
## distribution.
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-updates main restricted

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team. Also, please note that software in universe WILL NOT receive any
## review or updates from the Ubuntu security team.
deb http://mirrors.ustc.edu.cn/ubuntu/ focal universe
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal universe
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-updates universe
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-updates universe

## N.B. software from this repository is ENTIRELY UNSUPPORTED by the Ubuntu
## team, and may not be under a free licence. Please satisfy yourself as to
## your rights to use the software. Also, please note that software in
## multiverse WILL NOT receive any review or updates from the Ubuntu
## security team.
deb http://mirrors.ustc.edu.cn/ubuntu/ focal multiverse
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal multiverse
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-updates multiverse
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-updates multiverse

## N.B. software from this repository may not have been tested as
## extensively as that contained in the main release, although it includes
## newer versions of some applications which may provide useful features.
## Also, please note that software in backports WILL NOT receive any review
## or updates from the Ubuntu security team.
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-backports main restricted universe multiverse

## Uncomment the following two lines to add software from Canonical's
## 'partner' repository.
## This software is not part of Ubuntu, but is offered by Canonical and the
## respective vendors as a service to Ubuntu users.
# deb http://archive.canonical.com/ubuntu focal partner
# deb-src http://archive.canonical.com/ubuntu focal partner

deb http://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-security main restricted
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-security universe
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-security universe
deb http://mirrors.ustc.edu.cn/ubuntu/ focal-security multiverse
# deb-src http://mirrors.ustc.edu.cn/ubuntu/ focal-security multiverse
deb http://dk.archive.ubuntu.com/ubuntu/ xenial main
deb http://dk.archive.ubuntu.com/ubuntu/ xenial universe
```

