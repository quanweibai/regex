# [正则表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions)
[TOC]

1. 一般字符 a,b,c
2. 特殊字符 \,^,$,*,+,?,.,(x),(?:x),x(?=y),x(?!y),x|y,{n},{n,m},[xyz],[^xyz], 
      [\b],\b,\B,\cX,\d,\D,\f,\n,\r,\s,\S,\t,\v,\w,\W,\n,\0,\xhh,\uhhhh,\u{hhhh}
      
# regex
### 直接量字符
<table>
  <tr>
    <td>字符</td>
    <td>匹配</td>
  </tr>
  <tr>
    <td>字母和数字本身</td>
    <td>自身</td>
  </tr>
  <tr>
    <td>\0(不重要)</td>
    <td>NUL字符(\u0000)</td>
  </tr>
  <tr>
    <td>\t(不重要)</td>
    <td>制表符(\u0009)</td>
  </tr>
  <tr>
    <td>\n</td>
    <td>换行符(\u000A)</td>
  </tr>
  <tr>
    <td>\v(不重要)</td>
    <td>垂直制表符(\u000B)</td>
  </tr>
  <tr>
    <td>\f(不重要)</td>
    <td>换页符(\u000C)</td>
  </tr>
  <tr>
    <td>\r(不重要)</td>
    <td>回车符(\u000D)</td>
  </tr>
  <tr>
    <td>\xnn(不重要)</td>
    <td>由十六进制数nn指定的拉丁字符，例如，\x0A等价于\n</td>
  </tr>
  <tr>
    <td>\uxxxx(不重要)</td>
    <td>由十六进制数xxxx指定的Unicode字符，例如\u0009等价于\t</td>
  </tr>
  <tr>
    <td>\cX(不重要)</td>
    <td>控制字符^X，例如\cJ等价于换行符\n</td>
  </tr>
