### List

Fuzzing101	----> guthub 

xray				----->github

xray + xtls	------> 

​					https://v2xtls.org



iterm2 	----->  https://zhuanlan.zhihu.com/p/112383265?from_voters_page=true

https://imeizi.me/#/?page=1

​					

这是本人推荐的方式，花费一般比VPN少，但更稳定，而且没有设备数量限制，部署好后无限设备同时使用，随意分享给家人和好友使用。

自己部署有四个步骤：

\1. 购买服务器，想要服务器稳定、速度快请参考 [搬瓦工VPS购买教程](https://v2xtls.org/搬瓦工vps购买教程/) 或 [购买AkkoCloud德国、美西CN2 GIA VPS](https://www.akkocloud.com/aff.php?aff=122&gid=7)，希望ip被封后免费换请参考：[购买vultr服务器超详细图文教程](https://v2xtls.org/购买vultr服务器超详细图文教程/)；

\2. 连接到服务器，Windows系统请参考 [Bitvise连接Linux服务器教程](https://v2xtls.org/bitvise连接linux服务器教程/)，mac用户请参考 [Mac电脑连接Linux教程](https://v2xtls.org/mac电脑连接linux教程/)

\3. 运行一键脚本。目前主流的翻墙技术主要有四种，本站都提供了一键脚本：

- Shadowsocks/SS，请参考：[Shadowsocks/SS一键脚本](https://v2xtls.org/shadowsocks-ss一键脚本/)
- ShadowsocksR/SSR，请参考：[ShadowsocksR/SSR一键脚本](https://v2xtls.org/shadowsocksr-ssr一键脚本/)
- V2Ray，请参考：[V2Ray一键脚本](https://v2xtls.org/v2ray多合一脚本，支持vmesswebsockettlsnginx、vlesstcpxtls、vlesstcptls等组合/)
- trojan，请参考：[trojan一键脚本](https://v2xtls.org/trojan一键脚本/)

**注意：**你可任选一种技术（推荐v2ray），也可以在服务器上同时安装多个软件，**但这些软件的端口必须不同！**

\4. 下载并配置客户端。本站提供了各种技术的客户端下载以及详细的配置教程，**请在顶部菜单中选择技术类别**，然后阅读相关文章。

**自己部署的优点是比较稳定、花钱少，没有设备数量限制**。缺点主要是**折腾**，需要看懂本站或网上的教程。如果部署过程中遇到问题，请到 [网络跳越论坛](https://hijk.club/) 查看解决方案和交流。

愿网络无边界，自由可及。



# 搬瓦工VPS购买教程

> 本文转载自：https://v2raytech.com/bandwagonghost-buy-vps-tutorial/，如文中内容有错误请到原文查看原始版(最新版)

> 使用过程中遇到问题，欢迎到 [网络跳越论坛](https://hijk.club/) 或 tg群组https://t.me/hijkclub 交流，或关注Youtube频道：[网络跳越](https://youtube.com/channel/UCYTB--VsObzepVJtc9yvUxQ)
>
> 2020.06.11更新：搬瓦工香港套餐从PCCW升级为CN2 GIA，价格不变
>
> 202.1.10更新：搬瓦工下架洛杉矶CN2 GIA套餐，仅保留CN2 GIA-E线路

## 搬瓦工介绍

[搬瓦工](https://bwh89.net/aff.php?aff=55490&gid=1) 是一家全球知名的美国vps服务商，以~~廉价~~、高速稳定(线路针对中国做了特别优化)而深受国人喜爱。**搬瓦工提供30天不满意退款服务**，稳定运营多年，基本上没有跑路风险。因太多网友买它的vps做你懂的事，因此官网及镜像经常被屏蔽。目前能直接访问的最新官网是：[https://bwh89.net/](https://bwh89.net/aff.php?aff=55490&gid=1)。

> **注意：**搬瓦工服务器换ip需要手续费，如果希望ip被墙免费换，可以考虑vultr，购买请参考： [购买vultr服务器超详细图文教程](https://v2xtls.org/购买vultr服务器超详细图文教程/)

本教程介绍购买和使用搬瓦工vps的详细步骤，附省钱优惠码。

## 搬瓦工VPS购买教程

搬瓦工提供种类繁多的套餐，服务器网速排序是：**搬瓦工香港 > 搬瓦工CN2 GIA-E >= 搬瓦工CN2 GIA > 搬瓦工CN2 > 普通KVM**。一般来说速度越好的越贵(香港vps每月90刀起，仅有500G流量，适合土豪)，性价比高的套餐经常断货（49.99刀每年的CN2 GIA基本抢不到）。

> 如果仅是科学上网，也可考虑购买 [搬瓦工官方代理服务Just My Socks](https://v2xtls.org/just-my-socks购买和使用教程/)

[搬瓦工套餐列表](https://bwh89.net/aff.php?aff=55490&gid=1) 列出了许多套餐，个人建议重点考虑如下几款(点进去显示”out of stock”说明该套餐没货了)：

| 套餐               | 配置                                                         | 价格                                                         | 链接                                                     |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :------------------------------------------------------- |
| **CN2 20GB**       | CPU：1 核内存：1024 MB硬盘：20 GB SSD流量：1000 GB / 月带宽：1 Gbps机房：CN2 9个机房迁移：可迁移机房，流量不变 | 49.99 刀/年常年有货，入门首选                                | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=57) |
| **CN2 40GB**       | CPU：1 核内存：2048 MB硬盘：40 GB SSD流量：2000 GB/月**带宽：1 Gbps**机房：CN2 9个机房迁移：可迁移机房，流量不变 | 52.99 刀/半年99.99 刀/年                                     | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=58) |
| **CN2 GIA-E 20GB** | CPU：2 核内存：1 GB硬盘：20 GB SSD流量：1000 GB/月**带宽：2.5 Gbps**机房：DC6 CN2 GIA-E等11个机房迁移：可迁移机房，流量不变 | 49.99 刀/季89.99刀/半年169.99 刀/年高端首选                  | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=87) |
| **CN2 GIA-E 40GB** | CPU：3 核内存：2 GB硬盘：40 GB SSD流量：2000 GB/月**带宽：2.5 Gbps**机房：DC6 CN2 GIA-E等10个机房迁移：可迁移机房，流量不变 | 89.99 刀/季度169.99 刀/半年299.99 刀/年                      | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=88) |
| **香港 40G**       | CPU：2 核内存：2048 MB硬盘：40 GB SSD流量：500 GB/月**带宽：1 Gbps**机房：香港 HKHK_8迁移：不可迁移机房 | 89.99 刀/月899.99 刀/年尽管贵，但经常没货                    | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=95) |
| **香港 80G**       | CPU：4 核内存：4096 MB硬盘：80 GB SSD**流量：1000 GB/月****带宽：1 Gbps**机房：香港 HKHK_8迁移：不可迁移机房 | 155.99 刀/月439.99 刀/季829.99 刀/半年1559.99 刀/年常年有货，土豪专用 | [直达链接->](https://bwh89.net/aff.php?aff=55490&pid=96) |

> 如果上述套餐不满意或无货，请在 [套餐列表](https://bwh89.net/aff.php?aff=55490&gid=1) 页面搜”HONG KONG”查看香港套餐，搜”GIA”查看GIA/GIA-E套餐，搜”CN2″查看CN2套餐。如果没有满意的套餐，可考虑 [其他CN2 GIA VPS和商家](https://v2xtls.org/cn2-gia-vps和商家推荐/)，或购买 [搬瓦工官方代理服务Just My Socks](https://v2xtls.org/just-my-socks购买和使用教程/)

选好套餐后进入详情界面，可选择购买付费周期和机房：

[![搬瓦工订单界面](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E8%AE%A2%E5%8D%95%E7%95%8C%E9%9D%A2.png)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工订单界面.png)

搬瓦工订单界面

确认服务器配置没问题，选好机房（默认机房就可以），点击下方的“Add to Cart”加入购物车，进入订单界面：

[![搬瓦工订单确认界面](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E8%AE%A2%E5%8D%95%E7%A1%AE%E8%AE%A4%E7%95%8C%E9%9D%A2.png)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工订单确认界面.png)

搬瓦工订单确认界面

> **2020.11.27更新**：搬瓦工黑五促销，请使用搬瓦工优惠码 `BWH2020BF`优惠10%，续费同价

优惠码输入框输入 `**BWH3HYATVBJW**`，然后点击“Validate Code”，可以优惠6.58%。确认无误后，点击右边的 “Checkout” 进入付款页面：

[![搬瓦工创建新订单](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E5%88%9B%E5%BB%BA%E6%96%B0%E8%AE%A2%E5%8D%95.png)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工创建新订单.png)

搬瓦工创建新订单

根据提示填入个人信息，其中国家先选中国(China)，州/省 一栏会变成输入框，使用拼音输入省、城市即可，填写好后按“Update”。在支付方式一栏选择“Alipay”（支付宝），勾选“I have read and agree to the Terms of Service”，然后点击下方的“Complete Order”，进入付款界面。确认支付方式是Alipay，点击绿色的 “Pay now”按钮进入支付宝扫码付款页面，打开手机支付宝扫码付款即可。

[![搬瓦工支付宝付款](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E6%94%AF%E4%BB%98%E5%AE%9D%E4%BB%98%E6%AC%BE.png)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工支付宝付款.png)

搬瓦工支付宝付款

## 搬瓦工VPS管理教程

支付成功后，选择菜单界面的Services -> MyService（如果没登录请先点击右上角的 “Client Area” 用刚才填写的电子邮箱和账户密码登录），点击就可以看到刚才买的vps：

[![搬瓦工已购买vps列表](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E5%B7%B2%E8%B4%AD%E4%B9%B0vps%E5%88%97%E8%A1%A8.jpg)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工已购买vps列表.jpg)

搬瓦工已购买vps列表

点击右边的KiwiVM Control Panel，可以查看VPS信息：

[![搬瓦工vps信息](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5vps%E4%BF%A1%E6%81%AF.jpg)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工vps信息.jpg)

搬瓦工vps信息

### 搬瓦工重装系统教程

本站的一键脚本支持CentOS 7/8、Ubuntu 16.04及高版本系统，如果系统不是这两种，第一件事应该是重装操作系统（如果是请往下看）：

1. vps信息页面上点击 “stop” 按钮关机；
2. 点击左边菜单栏的 “Install new OS”，在系统镜像中选择 “centos7-x86_64”，勾选下面的 “I agree that all existing data on my VPS will be lost”；
3. 点击 “Reload” 重装。重装期间会显示 vps 的root密码、新的SSH端口，**请务必记住root密码，因为只会出现一次**！

[![搬瓦工重装系统信息](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E9%87%8D%E8%A3%85%E7%B3%BB%E7%BB%9F%E4%BF%A1%E6%81%AF.jpg)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工重装系统信息.jpg)

搬瓦工重装系统信息

### 搬瓦工重置root密码教程

如果系统已经是CentOS 7/8或者Ubuntu 16.04及以上版本系统，或你忘记了root密码，搬瓦工可以直接重置root密码。操作流程如下：

1. 确保VPS处于开机状态；
2. 点击左侧菜单的 “root password modification”，点击 “generate and set new password” 重置密码：

[![搬瓦工重置root密码](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E9%87%8D%E7%BD%AEroot%E5%AF%86%E7%A0%81-1024x632-1.jpg)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工重置root密码-1024x632-1.jpg)

搬瓦工重置root密码

重置密码成功后会显示新的密码，请牢记新密码：

[![搬瓦工重置root密码成功](https://v2xtls.org/wp-content/uploads/2020/11/%E6%90%AC%E7%93%A6%E5%B7%A5%E9%87%8D%E7%BD%AEroot%E5%AF%86%E7%A0%81%E6%88%90%E5%8A%9F-1024x703-1.jpg)](https://v2xtls.org/wp-content/uploads/2020/11/搬瓦工重置root密码成功-1024x703-1.jpg)

搬瓦工重置root密码成功

至此购买vps教程结束，你已经有了vps的IP、SSH端口和root密码，接下来开始连接到服务器运行一键脚本吧。

**买服务器只是科学上网的第一步**，请继续往下看教程！

## 连接搬瓦工服务器

**连接服务器是科学上网的第二步。**

windows用户请参考：[Bitvise连接Linux服务器教程](https://v2xtls.org/bitvise连接linux服务器教程/)

mac系统请参考：[Mac电脑连接Linux教程](https://v2xtls.org/mac电脑连接linux教程/)

**运行一键脚本是科学上网的第三步。**本站提供四种技术的一键部署教程供参考（四选一即可，当然同时安装四个也是没问题的！）：

**[Shadowsocks/SS一键脚本](https://v2xtls.org/shadowsocks-ss一键脚本/)**

**[ShadowsocksR/SSR一键脚本](https://v2xtls.org/shadowsocksr-ssr一键脚本/)**

**[V2Ray一键脚本](https://v2xtls.org/v2ray一键脚本/)**

[**trojan一键脚本**](https://v2xtls.org/trojan一键脚本/)

**注意：**你可任选一种技术（推荐v2ray），也可以在服务器上同时安装四个软件，**但四个软件的端口必须不同！**

**科学上网的最后一步是**下载客户端并**配置**，一键脚本里有电脑、手机的下载链接，请下载并参考教程配置客户端。有问题请先仔细看教程，然后参考 [科学上网常见问题](https://v2xtls.org/科学上网常见问题/) 。

如果使用中感觉不满意，可以申请退款，操作请参考：[搬瓦工退款教程](https://v2xtls.org/搬瓦工vps-bandwagonhost-如何退款？退款政策详解-退款教程/)





# Xray一键脚本

> 本文转载自：https://v2raytech.com/xray-one-click-script/，如文中内容有错误请到原文查看原始版(最新版)

> 使用过程中遇到问题，欢迎到 [网络跳越论坛](https://hijk.club/) 或 tg群组https://t.me/hijkclub 交流，或关注Youtube频道：[网络跳越](https://youtube.com/channel/UCYTB--VsObzepVJtc9yvUxQ)

Xray项目已经确定独自运作，目前最新版是1.1.2版本。根据测试数据，服务端direct+客户端使用splice后性能比VLESS裸奔还要强上一倍，已经远超trojan/trojan-go，非常推荐使用。

本文的Xray一键脚本可以配置常规VMESS协议、VMESS+KCP、VMESS+websocket+TLS+Nginx、VLESS+TCP+XTLS、VLESS+TCP+TLS、trojan、trojan+XTLS等多种组合，支持CentOS 7/8、Ubuntu 16.04、Debian 8及新版系统。

## Xray一键脚本使用方法

[Xray一键脚](https://v2xtls.org/tag/xray一键脚本/)本使用步骤如下：

\1. 准备一个境外服务器，想服务器速度快请参考 [搬瓦工VPS购买教程](https://v2xtls.org/搬瓦工vps购买教程/) 或从 [CN2 GIA VPS商家推荐](https://v2xtls.org/cn2-gia-vps和商家推荐/) 选购，想ip被封后免费换请参考：[购买vultr服务器超详细图文教程](https://v2xtls.org/购买vultr服务器超详细图文教程/)。

如果用VMESS+WS+TLS或者VLESS系列协议，则还需一个域名。对域名没有要求，国内/国外注册的都可以，**不需要备案**，不会影响使用，也不会带来安全/隐私上的问题。购买域名可参考：[Namesilo购买域名详细教程](https://v2xtls.org/namesilo域名注册和使用教程/)。

值得一提的是本Xray一键脚本支持ipv6 only服务器，但是不建议用只有ipv6的VPS用来科学上网。

\2. 如果vps运营商开启了防火墙（阿里云、Ucloud、腾讯云、AWS、GCP等商家默认有，搬瓦工/hostdare/vultr等商家默认关闭），请先登录vps管理后台放行80和443端口，否则可能会导致获取证书失败。此外，**本脚本支持上传自定义证书**，可跳过申请证书这一步，也可用在[NAT VPS](https://v2raytech.com/tag/nat-vps/)上。

\3. ssh连接到服务器。Windows系统请参考 [Bitvise连接Linux服务器教程](https://v2xtls.org/bitvise连接linux服务器教程/)，mac用户请参考 [Mac电脑连接Linux教程](https://v2xtls.org/mac电脑连接linux教程/)。

\4. 复制（或手动输入）下面命令到终端：

```
bash <(curl -sL https://s.hijk.art/xray.sh)
```

按回车键，将出现如下操作菜单。如果菜单没出现，CentOS系统请输入 `yum install -y curl`，Ubuntu/Debian系统请输入 `sudo apt install -y curl`，然后再次运行上面的命令：

[![Xray一键安装脚本](https://v2xtls.org/wp-content/uploads/2020/12/Xray%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E8%84%9A%E6%9C%AC.jpg)](https://v2xtls.org/wp-content/uploads/2020/12/Xray一键安装脚本.jpg)

Xray一键安装脚本

本Xray一键脚本目前支持以下组合方式：

- **VMESS**，即最普通的V2ray服务器，没有伪装，也不是VLESS
- **VMESS**+KCP，传输协议使用mKCP，VPS线路不好时可能有奇效
- **VMESS**+TCP+TLS，带伪装的V2ray，不能过[CDN中转](https://v2xtls.org/v2ray使用cloudflare中转流量，拯救被墙ip/)
- **VMESS**+WS+TLS，即最通用的V2ray伪装方式，能过[CDN中转](https://v2xtls.org/v2ray使用cloudflare中转流量，拯救被墙ip/)，推荐使用
- **VLESS**+KCP，传输协议使用mKCP
- **VLESS**+TCP+TLS，通用的VLESS版本，不能过[CDN中转](https://v2xtls.org/v2ray使用cloudflare中转流量，拯救被墙ip/)，但比VMESS+TCP+TLS方式性能更好
- **VLESS**+WS+TLS，基于websocket的V2ray伪装VLESS版本，能过[CDN中转](https://v2xtls.org/v2ray使用cloudflare中转流量，拯救被墙ip/)，有过CDN情况下推荐使用
- **VLESS**+TCP+XTLS，目前最强悍的VLESS+XTLS组合，强力推荐使用（但是支持的客户端少一些）
- **trojan**，轻量级的伪装协议
- **trojan**+XTLS，trojan加强版，使用XTLS技术提升性能

> 注意：目前一些客户端不支持VLESS协议，或者不支持XTLS，请按照自己的情况选择组合

\5. 按照自己的需求选择一个方式。例如6，然后回车。接着脚本会让你输入一些信息，也可以直接按回车使用默认值。需要注意的是，对于要输入伪装域名的情况，**如果服务器上有网站在运行**，请联系运维再执行脚本，否则可能导致原来网站无法访问！

[![xray一键脚本输入](https://v2xtls.org/wp-content/uploads/2020/12/xray%E4%B8%80%E9%94%AE%E8%84%9A%E6%9C%AC%E8%BE%93%E5%85%A5-1024x792-1.jpg)](https://v2xtls.org/wp-content/uploads/2020/12/xray一键脚本输入-1024x792-1.jpg)

xray一键脚本输入

\6. 脚本接下来会自动运行，一切顺利的话结束后会输出配置信息：

[![Xray一键脚本运行成功输出信息](https://v2xtls.org/wp-content/uploads/2020/12/Xray%E4%B8%80%E9%94%AE%E8%84%9A%E6%9C%AC%E8%BF%90%E8%A1%8C%E6%88%90%E5%8A%9F%E8%BE%93%E5%87%BA%E4%BF%A1%E6%81%AF.jpg)](https://v2xtls.org/wp-content/uploads/2020/12/Xray一键脚本运行成功输出信息.jpg)

Xray一键脚本运行成功输出信息

**到此服务端配置完毕**，服务器可能会自动重启（**没提示重启则不需要**），windows终端出现“disconnected”，mac出现“closed by remote host”说明服务器成功重启了。

对于VLESS协议、VMESS+WS+TLS的组合，网页上输入伪装域名，**能正常打开伪装站**，说明服务端已经正确配置好。如果运行过程中出现问题，请在本页面下方查找解决方法或留言。

## Xray一键脚本其他事项

服务端配置好后，如果想使用CloudFlare等CDN中转（必须是WS版才可以），请参考：[使用cloudflare中转流量，拯救被墙ip](https://v2xtls.org/v2ray使用cloudflare中转流量，拯救被墙ip/)。

本脚本默认使用的加速技术是BBR，换成魔改BBR/BBR Plus/锐速清参考：[安装魔改BBR/BBR](https://v2xtls.org/安装魔改bbr-bbr-plus-锐速lotserver/)[ Plus/锐速(](https://v2xtls.org/安装魔改bbr-bbr-plus-锐速lotserver/)[Lotserver)](https://v2xtls.org/安装魔改bbr-bbr-plus-锐速lotserver/)。

如果伪装站类型没有你满意的，比如你想搭建WordPress博客，请参考：[V2ray伪装建站教程](https://v2xtls.org/v2ray伪装建站教程/)。

对于使用TLS的方式，脚本默认会申请域名证书，证书存放在和xray配置文件同一个文件夹内（即`/usr/local/etc/xray`目录下）。证书会自动更新，如果客户端突然无法使用，请打开伪装网站查看是否能正常打开。如果证书已过期，请再次运行上面的脚本重新配置。

最后，刚搭建好Xray后不要猛上流量，否则会导致被限速、端口被墙，严重可能导致ip被墙。

接下来是配置客户端，下载客户端和配置教程请参考：

- [V2ray Windows客户端下载](https://v2xtls.org/v2ray-windows客户端下载/)
- [V2ray 安卓客户端下载](https://v2xtls.org/v2ray安卓客户端下载/)
- [V2ray Mac客户端下载](https://v2xtls.org/v2ray-mac客户端下载/)
- [V2ray苹果客户端下载](https://v2xtls.org/v2ray-ios客户端下载/)

祝大家使用愉快。如有问题请在页面下方留言，也欢迎到 [网络跳越论坛](https://hijk.club/) 或 tg群组https://t.me/hijkclub 交流，或关注Youtube频道：[网络跳越](https://youtube.com/channel/UCYTB--VsObzepVJtc9yvUxQ)。

## 参考

1. [V2ray一键脚本](https://v2xtls.org/v2ray多合一脚本，支持vmesswebsockettlsnginx、vlesstcpxtls、vlesstcptls等组合/)
2. [V2ray带伪装一键脚本](https://v2xtls.org/v2ray带伪装一键脚本/)
3. [V2ray的VLESS协议介绍和使用教程](https://v2xtls.org/v2ray的vless协议介绍和使用教程/)
4. [VLESS协议的fallback参数详解](https://v2xtls.org/vless协议的fallback参数介绍/)



港大 

港科

理工

城大