# Go语言函数式编程

## 函数式编程定义

- 函数是一等公民(参数，变量返回值都可以是函数)

- 闭包

- 不可变性

- 只有一个参数

## 闭包

- 局部变量
- 自由变量(描述函数所处的环境)

![-w1155](https://raw.githubusercontent.com/BryantChang/Go_study/master/imgs/closure.png)

- example -- 计算部分和

```go
package main

func adder func(int) int {
  sum := 0
  return func(v int) int {
    sum += v
    return sum
  }
}

func main() {
  a := adder()
  for i := 0; i < 10; i++ {
        fmt.Printf("0+...+%d=%d\n", i, a(i))
  }
}
```

//不使用自由变量的函数编程

```go
package main

type iAdder func(int) (int, iAdder) //递归定义

func adder2(base int) iAdder {
  return func(v int)(int, iAdder) {
    return base + v, adder2(base + v)
  }
}

func main() {
    a := adder2(0)
    for i := 0; i < 10; i++ {
        var s int
        s, a = a(i)
        fmt.Printf("0+...+%d=%d\n", i, s)
    }
}
```

- 示例代码2斐波那契数列生成器(10000以下)

```go
type intGen func() int

// 1, 1, 2, 3, 5, 8, 13
//    a, b
//         a, b
func fibonacci() intGen() {
  a, b := 0, 1
  return func() int {
    a, b = b, a+b
    return a
  }
}

//实现一个io.Reader的方法Read(p []byte) (n int, err error)
func (g intGen) Read(p []byte) (n int, err error) {
  next := g()
  if next > 1000 {
    return 0, io.EOF
  }
  s := fmt.Sprintf("%d\n", next)
  return strings.NewScanner(reader).Read(p)
}

func printFileContents(reader io.Reader) {
  scanner := bufio.NewScanner(reader)
  for scanner.Scan() {
    fmt.Println(scanner.Text())
  }
}

func main() {
  f := fibonacci()
  printFileContents(f)
}
```

```
Printf(),是把格式字符串输出到标准输出（一般是屏幕，可以重定向）。
Printf()是和标准输出文件(stdout)关联的,Fprintf则没有这个限制.
Sprintf(),是把格式字符串输出到指定字符串中，所以参数比printf多一个char*。那就是目标字符串地址。
Fprintf(),是把格式字符串输出到指定文件设备中，所以参数笔printf多一个文件指针FILE*。主要用于文件操作。Fprintf()是格式化输出到一个stream，通常是到文件。
```

- 其他语言实现闭包

- python

```python
def adder():
  sum = 0
  def f(value):
    nonlocal sum
    sum += value
    return sum
  return f
```

- c++

```c++
auto adder() {
  auto sum = 0
  return [=](int value) mutable {
    sum += value
    return sum
  };
}
```

-java

```java
Function<Integer, Integer> adder() {
  final Holder<Integer> sum = new Holder<>(0)
  return (Integer value) -> {
    sum.value += value;
    return sum.value
  }
}
```
