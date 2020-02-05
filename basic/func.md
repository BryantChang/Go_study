# Go语言基础语法--函数
* go语言函数是一等公民
    * 参数
    * 返回值
    * 变量

## 基本定义
```go
func eval（a, b int） int
//多返回值
func div(a, b int)(q, r int)
```

## 举例--多返回值

```go
package main

import "fmt"

func div(a, b int)(int, int) {
    return a/b, a%b
}

func main(){
    q, r := div(10, 3)
    fmt.Printf("q is %d, r is %d", q, r)
}
```

## 举例--函数作为参数传递

```go
package main
import "fmt"

func apply(op func(int, int) int, a, b int) int {
    p := reflect.ValueOf(op).Pointer()
	opName := runtime.FuncForPC(p).Name()
	fmt.Printf("calling function %s with args (%d, %d)\n", opName, a, b)
	return op(a, b)
}

func main() {
    fmt.Println(apply(
		func(a int, b int) int {
			return int(math.Pow(float64(a), float64(b)))
		}, 3, 5))
}
```

## 举例--多个参数

```go
package main

func sum(s ...int) int {
   ret := 0
	for m := range s {
		ret += m
	}
	return ret
}

func main() {
   fmt.Println("sum is:", sum(1, 2, 3, 4, 5, 6, 7, 8, 9, 10))
}
```
