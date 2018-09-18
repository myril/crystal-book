# Char

[Char](http://crystal-lang.org/api/Char.html)表示32位[Unicode](http://en.wikipedia.org/wiki/Unicode) [代码点](http://en.wikipedia.org/wiki/Code_point).

通常用单引号括一个UTF-8字符来创建一个Char.

```crystal
'a'
'z'
'0'
'_'
'あ'
```

反斜杠表示一个特殊字符, 它可以是命名的转义字符串或者一个unicode代码点的数值表示.

可用的转义字符串:
```crystal
'\'' # 单引号
'\\' # 反斜杠
'\a' # 响铃
'\b' # 回退
'\e' # esc 中止,控制(主要用于命令行样式展示)
'\f' # 换页
'\n' # 新行
'\r' # 回车
'\t' # 制表
'\v' # 纵向制表
'\uNNNN' # 16进制unicode字符
'\u{NNNN...}' # 16进制unicode字符
```

反斜杠后跟一个`u`来表示一个unicode代码点. 它也能跟随确切的4位16进制字符来表示unicode字节(`\u0000` to `\uFFFF`)或者用大括号包起来的1到6个16进制字符(`\u{0}` to `\u{10FFFF}`.

```crystal
'\u0041' # => 'A'
'\u{41}' # => 'A'
'\u{1F52E}' # => '&#x1F52E;'
```
