# Go语言基础语法--基本数据结构

## 数组

- 数组是值类型，需要提前定义好大小

### 举例--定义和使用

```go
package main
import "fmt"

func main() {
    var arr1 [5]int
    arr2 := [3]int{1,3,4,5,6}
    arr3 := [...]int{2,4,5,6,7}
    for i,v := range arr2 {
        fmt.Println(i, v)
    }
}
```

## 切片(Slice)

- 切片是数组的视图，本身是没有数据的

```go
var s []int//声明 (s nil)
arr2 := [...]int{1,2,3,4,5,6,7}
slice1 := arr2[2:6] //2-5
slice2 := arr2[:6] //0-5
slice3 := arr2[2:] //2后所有
slice4 := arr2[:] //所有

slice5 := slice2[2:] //reslice
```

- 修改slice，原本的arr会随之修改
- slice会自动扩展，可以向后扩展，不能向前扩展
- s[i] 不能超过len(s) 向后扩展不能超过cap(s)

![-w1155](https://raw.githubusercontent.com/BryantChang/Go_study/master/imgs/slice_example.png)

### slice实现

![-w970](https://raw.githubusercontent.com/BryantChang/Go_study/master/imgs/slice_structure.png)

### slice常用操作

- slice = append(slice, elm)//必须接收返回值

  - 添加元素超过cap(s)会重新分配更大的底层数组
  - 用长度会自动扩展*2

- slice = make([]int, 10, 32) len,cap
- copy(s2, s1)

## Map

### example

```go
package main
import "fmt"

func main() {

    m := map[string]string{
        "name":    "ccmouse",
        "course":  "golang",
        "site":    "imooc",
        "quality": "notabad",
    }

    m2 := make(map[string]int)
   //遍历
   for k, v := range m {
       fmt.Println(k, v)
   }
   //访问
   if courceName,ok := m["course"]; ok {
       fmt.Println(courseName)
   }else {
       fmt.Println("key not exist")
   }
}
```
