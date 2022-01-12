# x2ray
Xray一键脚本使用步骤如下：

1. 准备一个境外服务器，想服务器速度快请参考 搬瓦工VPS购买教程 或从  CN2 GIA VPS商家推荐 选购，想ip被封后免费换请参考：购买vultr服务器超详细图文教程。

如果用VMESS+WS+TLS或者VLESS系列协议，则还需一个域名。对域名没有要求，国内/国外注册的都可以，不需要备案，不会影响使用，也不会带来安全/隐私上的问题。购买域名可参考：Namesilo购买域名详细教程。

值得一提的是本Xray一键脚本支持ipv6 only服务器，但是不建议用只有ipv6的VPS用来科学上网。

在NAT VPS运行本脚本请先参考：在NAT VPS上运行本站一键脚本

2. 如果vps运营商开启了防火墙（阿里云、Ucloud、腾讯云、AWS、GCP等商家默认有，搬瓦工/hostdare/vultr等商家默认关闭），请先登录vps管理后台放行80和443端口，否则可能会导致获取证书失败。此外，本脚本支持上传自定义证书，可跳过申请证书这一步，也可用在NAT VPS上。

3. ssh连接到服务器。Windows系统请参考 Bitvise连接Linux服务器教程，mac用户请参考 Mac电脑连接Linux教程。

4. 复制（或手动输入）下面命令到终端

bash <(curl -sL https://raw.githubusercontent.com/manche123/x2ray/main/xray.sh)

按回车键，将出现如下操作菜单。如果菜单没出现，CentOS系统请输入 yum install -y curl，Ubuntu/Debian系统请输入 sudo apt install -y curl，然后再次运行上面的命令：
![image](https://user-images.githubusercontent.com/34021259/149056687-5fd0296c-cccb-4c99-a8d5-140f4b32c4da.png)
                            Xray一键安装脚本

本Xray一键脚本目前支持以下组合方式：

VMESS，即最普通的V2ray服务器，没有伪装，也不是VLESS
VMESS+KCP，传输协议使用mKCP，VPS线路不好时可能有奇效
VMESS+TCP+TLS，带伪装的V2ray，不能过CDN中转
VMESS+WS+TLS，即最通用的V2ray伪装方式，能过CDN中转，推荐使用
VLESS+KCP，传输协议使用mKCP
VLESS+TCP+TLS，通用的VLESS版本，不能过CDN中转，但比VMESS+TCP+TLS方式性能更好
VLESS+WS+TLS，基于websocket的V2ray伪装VLESS版本，能过CDN中转，有过CDN情况下推荐使用
VLESS+TCP+XTLS，目前最强悍的VLESS+XTLS组合，强力推荐使用（但是支持的客户端少一些）
trojan，轻量级的伪装协议
trojan+XTLS，trojan加强版，使用XTLS技术来提升性能
注意：目前一些客户端不支持VLESS协议，或者不支持XTLS，请按照自己的情况选择组合

5. 按照自己的需求选择一个方式。例如6，然后回车。接着脚本会让你输入一些信息，也可以直接按回车使用默认值。需要注意的是，对于要输入伪装域名的情况，如果服务器上有网站在运行，请联系运维再执行脚本，否则可能导致原来网站无法访问！
![image](https://user-images.githubusercontent.com/34021259/149056890-3c1fd4d3-6995-4964-aa19-d2ad1a0c5fdd.png)
                          xray一键脚本输入

6. 脚本接下来自动运行，一切顺利的话结束后会输出配置信息：
![image](https://user-images.githubusercontent.com/34021259/149056949-c92e7d96-fe62-4a14-a7ef-6d704c0ad595.png)

                        Xray一键脚本运行成功输出信息


到此服务端配置完毕，服务器可能会自动重启（没提示重启则不需要），windows终端出现“disconnected”，mac出现“closed by remote host”说明服务器成功重启了。

对于VLESS协议、VMESS+WS+TLS的组合，网页上输入伪装域名，能正常打开伪装站，说明服务端已经正确配置好。如果运行过程中出现问题，请在本页面下方查找解决方法或留言。

Xray一键脚本其他事项
服务端配置好后，如果想使用CloudFlare等CDN中转（必须是WS版才可以），请参考：使用cloudflare中转流量，拯救被墙ip；

本脚本默认使用的加速技术是BBR，换成魔改BBR/BBR Plus/锐速清参考：安装魔改BBR/BBR Plus/锐速(Lotserver)。

如果伪装站类型没有你满意的，比如你想搭建WordPress博客，请参考：V2ray伪装建站教程。

对于使用TLS的方式，脚本默认会申请域名证书，证书存放在和xray配置文件同一个文件夹内（即/usr/local/etc/xray目录下）。证书会自动更新，如果客户端突然无法使用，请打开伪装网站查看是否能正常打开。如果证书已过期，请再次运行上面的脚本重新配置。

最后，刚搭建好Xray后不要猛上流量，否则会导致被限速、端口被墙，严重可能导致ip被墙。

接下来是配置客户端，下载客户端和配置教程请参考：

V2ray Windows客户端下载
V2ray 安卓客户端下载
V2ray Mac客户端下载
V2ray苹果客户端下载
