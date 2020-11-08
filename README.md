# openvpn-checkpsw
Mathias Sundman大佬的源码，来源http://www.openvpn.se/files/other/

## 使用方法

### 服务器端

在你的OpenVPN服务器配置文件`server.conf`中指明`auth-user-pass-verify` 为`checkpsw.sh`的路径

例如

```
auth-user-pass-verify /etc/openvpn/checkpsw.sh via-env
client-cert-not-required #表示不请求客户的证书，使用user/pass认证
username-as-common-name #表示客户端认证时候需要用户名
script-security 3 execve #保存密码在环境变量中，如果2时就不能验证密码了,需要使用3。execve代表执行脚本时一般情况下只能使用内置命令，比较安全。
```

在`/etc/openvpn/`目录新建一个文件`psw-file`

内容：

```
username passward
username2 passward2
```

用户名和密码用空格分开，一行一个用户。

给`checkpsw.sh`执行权限，例如`chmod +x checkpsw.sh `

### 客户端

客户端配置文件

```
# 注释掉即可
#cert laptop.crt
#key laptop.key

# 新增验证方式
auth-user-pass
```

重新导入配置文件到软件，连接即可。

参考：

1. [OpenVPN 使用账号+密码方式登陆](https://xu3352.github.io/linux/2017/06/08/openvpn-use-username-and-password-authentication)
2. [openvpn使用账号密码登录](https://my.oschina.net/u/4312735/blog/3615628)
3. [openvpn本地用户名密码验证](https://blog.51cto.com/lvnian/1708851)
4. [[OpenVPN] OpenVPN脚本应用之--简介.](http://chenall.net/post/openvpn_script_pre/)
