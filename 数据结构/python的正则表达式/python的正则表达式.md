## Python的正则表达式

### 正则表达式包```(re)```的基本操作
* 生成正则表达式对象：```re.compile(pattern, flag=0)```
  
  从```pattern```生成正则表达式对象，下面几个操作都可以从```pattern```自动生成对象，因此下面几个函数的```pattern```参数既可以是普通字符串，也可以是```compile```出来的正则表达式对象。
* 检索：```re.search(pattern, string, flag=0)```
* 匹配：```re.match(pattern, string, flag=0)```
  
  若检索和匹配成功，返回相应的```match```对象，里面记录了成功匹配的相关信息，也可以直接用于真值判断。
* 分割：```re.split(pattern, string, maxsplit=0, flags=0)``` 
  
  ```maxsplit=0```表示要处理完整个```string```，函数返回分割后的list
* 找出所有匹配串：```re.findall(pattern, string, flags=0)```
  
  ```findall```返回匹配的子串的list，从左到右，非重叠

### 正则表达式的构造

#### 字符组
1. 字符组描述符```[...]```：与方括号中列出的字符序列中的任意字符匹配，与排列顺序无关。
   * 区间形式：```[0-9]```，```[a-zA-Z]```或者混写```[34ad-fs-z]```
   * 特殊形式```[^...]```：表示对```^```后列出的字符组求补，就是不匹配列出的字符的意思。
2. 圆点字符```.```：```.```可以匹配任意字符，比如```a..b```可以匹配所有以a开头b结尾的四字符串。
3. 为了方便，```re```采用转义串的形式定义了一些常用的字符组：
   * ```\d```：等价于```[0-9]```
   * ```\D```：等价于```[^0-9]```
   * ```\s```：与所有空白字符匹配，等价于```[ \t\v\n\f\r]```
   * ```\S```：与所有非空白字符匹配，等价于```[^ \t\v\n\f\r]```
   * ```\w```：与所有数字字母匹配，等价于```[0-9a-zA-Z]```
   * ```\W```：与所有非数字字母匹配，等价于```[^0-9a-zA-Z]```

#### 重复
1. 重复描述符：```*```，模式```a*```要求匹配模式a能匹配的字符串的0次或任意多次重复。
   * 贪婪匹配：模式与字符串里有可能匹配的最长子串匹配。如```ab*```应与```abbbbbbbc```中的```abbbbbbb```匹配。```re```从采用贪婪匹配。
   * 非贪婪匹配：模式与有可能匹配的最短子串匹配。
   * 还有一个重复描述符```+```：表示至少1次重复。如```\d+```等价于```\d\d*```。
2. 可选描述符```?```：```a?```可以与空串或与a匹配的字符串匹配，也就是说它要求与a匹配的字符串的0或1次重复匹配。
3. 重复次数描述符：```{n}```，```a{n}```与a匹配的串的n次重复匹配。
4. 重复次数的范围描述符：```{m,n}```表示重复[m,n]次匹配
* 在上述4种重复描述符后加```?```则采用非贪婪匹配策略。

#### 选择
1. 选择描述符：```|```描述与两种或多种情况之一的匹配，表示“或”，可以结合```()```使用，比如```(ab)|(cd)```等等。
   
#### 首尾描述符
1. 行首描述符：以```^```开头的模式，只能与一行的前缀子串匹配。
2. 行尾描述符：以```$```开头的模式，只能与一行的后缀子串匹配。

    * 注意：一行的前缀和后缀也包含整个被匹配串的前缀和后缀，如果串里有换行符，那么还包括换行符前的子串的后缀和换行符后的子串的前缀。
3. 串首描述符：```\A```开头的模式只与整个被匹配串的前缀匹配。
4. 串尾描述符：```\Z```结束的模式只与整个被匹配串的后缀匹配。

#### 匹配对象 (match对象)
用mat表示match对象
* 取得被匹配的子串：```mat.group()```
* 在目标串里的匹配位置：```mat.start()```
* 目标串里被匹配子串的结束位置：```mat.end()```
  * ```[start:end]```可以表示pattern在string中的切片
* 目标串里被匹配的区间：```mat.span()```
* 其他：```mat.re```和```mat.string```分别取得这个match对象所做匹配的正则表达式对象和目标串。

#### 模式里的组（group）
在一次成功匹配中，模式串里的各个组也都成功匹配，与他们匹配的那一组字符串将从1开始编号，而后可以通过方法调用```mat.group(n)```获取。如：

执行语句
```python
mat = re.search('((.)e)f', 'abcdef')
```
表达式```mat.group()```的值是```'cdef'```，表达式```mat.group(1)```的值是```'de'```，表达式```mat.group(2)```的值是```'d'```。
此外，```mat.groups()```将得到从1开始的序对列表。

另外，通过匹配得到的group序号可以用来约束模式后面的匹配，比如：
```'(.{2}) \1'```可以匹配字符串```'ok ok'```或```'no no'```，但不可以匹配```'no oh'```，模式里的```\1```表示匹配group(1)里相同的模式。

#### 正则表达式对象
通过```re.compile(pattern)```得到的正则表达式对象有自己的一套方法。
* 检索：```regex.search(string[, pos[, endpos]])```
* 匹配：```regex.match(string[, pos[, endpos]])```
* 完全匹配：```regex.fullmatch(string[, pos[, endpos]])```
* ```regex.findall(string[, pos[, endpos]])```
* ```regex.finditer(string[, pos[, endpos]])```
* 切分：```regex.split(string, maxsplit=0)```
* 替换：```regex.sub(repl, string, count=0)```
* ```regex.pattern```取得pattern