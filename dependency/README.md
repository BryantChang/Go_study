# Go语言依赖管理

## 依赖管理三个阶段

- GOPATH
- GOVENDER
- GOMODE

### GOPATH

- 默认在~/go
- 所有项目都会放到gopath中
- $GOPATH/src
- go get -u xxxx
- 寻找顺序

  - proj/vender
  - goroot
  - gopath/src

### GOVENDER

- 在每个proj下添加vender目录

### Go Moudule

- gopath/pkg/mod
- go build ./...
