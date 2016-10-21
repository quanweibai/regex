#answer
### 直接量字符
```
"absab".match(/ab/); ["ab"]
```
### 字符集
```
"abs1".match(/[ab]/); ["a"]
"hello, world".match(/[a-z]+/); ["hello"]
"2016, hello-world".match(/[-a-z]+/); ["hello-world"]
"2016, hello.world".match(/[.]+/); ["."]
"2016, hello.world".match(/.+/); ["2016, hello.world"]
"2016, hello.world".match(/[^0-9a-z]/); [","]
```
### 字符类
```
"hello\n\world".match(/.\*/); ["hello"]
"hello_world 2016".match(/\w\*/); ["hello_world"]
```
### 重复
```
"hello, world".match(/r?l/); ["l"]
"hello, world".match(/e?l?/); [""]
"hello, world".match(/\w\*/); ["hello"] 
"helhelhel, world".match(/hel+/); ["hel"]
"helhelhel, world".match(/(hel)+/); ["helhelhel", "hel"]
```
### 贪婪和非贪婪
```
"hello, world".match(/\w+/); "hello, world".match(/\w+?/); ["hello"] ["h"]
```
### 选择、分组和引用
```
"hello, world".match(/hello|world/); "hello, world".match(/world|hello/); ["hello"]
"hello, world".match(/world|hello/g); ["hello", "world"];
"12345678".match(/\d{3}|\d{2}/g); ["123", "456", "78"];
"12345678".match(/\d{2}|\d{3}/g); ["12", "34", "56", "78"];
"hello, world".match(/(\w)+,\s(\w)+/); ["hello, world", "o", "d"];
"hello, world".match(/(?:\w)+,\s(?:\w)+/); ["hello, world"];
"hello, hello".match(/(\w+), \1/); ["hello, hello", "hello"];
"hello, hello, world, world".match(/(\w+), \1, (\w+), \2/); ["hello, hello, world, world", "hello", "world"]
"hhhhaacc".match(/(\w)+\1/); ["hhhhaacc", "c"]
"hhhhaacc".match(/(\w)+?\1/); ["hh", "h"]
"hello=\"abs\"".match(/[^"']\*(["'])([^"']\*)\1/) ["hello="abs"", """, "abs"]
```
### 指定匹配位置、断言
```
"hello, hello".match(/^hello/g); ["hello"]
"hello\nhello".match(/^hello/gm); ["hello", "hello"]
"hello\nhello".match(/^hello/g); ["hello"] 
"hello world".match(/\b\w+\b/g); ["hello", "world"]
"hello, world heLLO world".match(/llo/gi);  ["llo", "LLO"]
"hello, world heLLO world".match(/llo(?= world)/gi); ["LLO"]
"hello, world heLLO world".match(/llo(?! world)/gi); ["llo"] 

"1234567".replace(/(\d)(?=(\d{3})+)/g, "$1,");
"1234567".replace(/(\d)(?=(\d{3})+$)/g, "$1,");
"1234567".replace(/(?<=\d)(?=(\d{3})+$)/g, "$1,"); // 不支持
```
### split()
```
"1  ,  2, 3, 4, 5 ,6".split(/\s*,\s*/); ["1", "2", "3", "4", "5", "6"]
```
