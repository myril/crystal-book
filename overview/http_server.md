# HTTP Server

一个稍微有趣的例子是HTTP Server:

```crystal
require "http/server"

server = HTTP::Server.new do |context|
  context.response.content_type = "text/plain"
  context.response.print "Hello world! The time is #{Time.now}"
end

address = server.bind_tcp 8080
puts "Listening on http://#{address}"
server.listen
```

如果你阅读过整个语言参考那么上面的代码就会有意义, 但我们从中已经学到了一些东西.

* 你可以[require](../syntax_and_semantics/requiring_files.html)在其他文件中定义的代码:

    ```crystal
    require "http/server"
    ```
* 你可以定义[本地变量](../syntax_and_semantics/local_variables.html)无需指定他们的类型:

    ```crystal
    server = HTTP::Server.new ...
    ```
* HTTP server的端口通过HTTP::Server对象的bind_tcp方法来指定 (端口设为8080).
    ```crystal
    address = server.bind_tcp 8080
    ```


* 你通过调用对象[方法](../syntax_and_semantics/classes_and_methods.html)(或者给对象发送消息)来编程.

    ```crystal
    HTTP::Server.new ...
    ...
    Time.now
    ...
    address = server.bind_tcp 8080
    ...
    puts "Listening on http://#{address}"
    ...
    server.listen
    ```

* 你可以用代码blocks或者简单[blocks](../syntax_and_semantics/blocks_and_procs.html), 这是一种非常简单的方式来复用代码并且从功能世界中获取一些功能:

    ```crystal
    HTTP::Server.new do |context|
      ...
    end
    ```

* You can easily create strings with embedded content, known as string interpolation. The language comes with other [syntax](../syntax_and_semantics/literals.html) as well to create arrays, hashes, ranges, tuples and more:

    ```crystal
    "Hello world! The time is #{Time.now}"
    ```
