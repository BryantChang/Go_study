# Go基础语法--变量与常量
## 变量定义

### 变量定义
```go
package main
var (
	aa = 3
	bb = "kkk"
	ss = true
)
func main() {
   var a int
	var s string
	fmt.Printf("%d %q\n", a, s)
}
```

### :=
* 声明+赋初值

```go
package main

func main() {
    s1 := 1
    var s2 int  //两种等价
    s2=1
}
```
* 只能在函数内使用，无法在包内使用

## go语言内建变量
* rune: int32--字符型
* float32,float64

## 常量与枚举

```go
package main
func main() {
    const (
		cpp = iota//itoa 自增量
		java
		python
		golane
	)
	fmt.Println(cpp, java, python)
}
```
