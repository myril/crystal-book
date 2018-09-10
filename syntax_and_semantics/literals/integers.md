# Integers

它们包含4个有符号数值类型和4个无符号数值类型:

类型 | 长度  | 最小值 | 最大值
 ---------- | -----------: | -----------: |-----------:
[Int8](http://crystal-lang.org/api/Int8.html)  | 8       | -128 | 127
[Int16](http://crystal-lang.org/api/Int16.html)  | 16 | −32,768 | 32,767
[Int32](http://crystal-lang.org/api/Int32.html) | 32  | −2,147,483,648 | 2,147,483,647
[Int64](http://crystal-lang.org/api/Int64.html)   |  64 | −2<sup>63</sup> | 2<sup>63</sup> - 1
[UInt8](http://crystal-lang.org/api/UInt8.html) | 8 |  0 | 255
[UInt16](http://crystal-lang.org/api/UInt16.html) | 16 | 0 | 65,535
[UInt32](http://crystal-lang.org/api/UInt32.html) | 32 |  0 | 4,294,967,295
[UInt64](http://crystal-lang.org/api/UInt64.html) | 64 | 0 | 2<sup>64</sup> - 1

数值字面的`+`或者`-`标志是可选的, 后面的一系列数字和下划线也是可以作为一个可选的后缀. 如果没有后缀, 那字面的类型则是`Int32`, `Int64`和`UInt64`中所有适合数值类型中最低的那个类型::

```crystal
1      # Int32

1_i8   # Int8
1_i16  # Int16
1_i32  # Int32
1_i64  # Int64

1_u8   # UInt8
1_u16  # UInt16
1_u32  # UInt32
1_u64  # UInt64

+10    # Int32
-20    # Int32

2147483648          # Int64
9223372036854775808 # UInt64
```

后缀前面的`_`是可选的.

下划线能让数值更易读:

```crystal
1_000_000 # better than 1000000
```

二进制是以`0b`开头:

```crystal
0b1101 # == 13
```

八进制是以`0o`开头:

```crystal
0o123 # == 83
```

十六进制是以`0x`开头:

```crystal
0xFE012D # == 16646445
0xfe012d # == 16646445
```
