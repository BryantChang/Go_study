# Go面向接口编程

## 接口的定义

- 强类型系统---编译时需要绑定类型

## duck typing

- 描述事物的外部行为而非内部的结构
- go为结构化类型系统，类似duck typing(严格的动态绑定)

### 不同语言对duck typing的支持

- python--运行时才知道是否有get

```python
def download(retriever):
    return retriever.get("www.imooc.com")
```

- c++--编译时知道

```c++
template<class R>
string download(const &R retriever) {
    return retriever.get("www.imooc.com")
}
```

- java---类似duck typing
- 无法同时继承多个接口
- 不是duck typing

```java

String <R extends Retriever> download(R r) {
    return r.get("www.imooc.com")
}
```

### Go语言的duck typing

- 接口由使用者定义
- 接口组装
- 具有灵活性
- 类型检查

### 举例

- 设定一个Retriever接口，拥有一个Get方法，能够根据url获取到对应的内容(为了简化，将所有的类型定义写到一个文件中)

```go
package main

type Retriever interface{
  Get(url string) string
}

//定义WebRetriever
type WebRetriever struct {
  UserAgent string
  Timeout time.Duration
}

//获得Retriever的能力
func (r *Retriever) Get(url string) string {
  resp, err := http.Get(url)
    if err != nil {
        panic(err)
    }
    result, err := httputil.DumpResponse(resp, true)
    resp.Body.Close()
    if err != nil {
        panic(err)
    }
    return string(result)
}

//定义另一个MockRetriever
type MockRetriever struct {
  Contents string
}

func (r *MockRetriver) Get(url string) string {
  return r.Contents
}

func main() {
  var r Retriever
  retriever = MockRetriever{Contents:"this is a fack imooc.com"}
  r = &retriever
  r = ℜ.Retriever{
        UserAgent: "Chrome",
        Timeout:   time.Minute,
    }
    inspect(r)

    //Type assertion
    if mockRetriever, ok := r.(*mock.Retriever); ok {
        fmt.Println(mockRetriever.Contents)
    } else {
        fmt.Println("not a mock retriever")
    }
}

func inspect(r Retriever) {
    fmt.Println("Inspecting", r)
    fmt.Printf(" > %T %v\n", r, r)
    fmt.Print(" > Type switch:")
    switch v := r.(type) {
    case *mock.Retriever:
        fmt.Println("Contents:", v.Contents)
    case *real.Retriever:
        fmt.Println("UserAgent:", v.UserAgent)
    }
    fmt.Println()
}
```

- 接口由使用者定义，实现是隐式的，不需要显示指定实现某一个接口
- interface{} 代表任何类型
- 接口的组合(使用者定义)

```go
type xxx interface {
  interface1
  interface2
}
```
