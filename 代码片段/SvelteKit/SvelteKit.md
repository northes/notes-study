## 创建

```bash
npm create svelte@latest my-app
cd myapp
npm install
npm run dev
```

## 学习

- [Introduction / Welcome to Svelte • Svelte Tutorial](https://learn.svelte.dev/tutorial/welcome-to-svelte)

## 路由

`+page.svelte` 表示一个新的页面

`src/routers/+page.svelte` 对应的路由为 `/`
`src/routers/about/+page.svelte` 对应的路由为 `/about`
`src/routers/blog/[slug]/+page.svelte` 对应的路由为 `/blog/1` 或 `/blog/x` 等


## Cookie

`+page.server.js`

```js
export function load({cookies}) {
    const visited = cookies.get('visited');

    cookies.set('visited', 'true', {page: '/'});

    return {
        visited
    };
}
```

框架使用的包 [GitHub - jshttp/cookie: HTTP server cookie parsing and serialization](https://github.com/jshttp/cookie#api)


## lib

通用的组件可以放在 `/src/lib` 目录下，可以通过 `$lib/xxx` 进行引用

```html
<script>
	import {message} from "$lib/message.js";
</script>
```


## +page.ts

### load

```ts
export const load = (async ( {params} ) => {
	// ...
	
	return {
		key: value,
		key2: value2
	}
})
```

可传参数
- url
```ts
  url: URL {
    href: 'http://localhost:5173/custom',
    origin: 'http://localhost:5173',
    protocol: 'http:',
    username: '',
    password: '',
    host: 'localhost:5173',
    hostname: 'localhost',
    port: '5173',
    pathname: '/custom',
    search: '',
    searchParams: URLSearchParams {},
    hash: ''
  },
```
- params：路由参数
- data：从上n层 load 方法传下来的数据
- route：路由信息
- fetch：执行调用
- setHeaders
- depends
- parent


## Stores

### page

`import {page} from '$app/stores'`

- url：当前页面的URL
- params：当前页面的参数
- route：表示当前路由的 `id` 属性的对象
- status：当前页面的HTTP状态码
- error：当前页面的错误对象
- data：当前页面的数据，合并所有`load`函数的返回值
- form：表单操作返回的数据

可以通过 `$page` 快速访问


### navigating

`import {navigating} from '$app/stores'`

- from：具有 `param` `route` `url` 属性的对象
- to：同 `from`
- type：导航类型，`link` 、 `popstate` 、`goto`