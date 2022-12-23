#### 1.正则

**定义**

``` js
// 正则表达式 Regular Expression  Regular 有规则的
    const reg = /前端/    // /xxx/ 是正则的字面量
    // 定义： 是一种字符串匹配模式（pattern）  模式 ==> 规则

    // 作用：
    //  1. 表单验证： 匹配
    //  2. 过滤敏感词： 替换
    //  3. 字符串中提取想要的部分： 提取

    // 使用
    // 1. 先定义规则
    // 2. 看是否匹配
```

**方法**

1. reg.test(要匹配的字符串)    //返回布尔值
2.  reg.exec('要检测的字符串') //返回的是结果数组 ，没有匹配成功就是返回null

``` js
 const str = '我们在学前端'

    // 1. reg.test(要匹配的字符串) 
    // ==> true / false 
    console.log(reg.test(str))
    // 2. reg.exec('要检测的字符串')
    // 如果匹配成功，返回的是结果数组，否则返回null
```

**边界符**

``` js
// 边界符  
    // 1.^ 脱字符 以什么什么开头
    // 2.$ 以什么什么结尾
      //3. 如果^$一起使用，必须精确匹配，检测的字符串和我们的规则一模一样，多一个字符少一个字都不行
```

**例子**

``` js
 console.log(/^哈/.test('哈'))  // true
    console.log(/^哈/.test('哈哈')) // true
    console.log(/^哈/.test('二哈')) // false  没有以哈字开头

    console.log(/^二哈/.test('二哈')) // true  
    console.log(/^二哈/.test('哈二哈')) // false  
    console.log('------------------')
    // $ 以什么什么结尾
    console.log(/哈$/.test('哈'))
    console.log(/二哈$/.test('哈二哈'))
    // 两个边界符一起配合使用
    console.log(/^哈$/.test('哈')) // true
    console.log(/^二哈hhh$/.test('二哈hhh')) // false

    console.log(/^哈$/.test('哈哈')) // false
```

**量词**符

``` js
// 量词符
    1. * 重复0次或更多次，
    2. +重复一次或更多次 
    3.？重复0次或1次
    4. 量词
    5. * >= 0
    6. + >= 1
    7. ?  0 || 1 
    8. {n}  n个
    9. {n,}  >=n
    10. {n,m}  >=n && <=m
```

**例**

``` js
 const reg1 = /^ab{2,5}c$/
    // abbc abbbc abbbbc abbbbbc
    const res = reg1.test('abbbbc')
    console.log(res)
    // 横向模糊匹配  一个正则可匹配的字符串长度是不固定的的，可以是多种情况
    // 实现方式 ： 量词
    // 字符类 [] 表示有一系列字符可供选择，只要匹配其中一个就可以了 
    // 字符组， 同一个位置上可能出现各种字符，也叫做纵向模糊匹配
    // 写法： []方括号中列出所有的可能性 ， 最后只选一个

    // 联想  ： 抽奖，只取一个！

    // [abc] 只选一个
    console.log(/^[abc]$/.test('a'))
    console.log(/^[abc]$/.test('b'))
    console.log(/^[abc]$/.test('c'))
    console.log('----------------')
    console.log(/^[abc]$/.test('ab'))  // false
    console.log(/^[abc]$/.test('aa'))  // false

    // /^[abc]$/ ==> /^a$/ /^b$/ /^c$/
    // 我们加了边界符，精确匹配，只能选一个， ab是两个字符

    console.log('--------------')
    // 不写边界符 
    console.log(/[abc]/.test('aa')) // true

    // ==> 字符组+量词   量词只作用于前一个字符组
    console.log(/^[abc][abc]$/.test('ab')) // true
    console.log(/^[abc]{3}$/.test('abc')) // true

    console.log(/^[ef][abc]{2}$/.test('eac')) // true

    //[abc][abc] ==> a b c  ; a b c ==>  aa  ab ac  ba bb bc ca cb cc

```

** 范围表示法**

``` js
范围表示法
    // 用-表示范围
    // [0123456789]  ==> [0-9] [a-z]
    // 但是，注意，不能写 [9-0]  [Z-A] [z-a], 码值小的-码值大的

    // [a-z]  匹配所有的英文小写字母   只能选一个
    // [A-Z]  匹配所有的大写字母     只能选一个
    // [0-9]  0-9只选一个
    // [a-zA-Z0-9]  大小写字母加数字  只选一个
    // [a-zA-Z0-9_] 大小写字母加数字加下划线 只选一个
 console.log(/^[A-Z]$/.test('d')) // false 
    console.log(/^[A-Z]$/.test('D')) // true 
    console.log(/^[a-z]$/.test('i')) // true

```

**取反**

``` js
取反  ^ 
    // 在方括号中的开头写上^, 表示取反  [^]

    // 1. /^[^0-9]$/ 除了0-9以外的任意单个字符
    // 2. /^[^a-z]$/ 除了a-z以外的任意单个字符
    // 3. /^[^abc]$/ 除了abc以外的任意单个字符

    console.log(/^[^0-9]$/.test('a')) // true
    console.log(/^[^0-9]$/.test('9')) // false 
```

**特殊字符.**

``` js	
2. 特殊单字符  . 
    // . 匹配除了换行符之外的任意单个字符
    console.log('---------------')
    console.log(/./.test('22'))
    console.log(/n./.test('n2'))
    console.log(/.n/.test('2n2'))

    console.log(/.n/.test('ab+n'))
```

**字符组简写**

``` js
1. // 字符组简写 小写

    // \d  [0-9]  记忆：digit （数字） 小写 
    // \w  [0-9a-zA-Z_]  单词字符， 表示数字，字母下划线，记忆： word 单词  
    // \s  [ \n\t\v\r\f]   空白字符  意义：space  s

    console.log(/\d/.test('9999')) // 数字
    console.log(/\w/.test('9999')) // 单词 数字字母下划线  
    console.log(/[0-9a-zA-Z_]/.test('9999')) // 单词 数字字母下划线  
    console.log(/\w/.test('word'))

   2. // 排除型字符组简写 大写
    // \D   [^0-9] 除了数字以外的任意单个字符
    // \W   [^0-9a-zA-Z_] 除了这些以外的
    // \S   非空白字符   
```

**修饰符**

``` js
 // 1. 修饰符
    //   约束正则的某些细节行为，比如是否区分大小写。

    // 2. 语法
    //  /表达式/修饰符

    // 3. 
    // 1. i  ignore  忽略   忽略大小写
    // 2. g  global  全局匹配

例子
    console.log(/^java$/.test('java'))
    console.log(/^java$/i.test('jAvA'))
    console.log(/^java$/i.test('JAVA'))
    let str1 = '哈哈，是哈哈，哈哈叫嘻嘻去打哈哈，哈哈是可以去打哈哈'
    let res1 = str1.replace(/哈哈/ig, '***')
    console.log(res1);
```

**正则替换**

``` js
str.replace(正则表达式,'替换为的字符')
//str 是操作的字符串，参数一是匹配要修改的字符，参数二是要把参数一换成什么字符
```



