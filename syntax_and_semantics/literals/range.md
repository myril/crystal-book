# Range

[Range](http://crystal-lang.org/api/Range.html)通常用range文本来构造:

```crystal
x..y  # 一个包含range, 数学上的定义: [x, y]
x...y # 一个非包含range, 数学上的定义: [x, y)

# Example:
0..5.to_a # => [0, 1, 2, 3, 4, 5]
0...5.to_a # => [0, 1, 2, 3, 4]
```

一个简单的方式来记住哪个是包含, 哪个是非包含的方式, 可以想象成额外的点把 *y* 挤到了range的外面.
