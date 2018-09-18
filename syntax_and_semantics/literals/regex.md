# 正则表达式

正则表达式是由[Regex](http://crystal-lang.org/api/Regex.html)类来表示的.

正则通常是用[PCRE](http://pcre.org/pcre.txt)语法的正则文本来创建的. 它是由正斜杠(`/`)包起来UTF-8字符串组成:

```crystal
/foo|bar/
/h(e+)llo/
/\d+/
/あ/
```

## 转义

正则表达式支持同样的[转义字符串文本](./string.html).

```crystal
/\// # 斜杠
/\\/ # 反斜杠
/\b/ # 回退
/\e/ # esc
/\f/ # 换页
/\n/ # 新行
/\r/ # 回车
/\t/ # 制表
/\v/ # 纵向制表
/\NNN/ # 8进制ASCII字符
/\xNN/ # 16进制ASCII字符
/\uNNNN/ # 16进制unicode字符
/\u{NNNN...}/ # 16进制unicode字符
```

分隔符`/`在斜杠分割的正则表达式文本中必须转义.
注意, 如果PCRE语法指定的字符作为文本字符的话, 则必须进行转义.

## 插值

在正则表达式文本中插值工作和[字符串文本](./string.html)一样. 需要注意的是, 如果结果字符串是一个非法的正则表达式, 那么在使用此功能时将会在运行时抛出异常.

## 修饰符
闭合分隔符后面可以跟一些可选的修饰符来调整正则表达式的匹配行为.

* `i`: 不区分大小写匹配 (`PCRE_CASELESS`):  Unicode letters in the pattern match both upper and lower case letters in the subject string.
* `m`: 多行匹配 (`PCRE_MULTILINE`): The *start of line* (`^`) and *end of line* (`$`) metacharacters match immediately following or immediately before internal newlines in the subject string, respectively, as well as at the very start and end.
* `x`: extended whitespace matching (`PCRE_EXTENDED`): Most white space characters in the pattern are totally ignored except when ignore or inside a character class. Unescaped hash characters `#` denote the start of a comment ranging to the end of the line.

```crystal
/foo/i.match("FOO")         # => #<Regex::MatchData "FOO">
/foo/m.match("bar\nfoo")    # => #<Regex::MatchData "foo">
/foo /x.match("foo")        # => #<Regex::MatchData "foo">
/foo /imx.match("bar\nFOO") # => #<Regex::MatchData "FOO">
```

## Percent regex literals

Besides slash-delimited literals, regular expressions may also be expressed as a percent literal indicated by `%r` and a pair of delimiters. Valid delimiters are parenthesis `()`, square brackets `[]`, curly braces `{}`, angles `<>` and pipes `||`. Except for the pipes, all delimiters can be nested meaning a start delimiter inside the literal escapes the next end delimiter.

These are handy to write regular expressions that include slashes which would have to be escaped in slash-delimited literals.

```crystal
%r((/)) # => /(\/)/
%r[[/]] # => /[\/]/
%r{{/}} # => /{\/}/
%r<</>> # => /<\/>/
%r|/|   # => /\//
```
