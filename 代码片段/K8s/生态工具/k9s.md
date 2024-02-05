## 官网

[K9s - Manage Your Kubernetes Clusters In Style](https://k9scli.io/)

## 快捷键

上下左右移动、页首页尾移动同 `vim` ，支持方向键

输入时可使用 `Tab` 快速完成

| 快捷键|功能 |
| --- | --- |
| ? | 帮助文档 |
|ctrl-a|展示所有资源及其别名|
|:q、ctrl-c|退出|
|:po、:svc|展示指定类型的资源|
|:po ns-name|展示指定namespace下的指定类型资源|
|:po /fred|展示指定类型资源并筛选名称|
|:po app=fred,env=dev|展示指定类型资源并筛选labels|
|:po @ctx1|切换context并展示资源|
|/filter|过滤名称|
|/!filter|排除过滤名称|
|/-l label-selector|过滤拥有指定label的资源|
|/-f filter|模糊查找给定的过滤器|
|\<ecs\>|退出当前页面|
|:ctx|展示上下文|
|:xray RESOURCE \[NAMESPACE\] |扫描资源并展示树状结构|
|:popeye or :pop|popeye 视图|
|:pulses or :pu|pulses 视图|
|ctrl+b|向上翻页|
|ctrl+f|向下翻页|