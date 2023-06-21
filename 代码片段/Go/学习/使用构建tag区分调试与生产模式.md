`debug.go`

```go
// +build debug

package main

const debug = true
```

`release.go`

```go
// +build !debug

package main

const debug = false
```

`main.go`

```go
package main

import "log"

func main() {
	if debug {
		log.Println("debug mode is enabled")
	}
}
```

```bash
# debug = true
$ go build -tags debug -o debug .
$ ./debug
2021/01/11 00:10:40 debug mode is enabled


# debug = false
$ go build -o release .
$ ./release
# no output
```
