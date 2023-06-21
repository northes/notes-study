`sync.Cond` 基于互斥锁\\读写锁，二者的区别是：
1. 互斥锁 `sync.Mutex` 通常用于保护临界区和共享资源
2. 条件变量 `sync.Cond` 用来协调想要访问共享资源的 goroutine


```go
var cond = sync.NewCond(&sync.Mutex{})
var done = false

func main() {
	go read("reader1")
	go read("reader2")
	go read("reader3")
	write("writer")

	time.Sleep(time.Second * 3)
}

func read(name string) {
	cond.L.Lock()
	for !done {
		cond.Wait()
	}
	log.Println(name, "starts reading")
	cond.L.Unlock()
}

func write(name string) {
	log.Println("starts writing")
	time.Sleep(time.Second)
	cond.L.Lock()
	done = true
	cond.L.Unlock()
	log.Println(name, "wakes all")
	cond.Broadcast()
}
```

## 参考

- [go - How to correctly use sync.Cond? - Stack Overflow](https://stackoverflow.com/questions/36857167/how-to-correctly-use-sync-cond)