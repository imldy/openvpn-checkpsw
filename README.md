# openvpn-checkpsw
Mathias Sundman大佬的源码，来源http://www.openvpn.se/files/other/

## 使用方法

在`server.conf`中指明`auth-user-pass-verify` 为`checkpsw.sh`的路径

例如

```
auth-user-pass-verify /etc/openvpn/checkpsw.sh via-env
```

