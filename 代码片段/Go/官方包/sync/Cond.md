`sync.Cond` 基于互斥锁\\读写锁，二者的区别是：
1. 互斥锁 `sync.Mutex` 通常用于保护临界区和共享资源
2. 条件变量 `sync.Cond` 用来协调想要访问共享资源的 goroutine


## 参考

- [go - How to correctly use sync.Cond? - Stack Overflow](https://stackoverflow.com/questions/36857167/how-to-correctly-use-sync-cond)