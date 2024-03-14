## 官网

[Svelte • Cybernetically enhanced web apps](https://svelte.dev/)

[Svelte 中文文档 | Svelte 中文网](https://www.svelte.cn/)

[SvelteKit • Web development, streamlined](https://kit.svelte.dev/)

## 生态官网

- [SvelteLab](https://www.sveltelab.dev/)
- [Advent of Svelte](https://advent.sveltesociety.dev/)
- [Discord](https://discord.com/channels/457912077277855764/1179937338751725659)
- [Home - Svelte Society](https://sveltesociety.dev/)

## JetBrains 集成

安装 `Svelte` 插件

## 创建项目

### 方式 0

使用 `sveltekit` 框架创建

[SvelteKit](../SvelteKit/SvelteKit.md#创建)

### 方式 1

```bash
npm init vite@latest
# 选择 svelte 选项
```

### 方式 2

> 从 Github 中拉取模板，模板已不再维护，推荐使用创建项目 1

```bash
npx degit sveltejs/template my-svelte-project
npm install
```



### 修改端口与地址

```js
  "scripts": {
	...
    "start": "sirv public --no-clear --port 9898 --host 0.0.0.0"
  },
```

## 部署

```bash
npm run build
```

直接部署整个 public 目录

## 精彩项目

- [GitHub - rocketlaunchr/awesome-svelte: Awesome Svelte: Useful resources for developing Svelte applications](https://github.com/rocketlaunchr/awesome-svelte)

类Svelte编译器实现
- [GitHub - malinajs/malinajs: Frontend compiler, inspired by Svelte](https://github.com/malinajs/malinajs)

## 格式化

配置：[Prettier](../Prettier/Prettier.md)

[GitHub - sveltejs/prettier-plugin-svelte: Format your svelte components using prettier.](https://github.com/sveltejs/prettier-plugin-svelte)

```bash
npm i --save-dev prettier-plugin-svelte prettier
```

```
// .prettierrc
{
    // ..
    "plugins": ["prettier-plugin-svelte"],
    "pluginSearchDirs": ["."], // should be removed in v3
    "overrides": [{ "files": "*.svelte", "options": { "parser": "svelte" } }]
}
```

使用命令行格式化

```bash
npx prettier --write .
```

作为 `package.json` 中脚本的一部分

```json
// package.json
{
    // ..
    "scripts": {
        "format": "prettier --write .", // v3
        "format": "prettier --write  --plugin prettier-plugin-svelte ." // v2
    }
}
```

### 与 Tailwindcss 结合使用

安装 `prettier-plugin-tailwindcss` 

[GitHub - tailwindlabs/prettier-plugin-tailwindcss: A Prettier plugin for Tailwind CSS that automatically sorts classes based on our recommended class order.](https://github.com/tailwindlabs/prettier-plugin-tailwindcss)

修改配置

```
// .prettierrc
{
    // ..
    "plugins": [
        "prettier-plugin-svelte",
        "prettier-plugin-tailwindcss" // MUST come last 必须放在最后
    ]
}
```

修改 `vscode` 配置，告诉 Prettier 扩展处理 svelte 文件（需要在 vscode 安装 prettier 插件）

```json
// settings.json
{
    // ..
    "prettier.documentSelectors": ["**/*.svelte"]
}
```