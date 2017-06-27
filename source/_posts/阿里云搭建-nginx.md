title: 阿里云搭建 nginx
date: 2017-06-27 15:36:55
tags:
- tech
- PE
---
## 1. 前言
为了开发微信小程序, 要买个 CA 证书, 看到阿里云有免费的, 就给申请, 就在此时又看到了阿里云的 ECS 有大优惠, 1-1-1的配置一年就要300+, 之前300+只能买三个月, 就顺道给买了, 简直是捆绑消费啊, 然而身为 FE 的我在配置阿里云服务器以及做 PE 相关的东西时显得捉襟见肘, 遇到了很多问题, 所以特此记录下来.

## 2. ssh
买了服务器当然要先登录啦, 通过我们的 SSH 客户端来
```
ssh root@123.123.123.123 // 你的服务器公网地址
```
接下来会询问你关于 ssh key 的问题, yes 就好, 另外一种情况, 你在本地登录过此台服务器结果又重装了, 再登录时这个 ssh 密钥会发生变化, 需要去 `vi ~/.ssh/known_hosts`中你的服务器那行给删掉, dd 即可.

## 3. yum
> yum（全称为 Yellow dog Updater, Modified）是一个在Fedora和RedHat以及SUSE中的Shell前端软件包管理器。基於RPM包管理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依赖性关系，并且一次安装所有依赖的软体包，无须繁琐地一次次下载、安装。yum提供了查找、安装、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

## 4. 修改 yum 源
其实 yum 就是类似于 node 中 npm 的包或者依赖管理工具, 其实应该反过来类比更对, 毕竟npm 太年轻, 要知道我们用 npm 时会将源切换到国内的, 这里也是同样的道理. 国内有很多 yum 源, 我也不知道哪家好, 基于 npm 的惯例, 还是用[阿里云](http://mirrors.aliyun.com/help/centos)的吧.  
我这里是 CentOS 7 版本

### 4.1 备份
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```


### 4.2 下载新的CentOS-Base.repo 到/etc/yum.repos.d/
```
wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
或者
curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```

### 4.3 生成缓存
```
yum makecache
```

## 5. 更新 yum 依赖
```
yum -y update
```

## 6. 安装 nginx
```
yum install nginx
```

## 7. 启动 nginx
```
service nginx start
```

## 8. 测试是否成功
```
curl http://127.0.0.1
```
如果有成功的返回则证明成功启动了 nginx 服务器  

## 9. 安全策略
但是, 这时从公网访问此服务器, 或者直接在本地 `curl http://47.xx.xx.xx` 则会发现链接超时, 这个地方坑了我很多天, 本来以为是防火墙的原因, 一直去查 iptables 等的配置, 实际上新的机器 iptables 并不会启用, 没有任何 ACL 来阻止我们的请求, 后来排查发现, 是阿里云有一个外部的总防火墙, 安全策略, 白名单里没有将80端口开放出来, 导致 nginx 的请求被阻止, 在这里进行配置
![安全组](/uploads/img/008 - aliyun-safe.png)
点击'配置规则', '快速创建规则', 将80端口的规则添加进去就 ok 了, 这个时候再访问, 就可以看到成功的页面了
![success](/uploads/img/009 - aliyun-nginx-success.png)

DONE! 至此搭建完毕~