# 使用Firekylin快速搭建博客 【ThinkJS+React+Node.js】
## 1 登录云服务器ECS

```
ssh root@1.1.1.1
```

输入实例密码
## 2 设置服务器用户
### 2.1 新增用户
```
adduser username
```
### 2.2 设置用户密码
```
sudo passwd username
```

<!--more-->
### 2.3 为用户添加和root一样的权限
```
visudo
```
找到
```
root ALL=(ALL)		ALL
```
添加
```
username ALL=(ALL) 	ALL
```
问题：如果中间出错要删除用户可用：
```
userdel username
```
然后使用rm -rf foldername命令手动删除两个目录
```
/home/username
```
和
```
/var/spool/mail/username
```

使用 ssh username@ip登录服务器

### 2.4 禁止root登陆
```
vi /etc/ssh/sshd_config
```
将PermitRootLogin的值改成yes，并保存
然后运行命令
```
service sshd restart
```
这样，就不能用root直接ssh登录了

## 3 更新环境
这个时候最好更新下系统的各种包和资源

```
yum -y update
```

这是阿里云推荐的更新方式，你也可以试试其他的，不过速度方面应该会差些。 yum是一个在Redora和RedHat以及SUSE中的shell前端软件包管理器，基于RPM包管理器。这里说明下参数的意思:
* -y（当安装过程提示选择全部为"yes"）
* update: 安装所有更新软件

## 4 安装nodejs
下载

```
wget http://nodejs.org/dist/node-latest.tar.gz
```

解压

```
tar zxf node-latest.tar.gz
```

预编译处理

```
./configure
```

如果提示需要安装g++，在运行一下命令

```
sudo yum install gcc-c++
```

编译

```
make
```

执行了以上的步骤，编译的时间比较久，然后开始安装

```
make install
```

然后测试一下

```
node -v
```

## 5 开启测试服务器
直接写一个监听脚本作为demo测试

```
vi app.js
```

简单的服务器脚本app.js：

```
var http = require('http');http.createServer(function(req,res){    res.writeHead(200,{'Content-Type':'text/plain'});    res.end('Hello body!');}).listen(80,'127.0.0.1');console.log('NodeJS Server sunning at http://127.0.0.1:80');
```

然后启动服务器：

```
node app.js
```

如果提示sudo：node：找不到命令
则执行以下命令

```
sudo ln -s /usr/local/bin/node /usr/bin/node
sudo ln -s /usr/local/lib/node /usr/lib/node
sudo ln -s /usr/local/bin/npm /usr/bin/npm
sudo ln -s /usr/local/bin/node-waf /usr/bin/node-waf
```


## 6 打开80端口
1. 登录阿里云的管理控制台。找到那台云服务器；

2. 在操作的部分点击“更多”，里面藏着一个“安全组配置”；
￼
3. 进入“安全组配置”后，点击“配置规则”；
￼
4. 然后点击“公网入方向”。默认里面有22和3389端口是打开的；
￼
5. 点击右上角的“添加安全组规则”；
￼
6. 在“添加安全组规则”的对话框里面，添加“端口范围”为“80/80”，添加“授权对象”为“0.0.0.0/0”，再点击“确定”按钮。
￼
这样在访问服务器IP，网站就正常显示了。

## 7 安装Nginx
假设当前目录为/server/download/nginx/

下载nginx openssl,pcre,zlib

```
wget http://nginx.org/download/nginx-1.12.0.tar.gz
wget https://www.openssl.org/source/openssl-1.1.0e.tar.gz
wget https://ftp.pcre.org/pub/pcre/pcre-8.37.tar.gz
wget http://prdownloads.sourceforge.net/libpng/zlib-1.2.11.tar.gz?download
```

解压nginx openssl,pcre,zlib

```
tar -zxvf nginx-1.12.0.tar.gz
tar -zxvf openssl-1.1.0e.tar.gz
tar -zxvf pcre-8.37.tar.gz
tar -zxvf zlib-1.2.11.tar.gz?download
```
进入源码目录
```
cd openssl-1.1.0e
```
配置
```
./config --prefix=/server/download/nginx/openssl --openssldir=/server/download/nginx/openssl/conf
```
编译安装
```
make && make install
```
检验安装(如果报错是文件路径不对的问题为下面两个文件设置软连接)

```
ln -s /server/download/nginx/openssl/bin/libssl.so.1.1 /usr/lib64/libssl.so.1.1
ln -s /server/download/nginx/openssl/bin/libcrypto.so.1.1 /usr/lib64/libcrypto.so.1.1 /server/download/nginx/openssl/bin/openssl version -a
```
 
进入源码目录

```
cd pcre-8.37

```

安装C ++编译器

```
yum install -y gcc gcc-c++
```
执行配置

```
./configure --prefix=/server/download/nginx/pcre/
```

编译安装

```
make && make install
```

进入源码目录

```
cd zlib-1.2.11
```

配置

```
./configure --prefix=/server/download/nginx/zlib/
```

编译安装

```
make && make install
```
 
 
进入安装目录
```
cd nginx-1.12.0
```
 
配置(使用openssl、pcre、zlib的源码路径)
```
./configure --user=www --group=www --prefix=/server/service/nginx --with-http_ssl_module --with-openssl=/server/download/nginx/openssl-1.1.0e --with-pcre=/server/download/nginx/pcre-8.37 --with-zlib=/server/download/nginx/zlib-1.2.11 --with-http_stub_status_module --with-threads
```
编译安装

```
make && make install
```
 
验证

```
nginx -V
```
添加用户跟用户组
```
/usr/sbin/groupadd -f www/usr/sbin/useradd -g www www
```
 
启动

```
/server/service/nginx/sbin/nginx -c /server/service/nginx/conf/nginx.conf
./nginx -s reload
```

查询nginx主进程号
```
ps -ef | grep nginx
```
停止进程 
```
kill -9 nginx
```
参考文档
- https://github.com/firekylin/firekylin
- 谷歌百度
