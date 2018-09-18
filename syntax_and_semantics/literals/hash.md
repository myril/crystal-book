# Hash

[Hash](http://crystal-lang.org/api/Hash.html)是将`K`类型的键映射到`V`类型的值的键值对的泛型集合.

Hashes通常是用大括号(`{ }`)括起来的一组用逗号`,`区分开的键值对且在键和值之间用`=>`作为分隔符的hash文本来创建.

```crystal
{"one" => 1, "two" => 2}
```

# 泛型类型参数

键`K`和值`V`的泛型类型参数分别通过文本内键和值的类型推导出来的. 如果各自参数类型有相同的类型, 那么`K`/`V`就等于它们, 否则就是所有各自键值类型的并集.

```crystal
{1 => 2, 3 => 4}     # Hash(Int32, Int32)
{1 => 2, 'a' => 3}   # Hash(Int32 | Char, Int32)
```

显式类型通过在结束大括号后面跟`of`(用空格隔开), 键类型(`K`)后跟分隔符`=>`和值类型(`V`)来指定.  这会重载推导类型, 初始可以创建一个只包含部分类型但还能接收其他类型的hash.

空hash文本必须要指定类型:
```crystal
{} of Int32 => Int32 # => Hash(Int32, Int32).new
```

## 类Hash类型文本

针对hashes和类hash类型Crystal支持额外的文本表示. 它是由类型名称后跟用大括号(`{}`)括起来的一组用逗号来区分的键值对组成的.

```crystal
Hash{"one" => 1, "two" => 2}
```

这个文本能适用所有类型, 只要它有argless构造函数并且能响应`[]=`.

```crystal
HTTP::Headers{"foo" => "bar"}
```

像`HTTP::Headers`这类非泛型类型, 则等同于:

```crystal
headers = HTTP::Headers.new
headers["foo"] = "bar"
```

对于泛型类型, 它是用和hash文本一样的方式通过键和值来推导出来的.

```crystal
MyHash{"foo" => 1, "bar" => "baz"}
```

如果`MyHash`是泛型, 则上面的等同于这个:

```crystal
my_hash = MyHash(typeof("foo", "bar"), typeof(1, "baz")).new
my_hash["foo"] = 1
my_hash["bar"] = baz
```

类型参数可以显式指定为类型名字的一部分:

```crystal
MyHash(String, String | Int32) {"foo" => "bar"}
```
