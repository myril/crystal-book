# Crystal编程语言

这是crystal编程语言的简介.

Crystal包含以下特性:

* 拥有类似ruby的语法(但目标不是为了兼容ruby).
* 静态类型检测, 但不用给变量和方法参数指定类型.
* 能通过在crystal编写绑定来调用C代码.
* 在编译时评估和生成代码, 以避免重复无用代码.
* 编译为高效的机器码.

## 为完善语言做贡献

你认为自己能帮到忙吗?如果你找到错误或者需要更详细说明的地方,
非常感谢你为crystal做出贡献. 你可以在这个资源提交一个合并请求:
https://github.com/crystal-lang/crystal-book

非常感谢!

### Building and Serving Locally

```
$ git clone https://github.com/crystal-lang/crystal-book.git
$ cd crystal-book
$ npm install -g gitbook-cli@2.3.0
$ npm install
$ gitbook serve
Live reload server started on port: 35729
Press CTRL+C to quit ...

info: 8 plugins are installed
info: loading plugin "ga"... OK
...
Starting server ...
Serving book on http://localhost:4000

```

Html output will be in `_book` folder (some links won't work if opening the files locally).
There is also a docker environment to avoid installing dependencies globally:

```
$ docker-compose up
...
gitbook_1  | Starting server ...
gitbook_1  | Serving book on http://localhost:4000
gitbook_1  | Restart after change in file node_modules/.bin
...
```

### Adding a page

To add a page, create a markdown file in the desired location. Example: `overview/hello_world.md`. Then, add a link in the `SUMMARY.md` file which acts as the navigation for the language reference.
