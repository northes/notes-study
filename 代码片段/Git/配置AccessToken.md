生成 access token  
  
添加全局配置

```shell  
git config --global url."https://{{username}}:{{access_token}}@gitlab.examile.com".insteadOf "https://gitlab.example.com"

git config --global url."ssh://git@gitlab.example.com".insteadOf "gitlab.example.com"
```  
  
或者直接添加
  
`~/.gitconfig`

```ini
[url "https://${user}:${personal_access_token}@gitlab.example.com"]  
   insteadOf = https://gitlab.example.com
[url "ssh://git@gitlab.example.com"]  
   insteadOf = gitlab.example.com  
```  
  