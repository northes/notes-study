## 参考文档

- [Remote Access API](https://www.jenkins.io/doc/book/using/remote-access-api/)
- [Authenticating scripted clients](https://www.jenkins.io/doc/book/system-administration/authenticating-scripted-clients/)


## 生成令牌

![](assets/Pasted%20image%2020230131175650.png)

## 执行 Job

`POST`

使用 `BASIC 身份验证`

```bash
curl JENKINS_URL/job/JOB_NAME/buildWithParameters \
  --user USER:TOKEN \
  --data id=123 --data verbosity=high
```

```bash
curl http://192.168.31.25:8080/job/xia_test_1/buildWithParameters --user admin:11411e13752b6617ee9a3982e9b000dd5a --data GAME_BRANCH=ci
```

## Q&A

### 请求后报500错误

检查是否是类型为选项的参数中，没有请求的入参。即入参匹配不上选项。

### 通过Body传参不生效

虽然请求方式为POST，但是只能通过Query传参，Body传参不生效