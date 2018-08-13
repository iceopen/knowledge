# 服务器技能管理
## Linux 服务器基本技能

## Ubuntu 镜像源配置建议使用阿里云
编辑/etc/apt/sources.list文件(需要使用vim), 在文件最前面添加以下条目(操作前请做好相应备份)

```
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
```

## Ubuntu&CentOs 服务器在线更新
- 1.通过 **export http_proxy=http://代理服务器IP:代理端口** 设置可以连通的服务器地址
- 2.通过 apt-get update 或 yum update 进行更新

## 备注：
- [网易开源镜像站](http://mirrors.163.com/)
- [USTC Open Source Software Mirror](http://mirrors.ustc.edu.cn/)
- [repository file generator](https://mirrors.ustc.edu.cn/repogen/)
- [huaweicloud](https://mirrors.huaweicloud.com/)