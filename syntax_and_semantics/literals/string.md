# String

[String](http://crystal-lang.org/api/String.html)表示不可变的UTF-8字符序列.

通常用双引号(`"`)括一些UTF-8字符来创建一个String:

```crystal
"hello world"
```

## Escaping

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

## Interpolation

A string literal with interpolation allows to embed expressions into the string which will be expanded at runtime.

```crystal
a = 1
b = 2
"sum: #{a} + #{b} = #{a + b}" # => "sum: 1 + 2 = 3"
```

String interpolation is also possible with [String#%](https://crystal-lang.org/api/master/String.html#%25(other)-instance-method).

Any expression may be placed inside the interpolated section, but it’s best to keep the expression small for readability.

Interpolation can be disabled by escaping the `#` character with a backslash or by using a non-interpolating string literal like `%q()`.

```crystal
"\#{a + b}"  # => "#{a + b}"
%q(#{a + b}) # => "#{a + b}"
```

Interpolation is implemented using a [String::Builder](http://crystal-lang.org/api/String/Builder.html) and invoking `Object#to_s(IO)` on each expression enclosed by `#{...}`. The expression `"sum: #{a} + #{b} = #{a + b}"` is equivalent to:

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

# Percent string literals

Besides double-quotes strings, Crystal also supports string literals indicated by a percent sign (`%`) and a pair of delimiters. Valid delimiters are parenthesis `()`, square brackets `[]`, curly braces `{}`, angles `<>` and pipes `||`. Except for the pipes, all delimiters can be nested meaning a start delimiter inside the string escapes the next end delimiter.

These are handy to write strings that include double quotes which would have to be escaped in double-quoted strings.

```crystal
%(hello ("world")) # => "hello (\"world\")"
%[hello ["world"]] # => "hello [\"world\"]"
%{hello {"world"}} # => "hello {\"world\"}"
%<hello <"world">> # => "hello <\"world\">"
%|hello "world"|   # => "hello \"world\""
```

A literal denoted by `%q` does not apply interpolation nor escapes while `%Q` has the same meaning as `%`.

```crystal
name = "world"
%q(hello \n #{name}) # => "hello \\n \#{name}"
%Q(hello \n #{name}) # => "hello \n world"
```

## Multiline strings

Any string literal can span multiple lines:

```crystal
"hello
      world" # => "hello\n      world"
```

Note that in the above example trailing and leading spaces, as well as newlines,
end up in the resulting string. To avoid this a string can be split into multiple lines
by joining multiple literals with a backslash:

```crystal
"hello " \
"world, " \
"no newlines" # same as "hello world, no newlines"
```

Alternatively, a backslash followed by a newline can be inserted inside the string literal:

```crystal
"hello \
     world, \
     no newlines" # same as "hello world, no newlines"
```

In this case, leading whitespace is not included in the resulting string.

## Heredoc

A *here document* or *heredoc* can be useful for writing strings spanning over multiple lines.
A heredoc is denoted by `<<-` followed by an heredoc identifier which is an alphanumeric sequence starting with a letter (and may include underscores). The heredoc starts in the following line and ends with the next line that starts with the heredoc identifier (ignoring leading whitespace) and is either followed by a newline or a non-alphanumeric character.

```crystal
<<-XML
<parent>
  <child />
</parent>
XML
```

Leading whitespace is removed from the heredoc contents according to the number of whitespace in the last line before the heredoc identifier.

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

It is possible to directly call methods on heredoc string literals, or use them inside parentheses:

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

A heredoc generally allows interpolation and escapes.

To denote a heredoc without interpolation or escapes, the opening heredoc identifier is enclosed in single quotes:

```crystal
<<-'HERE'
  hello \n #{world}
  HERE # => "hello \n #{world}"
```
