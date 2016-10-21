#answer
### 直接量字符
"absab".match(/ab/); ["ab"]
### 字符集
"abs1".match(/[ab]/); ["a"]
"hello, world".match(/[a-z]+/); ["hello"]
"2016, hello-world".match(/[-a-z]+/); ["hello-world"]
"2016, hello.world".match(/[.]+/); ["."]
"2016, hello.world".match(/.+/); ["2016, hello.world"]
"2016, hello.world".match(/[^0-9a-z]/); [","]
### 字符类
"hello\n\world".match(/.\*/); ["hello"]
"hello_world 2016".match(/\w\*/); ["hello_world"]