</table>
```
"absab".match(/ab/)
```
* 普通字符的匹配
* 匹配了一次就会停止，如果想[全局匹配](#修饰符)怎么做？
#### 字符集
<table>
  <tr>
    <td>字符</td>
    <td>匹配</td>
  </tr>
  <tr>
    <td>[...]</td>
    <td>方括号内的任意字符</td>
  </tr>
  <tr>
    <td>[^...]</td>
    <td>不在方括号内的任意字符</td>
  </tr>
</table>
* 表示范围用"-"，只有当-紧跟在[之后时，才表示"-"自身
* 字符集内的元字符和正则表达式的元字符不一样
```
"abs1".match(/[ab]/);
"hello, world".match(/[a-z]+/);
"2016, hello-world".match(/[-a-z]+/);
"2016, hello.world".match(/[.]+/); "2016, hello.world".match(/.+/);
"2016, hello.world".match(/[^0-9a-z]/);
```
### 字符类
<table>
  <tr>
    <td>字符</td>
    <td>匹配</td>
  </tr>
  <tr>
    <td>.</td>
    <td>除**换行符和其他Unicode行终止符**之外的任意字符</td>
  </tr>
  <tr>
    <td>\w</td>
    <td>任何ASCII字符组成的单词，等价于[a-zA-Z0-9_]</td>
  </tr>
  <tr>
    <td>\W</td>
    <td>任何不是ASCII字符组成的单词，等价于[^a-zA-Z0-9_]</td>
  </tr>
  <tr>
    <td>\s</td>
    <td>任何Unicode空白符</td>
  </tr>
  <tr>
    <td>\S</td>
    <td>任何非Unicode空白符的字符，注意\w和\S不同</td>
  </tr>
  <tr>
    <td>\d</td>
    <td>任何ASCII数字，等价于[0-9]</td>
  </tr>
  <tr>
    <td>\D</td>
    <td>除了ASCII数字之外的任何字符，等价于[^0-9]</td>
  </tr>
  <tr>
    <td>[\b](不重要)</td>
    <td>退格直接量</td>
  </tr>
</table>
* 大写表示小写的**反义**,\w(word),\s(space),\d(digit)
```
"hello\n\world".match(/.*/); 
"hello_world 2016".match(/\w*/); 
```
### 重复（量词）
<table>
  <tr>
    <td>字符</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>{n,m}</td>
    <td>匹配前一项至少n次，但不能超过m次</td>
  </tr>
  <tr>
    <td>{n,}</td>
    <td>匹配前一项n次或者更多次</td>
  </tr>
  <tr>
    <td>{n}</td>
    <td>匹配前一项n次</td>
  </tr>
  <tr>
    <td>?</td>
    <td>匹配前一项0次或者1次，也就是说前一项是可选的，等价于{0,1}</td>
  </tr>
  <tr>
    <td>+</td>
    <td>匹配前一项1次或多次，等价于{1,}</td>
  </tr>
  <tr>
    <td>*</td>
    <td>匹配前一项0次或多次，等价于{0,}</td>
  </tr>
</table>
* 默认是**贪婪**的，那么什么是**贪婪**，**非贪婪**
* 量词匹配的是前面**前面紧跟着的部分**
```
"hello, world".match(/r?l/);
"hello, world".match(/e?l?/);
"hello, world".match(/\w*/);
"helhelhel, world".match(/hel+/);
"helhelhel, world".match(/(hel)+/);
```
### 贪婪和非贪婪
贪婪和非贪婪只作用于量词，默认是贪婪，如果在量词后面紧跟一个"?"，则表示非贪婪；
```
"hello, world".match(/\w+/); "hello, world".match(/\w+?/);
```
### 选择、分组和引用
<table>
  <tr>
    <td>字符</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>|</td>
    <td>选择，匹配的是该符号左边的子表达式或右边的子表达式</td>
  </tr>
  <tr>
    <td>(...)</td>
    <td>组合，将几个项组合为一个单元，这个单元可通过"*"，"+"，"?"和"|"等符号加以修饰，而且可以记住和这个组合相匹配的字符串以供此后的引用使用</td>
  </tr>
  <tr>
    <td>(?:...)</td>
    <td>只组合，把项合并到一个单元，但不记忆与该组相匹配的字符</td>
  </tr>
  <tr>
    <td>\n</td>
    <td>和第n个分组第一次匹配的字符相匹配 ，组是圆括号中的子表达式（也有可能是嵌套的），组索引是从左到右的左括号数，"(?:"形式的分组不编码</td>
  </tr>
</table>
* 量词匹配的是**前面紧跟的部分**，选择匹配的是**子表达式**
* 选择匹配的顺序是从左到右
* 组合作用有两个，一个是将几个项组合为一个单元（量词匹配的是前面紧跟的部分，括号括起来的部分是一个单元），而是用于后续引用
* (...)(?:...)又分别叫做捕获型分组和非捕获型分组，捕获型分组具有上述两个作用，非捕获型分组只有上述第一个作用
* 什么时候会用到非捕获型分组？
* 带有量词的捕获型分组捕获以后只有一个分组还是匹配了多少次就捕获多少次？
* 匹配hello="abs"或者hello='abs',不匹配hello="abs'或者hello='abs"?
```
// 选择
"hello, world".match(/hello|world/);
"hello, world".match(/world|hello/);
"hello, world".match(/world|hello/g);
"12345678".match(/\d{3}|\d{2}/g); 
"12345678".match(/\d{2}|\d{3}/g);

// 分组
"hello, world".match(/(\w)+,\s(\w)+/); 
"hello, world".match(/(?:\w)+,\s(?:\w)+/);

// 引用
"hello, hello".match(/(\w+), \1/);
"hello, hello, world, world".match(/(\w+), \1, (\w+), \2/);
"hhhhaacc".match(/(\w)+\1/); 
"hhhhaacc".match(/(\w)+?\1/); 
"hello=\"abs\"".match(/[^"']*(["'])([^"']*)\1/)
"hello=\'abs\"".match(/[^"']*(["'])([^"']*)\1/)
```
### 指定匹配位置、断言
<table>
  <tr>
    <td>字符</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>^</td>
    <td>匹配字符串的开头，在多行检索中，匹配一行的开头</td>
  </tr>
  <tr>
    <td>$</td>
    <td>匹配字符串的结尾，在多行检索中，匹配一行的结尾</td>
  </tr>
  <tr>
    <td>\b</td>
    <td>匹配一个单词的边界，简言之，就是位于字符\w和\W之间的位置，或位于字符\w和字符串的开头或者结尾之间的位置（但需要注意，[\b]匹配的是退格符）</td>
  </tr>
  <tr>
    <td>\B</td>
    <td>匹配非单词边界的位置</td>
  </tr>
  <tr>
    <td>(?=p)</td>
    <td>零宽正向先行断言，要求接下来的字符都与匹配，但不能包括匹配p的那些字符</td>
  </tr>
  <tr>
    <td>(?!p)</td>
    <td>零宽负向先行断言，要求接下来的字符不与p匹配</td>
  </tr>
</table>
* [修饰符m](#修饰符)可以改变^和$的含义，默认匹配字符串的开始和结尾，添加修饰符以后可以匹配行首和行尾
* \b具体匹配哪些字符？[a-zA-Z0-9\_]
* "零宽""正向""先行""断言"这几个词怎么理解？(?<=p)(?<!p)
* "1234567" => "1,234,567"怎么实现？暂不考虑小数
```
"hello, hello".match(/^hello/g);
"hello\nhello".match(/^hello/g); "hello\nhello".match(/^hello/gm);
"hello world".match(/\b\w+\b/g);

"ab cs 11,44;dd0;p".match(/\b\w+\b/g);

"hello, world heLLO world".match(/llo/gi);
"hello, world heLLO world".match(/llo(?= world)/gi); 
"hello, world heLLO world".match(/llo(?! world)/gi); 
```
### 修饰符
<table>
  <tr>
    <td>字符</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>i</td>
    <td>执行不区分大小写的匹配</td>
  </tr>
  <tr>
    <td>g</td>
    <td>执行一个全局匹配，简言之，即找到所有的匹配，而不是在找到第一个之后就停止</td>
  </tr>
  <tr>
    <td>m</td>
    <td>多行匹配模式，^匹配一行的开头和字符串的开头，$匹配行的结束和字符串的结束</td>
  </tr>
</table>
# 正则表达式相关方法
### [字符串的方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
#### search()
```
str.search(regexp)
```
* 如果没有匹配返回-1，如果有返回第一次匹配的位置
* 会忽略修饰符g
```
"JavaScript".search(/script/i);
"JavaScript".search(/script/ig);
```
#### match()
```
str.match(regexp)
```
* 如果没有匹配返回null；如果使用了修饰符g，返回包含所有匹配结果的数组，如果没有使用修饰符g，返回一个数组，数组的第一个元素是匹配的字符串，余下的元素是正则表达式中用院落好括起来的子表达式
#### replace()
```
str.replace(regexp|substr, newSubStr|function)
```
如果第二个参数是字符串，该字符串可以包含的特殊字符如下：
<table>
  <tr>
    <td>模式</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>$$</td>
    <td>$本身</td>
  </tr>
  <tr>
    <td>$&</td>
    <td>匹配的字符串</td>
  </tr>
  <tr>
    <td>$`</td>
    <td>匹配字符串前面的部分</td>
  </tr>
  <tr>
    <td>$'</td>
    <td>匹配字符串后面的部分</td>
  </tr>
  <tr>
    <td>$n</td>
    <td>匹配第n个捕获型字符串的内容</td>
  </tr>
</table>
如果第二个参数是函数，该函数的参数如下：
<table>
  <tr>
    <td>可能的名字</td>
    <td>含义</td>
  </tr>
  <tr>
    <td>match</td>
    <td>匹配的字符串，相当于上面的$&</td>
  </tr>
  <tr>
    <td>p1, p2, ...</td>
    <td>对应上面的$1,$2,...</td>
  </tr>
  <tr>
    <td>offset</td>
    <td>匹配的字符串在整个字符串中的位置</td>
  </tr>
  <tr>
    <td>string</td>
    <td>整个字符串</td>
  </tr>
</table>
```
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
var newstr = str.replace(re, '$2, $1');
console.log(newstr);

function replace(str, array) {
  var index = 0;
  return str.replace(reg, function() {
    return array[index++];
  });
}
var str = "您输入的数值是：%, %, %";
var reg = /%/g;
replace(str, [20, 30, 40]);
```
#### split()
```
str.split([separator[, limit]])
```
* 参数可以是正则表达式
```
"1  ,  2, 3, 4, 5 ,6".split(/\s*,\s*/); 
```
### [正则表达式的方法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)
#### 创建正则表达式
* //
* new RegExp()
#### test()
* 存在匹配返回true，否则返回false
* 会改变正则对象的lastIndex值

#### exec()
```
regexObj.exec(str)
```
* 不存在返回null
* [例子](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec)
