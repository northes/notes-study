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


## Sveltekit

创建项目

```bash
wails init -n <app-name> -t svelte
```

删除前端，并安装 `sveltekit`

```bash
rm -rf frontend
npm init svelte@latest forntend
```

修改 `wails` 生成运行时和方法的位置，在 `wails.json` 中添加

```bash
"wailsjsdir": "./frontend/src/lib"
```

在 `main.go` 中修改 `embed` 路径为

```go
// 原来
//go:embed all:frontend/dist

// 修改为
//go:embed all:frontend/build
```

转到 `frontend` 文件夹，卸载自动适配器，安装静态适配器

```bash
npm i
npm uninstall @sveltejs/adapter-auto
npm i -D @sveltejs/adapter-static
```

修改 `svelte.config.js` 为静态适配器

```js
import adapter from '@sveltejs/adapter-static';
```

创建 `frontend/src/routers/+layout.ts`，使用 `SPA` 模式

```js
export const prerender = true
export const ssr = false
```

移除所有 `*.server.ts` 相关的页面和文件

返回项目根目录测试运行

```bash
wails dev
```