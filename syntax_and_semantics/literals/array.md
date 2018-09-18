# Array

[Array](http://crystal-lang.org/api/Array.html)是特定类型`T`元素的有序且整数索引的泛型集合.

Arrays通常用方括号(`[]`)来创建, 并且用逗号(`,`)来区分每个元素.

```crystal
[1, 2, 3]
```

## 泛型类型参数

数组的泛型类型参数`T`是通过数组元素的类型推导出来的. 当所有的数组元素的类型都相同, 那么`T`就等于这个类型. 否则就是所有元素类型的并集.

```crystal
[1, 2, 3]          # => Array(Int32)
[1, "hello", 'x']  # => Array(Int32 | String | Char)
```

显式类型通过在闭合方括号后跟`of`和类型来实现, 用空格隔开. 这会覆盖推导类型, 初始可以创建包含部分类型, 但以后可以接受其他的类型的数组.

```crystal
array_of_numbers = [1, 2, 3] of Float64 | Int32  # => Array(Float64 | Int32)
array_of_numbers << 0.5                          # => [1, 2, 3, 0.5]


array_of_int_or_string = [1, 2, 3] of Int32 | String  # => Array(Int32 | String)
array_of_int_or_string << "foo"                       # => [1, 2, 3, "foo"]
```

空数组必须要指定类型:

```crystal
[] of Int32  # => Array(Int32).new
```

## 百分号数组文本

[Arrays of strings](./string.html#Percent String Array Literal) 和 [arrays of symbols](./symbol.html#Percent Symbol Array Literal)都能通过百分号数组常量来创建:

```crystal
%w(one two three)  # => ["one", "two", "three"]
%i(one two three)  # => [:one, :two, :three]
```

## 类数组类型文本

Crystal对于数组和类数组类型支持额外的文本表示. 它是由类型名字后跟大括号(`{}`)括起来的一组元素组成, 其中的单个元素由逗号(`,`)分隔.

```crystal
Array{1, 2, 3}
```

这个文本能被用于任何类型, 只要它有argless构造函数且能响应`<<`.

```crystal
IO::Memory{1, 2, 3}
Set{1, 2, 3}
```

像`IO:Memory`这样的非泛型类型, 其相当于:

```crystal
array_like = IO::Memory.new
array_like << 1
array_like << 2
array_like << 3
```

像`Set`这样的泛型类型, 泛型类型`T`是跟数组文本一样通过其中的元素类型推导出来的. 上面相当于:

```crystal
array_like = Set(typeof(1, 2, 3)).new
array_like << 1
array_like << 2
array_like << 3
```

参数的类型能作为类型名字的一部分来明确指定:

```crystal
Set(Int32) {1, 2, 3}
```
