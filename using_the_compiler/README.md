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

Make sure to always use `--release` for production-ready executables and when performing benchmarks.

The reason for this is that performance without full optimizations is still pretty good and provides fast compile times, so you can use the `crystal` command almost as if it were an interpreter.

To reduce the binary size, you can add the `--no-debug` flag and use the `strip` command. Debug symbols will be removed, use this option if only size is an issue and you won't need to debug the program.

## Creating a statically-linked executable

To build a statically-linked executable of your program:

```
$ crystal build some_program.cr --release --static
```

**Note:** Building statically-linked executables is currently only supported on Alpine Linux.

More information about statically linking [can be found on the wiki](https://github.com/crystal-lang/crystal/wiki/Static-Linking).

## Creating a project or library

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
