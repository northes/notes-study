```bash
cat ~/.ssh/id_rsa.pub | ssh remote_username@server_ip_address "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"

cat ~/.ssh/id_rsa.pub | ssh root@192.168.31.40 "mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```

修改配置文件

`/etc/ssh/sshd_config`

```
RSAAuthentication yes 开启RSA验证  
PubkeyAuthentication yes 是否使用公钥验证  
AuthorizedKeysFile .ssh/authorized_keys 公钥的保存位置  
PasswordAuthentication no 禁止使用密码验证登录
```