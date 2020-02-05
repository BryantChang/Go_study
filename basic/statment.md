# Go语言基础语法--语句
## 条件语句--if
* example

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
* if条件里可以定义变量

## 分支语句
* case后面不需要break
* switch后面可以加表达式

## 循环语句
* 不存在while
* for后面不加括号
* for {} 死循环
