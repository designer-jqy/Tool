# 内网穿透

什么室内外穿透呐？如下图所示，通过一个中间服务器，让内网的数据可以被外网获取，或者实现内网和外网的`ssh`链接

![](Photo\原理.jpeg)

## 方法1

使用`ngrok`工具

1. 进入官网[^链接1]，点击主页`Get started for free`进行注册

   <img src="Photo\ngrok主页.png" style="zoom:50%;" />

2. 注册完成后，会自动跳转到如下下载页面。之后，根据自己的操作系统点击右侧的系统版本，可下载对应的压缩包

   <img src="Photo\下载.png" style="zoom:80%;" />

3. 压缩包下载完成后，通过以下命令进行解压缩，可以在当前文件夹下得到一个`ngrok`可执行文件

   `unzip ngrok-stable-linux-amd64.zip`

4. 之后根据网站当前页面`Connect your account`的指示，输入对应的命令，即可在本地写入相应的配置文件

   `./ngrok authtoken XXXXXXXXXXXXXXXXXXXXXXXXXXX`

5. 在终端运行`./ngrok tcp 22`，就会在终端弹出以下信息内容，表示服务端的端口已经开启

   ```shell
   Session Status                online
   Account                       11111 (Plan: Free)
Version                       2.3.8
   Region                        United States (us)
   Web Interface                 http://127.0.0.1:4041
   Forwarding                    tcp://0.tcp.ngrok.io:12345 -> localhost:22
   ```
   
6. 在客户端使用`SecureCRT`或其他远程ssh连接软件连接即可，命令行方式连接可通过`ssh name@0.tcp.ngrok.io -p12345`的方式进行连接

注：ssh连接的前提是在服务端和客户端通过`sudo apt install openssh-server`安装并开启ssh服务`service sshd start`

[链接1]:https://ngrok.com/

[参考]：https://www.zhihu.com/question/27771692

## 方法2

使用`natapp`工具

