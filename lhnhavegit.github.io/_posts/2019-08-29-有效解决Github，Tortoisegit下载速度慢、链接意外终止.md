

因为一些众所周知的原因，国内访问GitHub总会遇到下载速度缓慢、链接意外终止的情况。
![github](https://img-blog.csdnimg.cn/20190829091333297.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
为了更加愉快地使用~~全球最大同性交友~~网站上的优质资源，我们来做一些简单的本机上的调整。

通过查看下载链接，能够发现最终被指向到Amazon的服务器（http://github-cloud.s3.amazonaws.com）了。由于国内访问亚马逊网站非常慢，我们需要修改Hosts文件来实现流畅访问。
# 第一步，打开本机上的Hosts文件
首先，什么是Hosts文件？
>在互联网协议中，host表示能够同其他机器互相访问的本地计算机。一台本地机有唯一标志代码，同网络掩码一起组成IP地址，如果通过点到点协议通过ISP访问互联网，那么在连接期间将会拥有唯一的IP地址，这段时间内，你的主机就是一个host。
在这种情况下，host表示一个网络节点。host是根据TCP/IP for Windows 的标准来工作的，它的作用是包含IP地址和Host name(主机名)的映射关系，是一个映射IP地址和Host name(主机名)的规定，规定要求每段只能包括一个映射关系，IP地址要放在每段的最前面，空格后再写上映射的Host name主机名　。对于这段的映射说明用“#”分割后用文字说明。

~Linux/Mac 终端内输入：
>sudo vim /etc/hosts

打开之后，我们就要向里面追加信息了。
# 第二步，追加域名的IP地址
我们可以利用[https://www.ipaddress.com/](https://www.ipaddress.com/) 来获得以下两个GitHub域名的IP地址：

(1) github.com

(2) github.global.ssl.fastly.net

打开网页后，利用输入框内分别查询两个域名：
![主页](https://img-blog.csdnimg.cn/20190829092425840.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
先试一下github.com：
![github.com](https://img-blog.csdnimg.cn/20190829092559853.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
在标注的IP地址中，任选一个记录下来。

再来是github.global.ssl.fastly.net：
![github.global.ssl.fastly.net](https://img-blog.csdnimg.cn/20190829092716666.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
将以上两段IP写入Hosts文件中：![修改hosts文件](https://img-blog.csdnimg.cn/20190829092837886.jpg)
# 第三步，刷新 DNS 缓存
在终端或CMD中，执行以下命令：

>ipconfig /flushdns

![刷新ip](https://img-blog.csdnimg.cn/20190829093502846.jpg)

收工。

现在再来试一下 git clone 命令，或者使用其他工具进行clone,是不是可以轻松过百K了(之前只有10K左右)
![下载速度](https://img-blog.csdnimg.cn/20190829094315910.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzM1MTEyNTY3,size_16,color_FFFFFF,t_70)
