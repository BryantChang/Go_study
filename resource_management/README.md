# Go语言资源管理与出错处理

## defer调用

- 确保调用在函数结束时发生

- 多个defer会放在类似栈的结构中，函数结束前以"后进先出的方式调用"

- 一般用来释放资源

- 参数在defer语句时计算

### 错误处理

```go
package main

func main {
  file, err := os.Open("abc.txt")
  if err != nil {
    if pathError, ok := err.(*os.PathError); ok {
      fmt.Println(pathError.Err)
    }else {
      fmt.Println("unknown error", err)
    }
  }
}
```
