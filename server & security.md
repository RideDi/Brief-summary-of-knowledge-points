## PHP

### PHP 8大魔术常量

- \__CLASS__
- \__NAMESPACE__
- \__FUNCTION__
- \__LINE__
- \__DIR__
- \__TRAIT__
- \__FILE__
- \__METHOD__

### PHP高危函数

这些函数都能够执行外部程序！

- shell_exec
- system
- passthru
- Exec()
- Chroot()
- Chown()
- Chgrp()
- ini_set()
- Putenv()
- ……

## Apache

### Apache文件解析漏洞

- 多后缀名
  - apache允许一个文件有多个后缀text.txt.rar.igp.mp3，在zpache中会从右向左辨别后缀
- 罕见后缀名
  - Php3，php4……
- .htaccess(分布式配置文件)一种方便的、可作用于当前目录及子目录的配置文件

## Nginx

Nginx是一款轻量级的**Web服务器**/反向代理服务器及电子邮件（IMAP/POP3）代理服务器，并在一个BSD-like协议下发行。其特点是占有内存少，并发能力强，事实上nginx的并发能力确实在同类型的网页服务器中表现较好。

Nginx 相对于 Apache 优点：

     1) 高并发响应性能非常好，官方 Nginx 处理静态文件并发 5w/s 
     2) 反向代理性能非常强。（可用于负载均衡） 
     3) 内存和 cpu 占用率低。（为 Apache 的 1/5-1/10） 
     4) 对后端服务有健康检查功能。 
      5) 支持 PHP cgi 方式和 fastcgi 方式。 
     6) 配置代码简洁且容易上手。 
## IIS

### IIS解析漏洞

可能被IIS当做asp程序执行的后缀有：
.asp
.cer
.asa
.cdx

#### IIS6.0在解析文件时存在两个解析漏洞

- 目录解析
  - 以*.asp命名的文件夹里的文件都会被当作ASP文件执行
- 文件解析
  - *.asp;.jpg这种畸形文件名在 **;** 后面的会被忽略，会被当作asp执行

#### iis 7.x

##### ***iis+php***

利用：IIS7/7.5在Fast-CGI运行模式下,在一个文件路径(/xx.jpg)后面加上/xx.php会将/xx.jpg/xx.php 解析为 php 文件。

### IIS容器中还有一个经典漏洞WebDav

WebDav是一种基于HTTP1.1协议的通信协议，它扩展了HTTP协议，在GET、POST、HEAD等几个HTTP标准方法以外添加了一些新的方法，使HTTP协议更强大。在开启WebDav扩展的服务器之后，如果支持PUT、MOVE、COPY、DELETE等方法，就可能会存在一些安全隐患。攻击者就可能通过PUT方法向服务器上传危险脚本文件。

第一步：通过OPTIONS探测服务器所支持的HTTP方法

第二步：通过PUT方法向服务器上传脚本文件

第三步：通过MOVE或COPY方法改名

通过这三个步骤，攻击者就能轻松的获取一个WebShell

如果服务器开启了DELETE方法，攻击者还可以删除服务器上的任意文件。

IIS6.0中，如果开启了WebDAV，没有开启脚本资源访问权限的话，不能通过MOVE来讲Put上去的txt文件变成asp文件

虽然没开脚本资源访问权限，但是可以通过move改成后缀为txt的文件名。配合文件解析漏洞可getshell。

## Redis

### Redis未授权访问漏洞

Redis 默认情况下，会绑定在 **0.0.0.0:6379**，如果没有进行采用相关的策略，比如添加防火墙规则避免其他非信任来源 ip 访问等，这样将会将 Redis 服务暴露到公网上，如果在没有设置密码认证（一般为空）的情况下，会导致任意用户在可以访问目标服务器的情况下未授权访问 Redis 以及读取 Redis 的数据。攻击者在未授权访问 Redis 的情况下，利用 Redis 自身的提供的config 命令，可以进行写文件操作，攻击者可以成功将自己的ssh公钥写入目标服务器的 /root/.ssh 文件夹的authotrized_keys 文件中，进而可以使用对应私钥直接使用ssh服务登录目标服务器。



简单说，漏洞的产生条件有以下两点：

```
（1）redis绑定在 0.0.0.0:6379，且没有进行添加防火墙规则避免其他非信任来源ip访问等相关安全策略，直接暴露在公网；
（2）没有设置密码认证（一般为空），可以免密码远程登录redis服务。 
```

危害：

```
（1）攻击者无需认证访问到内部数据，可能导致敏感信息泄露，黑客也可以恶意执行flushall来清空所有数据；
（2）攻击者可通过EVAL执行lua代码，或通过数据备份功能往磁盘写入后门文件；
（3）最严重的情况，如果Redis以root身份运行，黑客可以给root账户写入SSH公钥文件，直接通过SSH登录受害服务器
```

```
Redis未设置密码可导致未授权访问漏洞
使用root账号启用Redis服务，可能导致反弹ssh shell
Redis默认开放端口是6379
```

