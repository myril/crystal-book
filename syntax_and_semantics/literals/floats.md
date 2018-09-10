# Floats

有两种浮点类型, [Float32](http://crystal-lang.org/api/Float32.html)和[Float64](http://crystal-lang.org/api/Float64.html),
与之对应的是IEEE定义的[binary32](http://en.wikipedia.org/wiki/Single_precision_floating-point_format)
和[binary64](http://en.wikipedia.org/wiki/Double_precision_floating-point_format).

浮点字面上`+`或者`-`标志是可选的, 后跟一系列数值或者下划线,再跟一个小数点, 再跟数值或下划线, 再跟可选的指数后缀, 再跟可选的类型后缀. 如果没有后缀, 则字面类型是`Float64`.

```crystal
1.0      # Float64
1.0_f32  # Float32
1_f32    # Float32

1e10     # Float64
1.5e10   # Float64
1.5e-7   # Float64

+1.3     # Float64
-0.5     # Float64
```

后缀前面的`_`是可选的.

下划线能让数值更易读:

```crystal
1_000_000.111_111 # 可读性比1000000.111111要高得多, 且功能性是一样的
```
