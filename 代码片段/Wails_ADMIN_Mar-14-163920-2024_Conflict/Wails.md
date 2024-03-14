## CLI

```bash
## 安装
go install github.com/wailsapp/wails/v2/cmd/wails@latest
## 版本
wails version
## 检查
wails doctor
```

## 创建项目

```bash
wails init -n myproject -t svelte
```

## 生成方法

```bash
wails generate module
```

通常生成的方法位于 `frontend/wailsjs/go/` 下，通过

```js
import {Greet} from '../wailsjs/go/main/App.js'
  
Greet(name).then(result => resultText = result)
```

引入并调用