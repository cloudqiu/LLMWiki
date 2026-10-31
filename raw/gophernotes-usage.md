# gophernotes 本地使用笔记

记录日期：2026-10-31。用户已在本地启动 gophernotes；具体安装方式、版本及 Jupyter 前端未核实。

## 运行 Go 代码

在 Jupyter 中新建或打开使用 **Go (gophernotes)** kernel 的 notebook，将下面代码粘贴到代码单元，按 `Shift+Enter` 执行。gophernotes 可直接执行 Go 语句，无须写 `package main` 或 `func main()`。

```go
import "fmt"

a, b := 0, 1
for i := 0; i < 10; i++ {
    fmt.Print(a, " ")
    a, b = b, a+b
}
```

预期输出：`0 1 1 2 3 5 8 13 21 34 `（末尾有一个空格）。此示例尚未在用户的本地环境实际验证。

## 补全

gophernotes 实现了 Jupyter kernel 的 completion 请求，使用 gomacro 的 `CompleteWords` 返回匹配项；补全能力可能有限。先执行 `import "fmt"`，再在新单元输入 `fmt.Pr` 并按 `Tab` 测试。键入时自动出现建议列表与 `Tab` 请求补全是不同功能；前者还取决于 Jupyter 前端与配置。用户本地的补全表现尚未核实。

## 来源

- gophernotes 项目说明与使用文档：https://github.com/gopherdata/gophernotes
- gophernotes 补全实现：https://github.com/gopherdata/gophernotes/blob/master/complete.go
