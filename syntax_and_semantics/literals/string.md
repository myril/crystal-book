# String

[String](http://crystal-lang.org/api/String.html)表示不可变的UTF-8字符序列.

通常用双引号(`"`)括一些UTF-8字符来创建一个String:

```crystal
"hello world"
```

## 转义

反斜杠表示字符串中的一个特殊字符, 它可以是一个命令的转义字符串或者用数值标识的unicode代码点.

可用的转义字符串:
```crystal
"\"" # 双引号
"\\" # 反斜杠
"\a" # 响铃
"\b" # 回退
"\e" # 中止,控制(主要用于命令行样式展示)
"\f" # 换页
"\n" # 新行
"\r" # 回车
"\t" # 制表
"\v" # 纵向制表
"\NNN" # 8进制ASCII字符
"\xNN" # 16进制ASCII字符
"\uNNNN" # 16进制unicode字符
"\u{NNNN...}" # 16进制unicode字符
```

任何带反斜杠的字符都会作为它本身插入.

一个反斜杠后跟最多3个0到7的随机数字来表示用8进制写的代码点:

```crystal
"\101" # => "A"
"\123" # => "S"
"\12"  # => "\n"
"\1"   # 一个字符的字符串, 代码点是1
```

反斜杠后跟一个`u`来表示一个unicode代码点. 它也能跟随确切的4位16进制字符来表示unicode字节(`\u0000` to `\uFFFF`)或者用大括号包起来的1到6个16进制字符(`\u{0}` to `\u{10FFFF}`.

```crystal
"\u0041"    # => "A"
"\u{41}"    # => "A"
"\u{1F52E}" # => "&#x1F52E;"
```

一个大括号可以包含多个unicode字符串, 用空格隔开.

```crystal
"\u{48 45 4C 4C 4F}" # => "HELLO"
```

## 插值

带插值的字符串允许绑定表达式, 该字符串将在运行时展开.

```crystal
a = 1
b = 2
"sum: #{a} + #{b} = #{a + b}" # => "sum: 1 + 2 = 3"
```

字符串插值也能用于[String#%](https://crystal-lang.org/api/master/String.html#%25(other)-实例方法).

任何表达式都能放到插值区域内, 但为了保证可读性尽量保证表达式简单.

可以用反斜杠转义`#`字符或者用非插值字符串如`%q()`来禁用插值.

```crystal
"\#{a + b}"  # => "#{a + b}"
%q(#{a + b}) # => "#{a + b}"
```

插值是用[String::Builder](http://crystal-lang.org/api/String/Builder.html)来实现, 并对`#{...}`里每个表达式调用`Object#to_s(IO)`. 表达式`"sum: #{a} + #{b} = #{a + b}"`等同于:

```crystal
String.build do |io|
  io << "sum: "
  io << a
  io << " + "
  io << b
  io << " = "
  io << a + b
end
```

# 百分比字符串文本

除了双引号字符串, Crystal也支持用百分号(`%`)和一对分隔符来表示字符串. 合法的分隔符有括号`()`, 中括号`[]`, 大括号`{}`, 尖括号`<>`和管道符`||`. 除了管道符, 其他所有分隔符都能嵌套, 这意味着字符串内的开始分隔符会转义下一个结束分隔符.

这样编写带双引号的字符串很方便, 这些双引号在双引号字符串中会被转义.

```crystal
%(hello ("world")) # => "hello (\"world\")"
%[hello ["world"]] # => "hello [\"world\"]"
%{hello {"world"}} # => "hello {\"world\"}"
%<hello <"world">> # => "hello <\"world\">"
%|hello "world"|   # => "hello \"world\""
```

`%q`表示的文字不会应用插值和转义, `%Q`有着和`%`一样的含义.

```crystal
name = "world"
%q(hello \n #{name}) # => "hello \\n \#{name}"
%Q(hello \n #{name}) # => "hello \n world"
```

## 多行字符串

任何字符串都能跨多行:

```crystal
"hello
      world" # => "hello\n      world"
```

注意上面的例子的末尾和前导空格, 以及回车最终都会出现在结果字符串中. 可以通过加入多个反斜杠来避免字符串被切割为多行:

```crystal
"hello " \
"world, " \
"no newlines" # 等同于 "hello world, no newlines"
```

或者, 在字符串中插入反斜杠后跟回车:

```crystal
"hello \
     world, \
     no newlines" # 等同于 "hello world, no newlines"
```

在这个例子中, 前导空格没被包含在结果字符串中.

## 定界符

*here document* 或者 *heredoc* 对于编写跨多行的字符串很有用. 定界符是通过`<<-`后跟字母开头的字符数值组成的定界符标识(并且也包含下划线)来表示. 定界符从下行开始, 在下一行以和开始定界标识符相同的字符作为结束(忽略前导空格), 后面可以跟新行或者非字母数值的字符.

```crystal
<<-XML
<parent>
  <child />
</parent>
XML
```

前导空格会从定界符内容中移除对应最后一行定界标识符前的空格个数.

```crystal
<<-STRING
  Hello
    world
  STRING # => "Hello\n  world"

<<-STRING
    Hello
      world
  STRING # => "  Hello\n    world"
```

可以在定界符字符串中直接调用方法(这个亲测报错, 不知道是不是我理解的问题)或者在括号里使用它们:

```crystal
<<-SOME
hello
SOME.upcase # => "HELLO"

def upcase(string)
  string.upcase
end

upcase(<<-SOME
  hello
  SOME) # => "HELLO"
```

定界符支持插值和转义.

把开始定界标识符用单引号引起来可以禁用插值和转义:

```crystal
<<-'HERE'
  hello \n #{world}
  HERE # => "hello \n #{world}"
```
