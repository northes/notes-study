在官方包 `sync.Once` 中使用到


```go
type Once struct {
	// done indicates whether the action has been performed.
	// It is first in the struct because it is used in the hot path.
	// The hot path is inlined at every call site.
	// Placing done first allows more compact instructions on some architectures (amd64/386),
	// and fewer instructions (to calculate offset) on other architectures.
	done uint32
	m    Mutex
}
```


简单解释下这句话：
1. 热路径(hot path)是程序非常频繁执行的一系列指令，sync.Once 绝大部分场景都会访问 o.done，在热路径上是比较好理解的，如果 hot path 编译后的机器码指令更少，更直接，必然是能够提升性能的。
2. 为什么放在第一个字段就能够减少指令呢？因为结构体第一个字段的地址和结构体的指针是相同的，如果是第一个字段，直接对结构体的指针解引用即可。如果是其他的字段，除了结构体指针外，还需要计算与第一个值的偏移(calculate offset)。在机器码中，偏移量是随指令传递的附加值，CPU 需要做一次偏移值与指针的加法运算，才能获取要访问的值的地址。因为，访问第一个字段的机器代码更紧凑，速度更快。

## 参考
- [go - What does "hot path" mean in the context of sync.Once? - Stack Overflow](https://stackoverflow.com/questions/59174176/what-does-hot-path-mean-in-the-context-of-sync-once)