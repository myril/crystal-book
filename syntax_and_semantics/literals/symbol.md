# Symbol

[Symbol](http://crystal-lang.org/api/Symbol.html)表示在整个源码中都是唯一的名字.

Symbols在编译时解释并且不能动态创建. 唯一的创建方法是用symbol文字, 用(`:`)加标识符来表示. 标识符也可以用(`"`)引起来.

```crystal
:unquoted_symbol
:"quoted symbol"
:"a" # identical to :a
```

双引号标识符能包含任何unicode字符, 包括空格和一些转义字符如[string literal](./string.html), 还不能用插值.

非双引号标识符的命令规则跟方法名是一样的. 能包含字母数值字符, 下划线(`_`)或者代码点大于`159`(`0x9F`)的字符. 且不能以数字开头, 能以感叹号(`!`)或者问号(`?`)结尾.

```crystal
:question?
:exclamation!
```

所有[Crystal操作符](../operators.html)都能作为symbol的非引号名字:
```crystal
:+
:-
:*
:/
:%
:&
:|
:^
:**
:>>
:<<
:==
:!=
:<
:<=
:>
:>=
:<=>
:===
:[]
:[]?
:[]=
:!
:~
:!~
:=~
```

底层, symbols是用`Int32`类型的常量数值来实现的.

## 百分号symbol数组

除了单个symbol文字, 也可以用百分号来创建symbol[数组](https://crystal-lang.org/api/Array.html). 它用`%i`加一对分隔符来指示. 合法的分隔符有括号`()`, 方括号`[]`, 大括号`{}`, 尖括号`<>`和管道`||`. 除了管道, 所有的分隔符都能嵌套, 这意味着字符串内的开始分隔符会转义下一个结束分隔符.

```crystal
%i(foo bar baz) # => [:foo, :bar, :baz]
%i(foo\nbar baz) # => [:"foo\nbar", :baz]
%i(foo(bar) baz) # => [:"foo(bar)", :baz]
```

标识符能包含任一unicode字符. 单个symbols由一个空格来分割, 对其(` `)转义之后能作为标识符的一部分.

```crystal
%i(foo\ bar baz) # => [:"foo bar", :baz]
```
