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

- 声明+赋初值

```go
package main

func main() {
    s1 := 1
    var s2 int  //两种等价
    s2=1
}
```

- 只能在函数内使用，无法在包内使用

## go语言内建变量

- rune: int32--字符型
- float32,float64

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

# Go语言基础语法--语句

## 条件语句--if

- example

```go
package main
import (
    "fmt"
    "io/ioutil"
)
func main() {
    const filename = "abc.txt"
    if contents, err := ioutil.ReadFile(filename); err != nil {
        fmt.Println(err)
    } else {
        fmt.Printf("%s\n", contents)
    }
}
```

- if条件里可以定义变量

## 分支语句

- case后面不需要break
- switch后面可以加表达式

## 循环语句

- 不存在while
- for后面不加括号
- for {} 死循环

# Go语言基础语法--函数

- go语言函数是一等公民

  - 参数
  - 返回值
  - 变量

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

# Go语言基础语法--指针

- go只有值传递，没有引用传递(传递前将值拷贝一份再传入)
- go中的指针不能进行运算

  ```go
  package main
  func main() {
    var a = 2
    var pa *int = &a
    *pa = 3
    fmt.Println(a)
  }
  ```

  ## 值传递 & 引用传递

- example

  ```c++
  void pass_by_val(int a) {
  a++;
  }

  void pass_by_ref(int& a) {
  a++;
  }

  int main() {
  int a = 3
  pass_by_val(a)
  std::cout << "After pass_by_val a is" << a << std::endl;
  std::cout << "After pass_by_ref a is" << a << std::endl;

  //结果为3，4
  return 0;
  }
  ```

- 图示举例--传递指针

  ![-w996](https://raw.githubusercontent.com/BryantChang/Go_study/master/imgs/ref_pass_val.png)

  ![-w1062](https://raw.githubusercontent.com/BryantChang/Go_study/master/imgs/pass_obj.png)
