在启动了Windows类型的实例后，您可以连接并登录它。根据您本地的操作系统和 CVM 实例是否可被 Internet 访问，不同情况下可以使用不同的登录方式，具体内容可参考下表：
<table><tbody>
<tr><th>本地操作系统类型</th><th> Windows 云服务器实例有公网 IP</th><th> Windows 云服务器实例没有公网 IP</th></tr>
<tr><td>Windows</td><td>VNC 登录<br>远程桌面连接</td><td rowspan="3">VNC登录</td></tr>
<tr><td>Linux</td><td>VNC 登录<br>rdesktop登录</td></tr>
<tr><td>Mac OS</td><td>VNC 登录<br>rdesktop登录</td></tr>
</tbody></table>

## 先决条件
登录到云服务器时，需要使用管理员帐号和对应的密码。
- 管理员账号：对于Windows类型的实例，管理员帐号统一为 ***Administrator*** 
- 密码：
  - 若用户在启动实例时选择【自动生成密码】，则初始密码由系统随机分配。您可以登录[腾讯云控制台](https://console.qcloud.com/)，点击右侧站内信按钮，查收新购买的服务器页面中将包含云主机登录管理员帐号及初始密码，如下图所示。
  ![](//mccdn.qcloud.com/img56a20f10a373a.png)
  - 若用户在启动实例时选择了自定义密码，则密码为用户在购买云服务器实例时指定的密码。有关密码的更多内容，如忘记登录密码怎么办，请参考[登录密码]()。

## 本地为Windows时：使用远程桌面连接登录Windows实例
在本地Windows机器上，点击开始菜单 -> Run，输入`mstsc`命令，即可打开远程桌面连接对话框。

在输入框输入Windows服务器的公网IP（登录[云服务器控制台](https://console.qcloud.com/cvm)可查看云服务器的公网IP），如下图所示：
![](//mccdn.qcloud.com/img56b1a11a3c31f.png)

点击【连接】，在新打开的界面中输入[先决条件]()中获取的管理员账号和对应的密码，如下图所示：
![](//mccdn.qcloud.com/static/img/878a0e8ef1a0bcc51ad5de2bcce4e353/image.png)
![](//mccdn.qcloud.com/static/img/e140d3151ac8747014313b33e6413568/image.png)

点击【确定】，即可登录到Windows云服务器。

如果登录失败，请检查您的云服务器实例是否允许3389端口的入流量。端口的查看请参考[安全组](),若您的云服务器处于[私有网络]()环境下，请同时查看相关子网的[网络ACL]()。 

## 本地为Linux时：使用rdesktop登录Windows实例
本地 Linux 计算机要登录远程 Windows 实例时，您需要安装相应的远程桌面连接程序，这里推荐使用 rdesktop 进行连接。有关 rdesktop 的更多内容，请参考[这里](http://www.rdesktop.org/)。

### 安装rdesktop
运行`rdesktop`命令检查系统是否已经安装，若未安装则请[下载最新的安装包](https://github.com/rdesktop/rdesktop/releases)，并在相应目录下运行以下命令解压和安装
```
tar xvzf rdesktop-<x.x.x>.tar.gz ##替换x.x.x为下载的版本号 
cd rdesktop-1.8.3
./configure --disable-credssp --disable-smartcard 
make 
make install
```
### 连接远程Windows实例
运行以下命令（将示例中的参数改为您自己的参数）：

```
rdesktop -u Administrator -p <your-password> <hostname or ip address> 
```
其中：-u 连接用户名即Administrator，-p 连接在先决条件中获得的密码， <hostname or ip address>为您的Windows实例公网IP或域名。

## 本地为Mac OS 时：使用 Microsoft Remote Desktop Connection Client for Mac 登录Windows实例

请前往Microsoft官方网站下载[用于Mac OS的远程登录客户端](https://www.microsoft.com/zh-cn/download/details.aspx?spm=5176.doc25435.2.2.l9afth&id=18140)。

安装完成后请使用先决条件中获得的用户名和密码登录远程Windows实例。

如果登录失败，请检查您的云服务器实例是否允许3389端口的入流量。端口的查看请参考[安全组](),若您的云服务器处于[私有网络]()环境下，请同时查看相关子网的[网络ACL]()。 

## 使用 VNC 连接到实例
VNC登陆是腾讯云为用户提供的一种通过web浏览器远程连接云服务器的方式。在没有安装远程登陆客户端或者客户端远程登陆无法使用的情况下，用户可以通过VNC登陆连接到云服务器，观察云服务器状态，并且可通过云服务器账户进行基本的云服务器管理操作。

VNC登陆的场景至少包括以下几种:
- 查看云服务器的启动进度
- 无法通过客户端SSH或mstsc登录时，通过VNC登陆来登录服务器 

在云服务器列表的操作列，点击【登录】按钮即可通过 VNC 连接至 Windows云服务器。

![](//mccdn.qcloud.com/img56b1a6cb7b3e8.png)

通过在左上角发送Ctrl+Alt+Del命令进入系统登录界面：

![](//mccdn.qcloud.com/img56b1a6ff2e305.png)

>注：
>- Ctrl + Alt + Delete是锁屏后登录Windows或打开任务管理器的快捷键
>- 该终端为独享，即同一时间只有一个用户可以使用VNC登录。
>- 要正常使用VNC登录，需要使用现代浏览器，如：chrome，firefox，IE10及以上版本等。
>- 暂不支持复制粘贴
>- 暂不支持文件上传下载