[![Build Status][travis-image]][travis-link]
# Rust 简例

## 什么 Gui？

这是 [Rust 简例][website] 的源代码！

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

### Generating the `SUMMARY.md`

`SUMMARY.md` 是通过 [examples/structure.json][structure] 生成的。这个 JSON
文件包含了一个例子们的类树形结构。

每个例子包含：

* ID，如 `hello`
* 标题，如 `Hello World`
* 子节点，该项为可选项，包含了其子节点，如 `null`
* 一个在 `examples` 目录下的子目录，如 [examples/hello][hello-folder]
* 一个在 examples/structure.json 里面的入口点，如 `{ "id": "hello", "title":
    "Hello World", "children": null }`
* an entry in examples/structure.json, e.g.
  * some source file(s), e.g. [examples/hello/hello.rs][hello-rs]
* an input markdown file, e.g.
  [examples/hello/input.md][hello-md]

When dealing with a child example, the path will have to include the id of its
ancestors; e.g. `examples/variable/mut/input.md`, implies that a `mut` example
lives under the `variable` example.

### Processing `input.md`

Instead of including the rust code directly in `input.md`, the code lives in
separate source files; and the preprocessing step will insert the source code
in the markdown file.

For example, to insert the source code of the `hello.rs` file, the following
syntax is used in the markdown file:

* `{hello.play}` expands the source code embedded in a live code editor
* `{hello.rs}` expands to static/plain source code.
* `{hello.out}` expands to the output of executing the source code.

The Makefile provides the following recipes:

* `make`: builds `update.rs` and does the preprocessing step
* `make book`: runs `gitbook` to generate the book
* `make serve`: runs `gitbook --serve` to generate the book and publishes it
  under `localhost:4000`
* `make test`: will check all the rust source files for compilation errors

## License

Rust by example is dual licensed under the Apache 2.0 license and the MIT
license.

See LICENSE-APACHE and LICENSE-MIT for more details.

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

