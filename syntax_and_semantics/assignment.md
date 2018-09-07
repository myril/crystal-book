# 赋值

赋值是用(`=`)字符来完成.

```crystal
# 赋值给本地变量
local = 1

# 赋值给实例变量
@instance = 2

# 赋值给类变量
@@class = 3
```

上面每种变量将在后面详细解释.

一些包含`=`字符的语法糖也是可以的:

```crystal
local += 1  # 等同于: local = local + 1

# 下面的运算符也适用于上面的表达式:
# +, -, *, /, %, |, &, ^, **, <<, >>

local ||= 1 # 等同于: local || (local = 1)
local &&= 1 # 等同于: local && (local = 1)
```

方法的调用也可以用`=`结尾的语法糖来使用:

```crystal
# 设置访问器
person.name=("John")

# 上面的也可以写为:
person.name = "John"

# 一个索引赋值
objects.[]=(2, 3)

# 上面的也可以写为:
objects[2] = 3

# 没有赋值相关, 但也是一个语法糖:
objects.[](2, 3)

# 上面的也可以写为:
objects[2, 3]
```

`=`运算符语法糖在设置访问器和索引访问器都是适用的. 注意`||`和`&&`会用`[]?`方法来检查键值是否存在.

```crystal
person.age += 1        # 等同于: person.age = person.age + 1

person.name ||= "John" # 等同于: person.name || (person.name = "John")
person.name &&= "John" # 等同于: person.name && (person.name = "John")

objects[1] += 2        # 等同于: objects[1] = objects[1] + 2

objects[1] ||= 2       # 等同于: objects[1]? || (objects[1] = 2)
objects[1] &&= 2       # 等同于: objects[1]? && (objects[1] = 2)
```
