---
{"dg-publish":true,"permalink":"/Joplin/"}
---

##### Joplin 是一个开源的笔记工具，拥有 Windows/macOS/Linux/iOS/Android/Terminal 版本的客户端。多端同步功能是笔记工具最重要的功能，只有实现了多端同步，我们才能在工作电脑和手机之间无缝切换笔记体验。

本文介绍如何在自己的[服务器](https://cloud.tencent.com/act/pro/promotion-cvm?from_column=20065&from=20065)上利用docker搭建 Joplin Server，并对同步进行配置，再结合cpolar内网穿透工具实现公网远程访问本地Joplin Sever。

#### 1. 安装Docker

本篇文章演示环境为CentOS 7,使用Xshell7进行ssh，需安装Docker,小编在本地Windows中已安装Joplin app，如未安装可到 Joplin官网中安装下载，支持多个版本下载。

Joplin官网地址：https://joplinapp.org/

没有安装Docker的小伙伴需安装Docker:

本教程操作环境为Linux CentOS 7系统，在开始之前，我们需要先安装Docker。

在终端中执行下方命令：

**添加Docker源**

代码语言：javascript

复制

```javascript
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

**安装Dokcer包**

代码语言：javascript

复制

```javascript
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

**通过运行映像来验证 Docker 引擎安装是否成功**

代码语言：javascript

复制

```javascript
sudo docker run hello-world
```

#### 2. 自建Joplin服务器

建立 /data/joplin/docker-compose.yml 文件,首先创建一个/data/joplin/目录

代码语言：javascript

复制

```javascript
mkdir -p /data/joplin
```

![Pasted image 20240826105716.png](/img/user/Pasted%20image%2020240826105716.png)