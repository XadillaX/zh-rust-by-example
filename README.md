[![Build Status][travis-image]][travis-link]
# Rust 简例

## 什么 Gui？

这是 [Rust 简例][website]的源代码！

## 如何贡献？

参照 [CONTRIBUTING.md][how-to-contribute]。

## 如何生成静态页？

```
make all
make book
make test
```

输入 `make serve` 来查看结果。

注意：在 Ubuntu 里 `node` 可能叫 `nodejs`。我不得不相应地修改 `.bin/gitbook`。

### 详细说明

我们使用下面的工具来生成这个静态站：

* [Rust][rust-lang] (ﾉ◕ヮ◕)ﾉ\*:･ﾟ✧
* [gitbook][gitbook]

`gitbook` 会从 Markdown 文件中生成页面（[点我](gitbook-format)看看它是怎么工作的）。

在跑 `gitbook` 之前我们需要用 [src/update.rs][update-rs] 来做一些前置工作。

这个工作包含两步：

### 生成 `SUMMARY.md`

`SUMMARY.md` 是通过 [examples/structure.json][structure] 生成的。这个 JSON
文件包含了一个例子们的类树形结构。

每个例子包含：

* ID，如 `hello`
* 标题，如 `Hello World`
* 子节点，该项为可选项，包含了其子节点，如 `null`
* 一个在 `examples` 目录下的子目录，如 [examples/hello][hello-folder]
* 一个在 examples/structure.json 里面的入口点，如 `{ "id": "hello", "title":
    "Hello World", "children": null }`
  * 一些源文件，如 [examples/hello/hello.rs][hello-rs]
* 一个输入 Markdown 文件，如 [examples/hello/input.md][hello-md]

When dealing with a child example, the path will have to include the id of its
ancestors; e.g. `examples/variable/mut/input.md`, implies that a `mut` example
lives under the `variable` example.

### 处理 `input.md`

Rust 的代码我们不直接放在 `input.md` 里面，而是放在另外的源文件里面；然后前置工作会把源代码插入到
markdown 文件里面。

举个栗子，为了插入 `hello.rs`，我们会在 markdown 文件里面添加如下的标记：

* `{hello.play}` 会把代码嵌入到一个在线编辑框里面。
* `{hello.rs}` 会放到静态文本里面。
* `{hello.out}` 会放这个程序的输出结果。

Makefile 提供了以下指令：

* `make`: 构建 `update.rs` 然后执行上述前置工作
* `make book`: 执行 `gitbook` 来生成 book
* `make serve`: 执行 `gitbook --serve` 来生成 book 然后以 `localhost:4000` 预览
* `make test`: 会测试所有的 Rust 源文件是否有编译错误

## License

Rust 简例包含了两种协议——Apache 2.0 以及 MIT 协议。请阅读该两种协议的详细内容。

[travis-image]: https://travis-ci.org/rust-lang/rust-by-example.svg?branch=master
[travis-link]: https://travis-ci.org/rust-lang/rust-by-example
[website]: http://rustbyexample.com
[how-to-contribute]: CONTRIBUTING.md
[rust-lang]: http://www.rust-lang.org/
[gitbook]: http://www.gitbook.io
[gitbook-dir]: https://github.com/GitbookIO/gitbook#book-format
[update-rs]: src/update.rs
[structure]: examples/structure.json
[hello-folder]: examples/hello
[hello-rs]: examples/hello/hello.rs
[hello-md]: examples/hello/input.md

