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
