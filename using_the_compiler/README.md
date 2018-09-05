# 使用编译器

只要你[安装](../installation/README.md)了编译器, 那么你将有一个叫`crystal`的二进制文件.

在之后的章节中美元符号(`$`)表示命令行.

## 编译和运行

要一次性编译且运行程序, 你可以通过带一个文件名的方式来调用`crystal`:

```
$ crystal some_program.cr
```

Crystal文件的扩展名是`.cr`.

另外你可以用`run`命令:

```
$ crystal run some_program.cr
```

## 创建可执行文件

用`build`命令来创建一个可执行文件:

```
$ crystal build some_program.cr
```

这将创建一个可运行的`some_program`文件:

```
$ ./some_program
```

**注意:** 默认生成的可执行文件 **是未完全优化的**. 用`--release`标志来开启优化:

```
$ crystal build some_program.cr --release
```

确保生产环境的可执行文件以及在执行基准测试时一直使用`--release`标志.

这个原因是即使没有完全优化性能仍相当不错并且提供了快速的编译时间, 所以你可以用`crystal`命令就跟它是解释器一样.

为了介绍二进制大小, 你可以增加`--no-debug`标志并且用`strip`命令. 调试代码将会被移除, 如果仅仅大小是个问题并且你不需要调试程序可以开启这个标志.

## 创建静态链接的可执行文件

为你的程序构建静态链接可执行文件:

```
$ crystal build some_program.cr --release --static
```

**注意:** 构建静态链接可执行文件目前只在Alpine Linux系统上支持.

更多关于静态链接的信息[能在这个wiki上找到](https://github.com/crystal-lang/crystal/wiki/Static-Linking).

## 创建项目或者库

Use the `init` command to create a Crystal project with the standard directory structure.

```
$ crystal init lib my_cool_lib
      create  my_cool_lib/.gitignore
      create  my_cool_lib/.editorconfig
      create  my_cool_lib/LICENSE
      create  my_cool_lib/README.md
      create  my_cool_lib/.travis.yml
      create  my_cool_lib/shard.yml
      create  my_cool_lib/src/my_cool_lib.cr
      create  my_cool_lib/src/my_cool_lib/version.cr
      create  my_cool_lib/spec/spec_helper.cr
      create  my_cool_lib/spec/my_cool_lib_spec.cr
Initialized empty Git repository in ~/my_cool_lib/.git/
```

## Other commands and options

To see the full set of commands, invoke `crystal` without arguments.

```
$ crystal
Usage: crystal [command] [switches] [program file] [--] [arguments]

Command:
    init                     generate a new project
    build                    build an executable
    docs                     generate documentation
    env                      print Crystal environment information
    eval                     eval code from args or standard input
    play                     starts crystal playground server
    run (default)            build and run program
    spec                     build and run specs (in spec directory)
    tool                     run a tool
    help, --help, -h         show this help
    version, --version, -v   show version
```

To see the available options for a particular command, use `--help` after a command:

```
$ crystal build --help
Usage: crystal build [options] [programfile] [--] [arguments]

Options:
    --cross-compile                  cross-compile
    -d, --debug                      Add full symbolic debug info
    --no-debug                       Skip any symbolic debug info
    -D FLAG, --define FLAG           Define a compile-time flag
    --emit [asm|llvm-bc|llvm-ir|obj] Comma separated list of types of output for the compiler to emit
    -f text|json, --format text|json Output format text (default) or json
    --error-trace                    Show full error trace
    -h, --help                       Show this message
    --ll                             Dump ll to Crystal's cache directory
    --link-flags FLAGS               Additional flags to pass to the linker
    --mcpu CPU                       Target specific cpu type
    --mattr CPU                      Target specific features
    --no-color                       Disable colored output
    --no-codegen                     Don't do code generation
    -o                               Output filename
    --prelude                        Use given file as prelude
    --release                        Compile in release mode
    -s, --stats                      Enable statistics output
    -p, --progress                   Enable progress output
    -t, --time                       Enable execution time output
    --single-module                  Generate a single LLVM module
    --threads                        Maximum number of threads to use
    --target TRIPLE                  Target triple
    --verbose                        Display executed commands
    --static                         Link statically
    --stdin-filename                 Source file name to be read from STDIN
```
