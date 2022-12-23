#### 1.作用域

``` js
1.js作用域分为全局作用域
2.局部作用域（函数作用域和块作用域）
 // 函数作用域，在函数内部声明的变量，只能在函数内部被访问
 //函数内部未声明直接赋值的变量，是全局变量，会挂载到window上
 // 函数的参数，相当于函数内部的局部变量
 // 块作用域：在 JavaScript 中使用 `{}` 包裹的代码称为代码块，
  //   使用let/const声明的变量，在{}中就会产生块级作用域。
```

``` js
 for (var i = 0; i < 5; i++) {
      console.log(i);

    }
    // console.log(i);

    console.log('-------------------------------');
    for (let i = 0; i < 5; i++) {
      console.log(i);

    }
     // 1. var 命令的变量提升机制，var 命令实际只会执行一次。
     // 2. let 命令不存在变量提升，所以每次循环都会执行一次，声明一个新变量（但初始化的值不一样）。
     // 3. for 的每次循环都是不同的块级作用域，let 声明的变量是块级作用域的，所以也不存在重复声明的问题。
     // 4. let生命变量的for循环里，每个匿名函数实际上引用的都是一个新的变量

```

**var let const 区别**

1. let const 可以形成块作用域，var不可以
2. let  const 是不存在变量提升的，var可以
3. let const 不能重复声明 ，var可以
4. let const 不能再声明之前使用（暂时性死区），var可以
5. const 声明变量的同时必须赋初始值

#### 2.作用域链

**定义**

变量查找机制，先从当前作用域查找，如果没有就往上一级查找，一直查找到全局作用域（就近原则）

``` js
 // 作用域链本质上是底层的变量查找机制，
    //   在函数被执行时，会优先查找当前函数作用域中查找变量，
    //   如果当前作用域查找不到则会依次逐级查找父级作用域直到全局作用域
    //   let a = 1
    function f() {
      // let a = 2
      function g() {
        //   a = 3
        console.log(a)
      }
      g()
    }
    f()
```

#### 3.垃圾回收机制

**垃圾回收机制**

 垃圾回收机制（garbage collection）简称GC， JS中内存的分配和回收是自动完成的，内存在不使用的时候会被JS引擎/垃圾回收程序自动回收。

**内存泄漏**

内存泄漏: 不再使用的内存，没有及时的释放。

1. 全局变量在页面关闭的时候会被回收

2. 函数里面的变量当函数调用完就回收

``` js
 // 全局的变量，会在页面关闭的时候，被回收
    let num = 10
    // 局部的变量：
    for (let i = 0; i < 4; i++) {
      // 块作用域，是每执行一次，回收一次
    }
    function fn() {
      const str = '你阳了吗'
      console.log(str)
      // 在函数被调用完毕的时候，就会被回收
    }
    fn()
    fn()
    fn()
```

**引用计数法**

``` js
<script>
    // 如何判断内存不会被使用了=>垃圾回收算法
    //   1. 引用计数法 （淘汰）
    //   2. 标记清除法 （主流）

    //   引用计数法
    // 1. 跟踪记录每个值被引用的次数
    // 2. 如果这个值被引用了一次，那么就记录次数1
    // 3. 多次引用会累加
    // 4. 如果减少一个引用就减少1
    //   5. 如果引用次数是0，则释放内存
    //   const person = {
    //     name: '黑马',
    //     age: 20,
    //   }
    //   const p = person
    //   person = 1
    //   p = null

    // 缺陷：循环引用：
    //   堆内存空间中的对象 互相引用，计数永远不能为0，无法被回收，内存泄漏
    function fn() {
      let a = {}
      let b = {}
      a.xx = b
      b.yy = a
    }
    fn()
  </script>
```

**标记清除法**

从根元素开始查找，也就是从全局作用域开始查找，如果查找得到的话，就不会销毁，标记为活动对象，查找不到就销毁，标记为非活动对象

``` js
// 标记清除算法
    // 主要将GC的过程分为两个阶段
    // 1. 标记阶段：标记空间中的活动对象和非活动对象
    // 2. 清除阶段：回收非活动对象，也就是销毁非活动对象

    // 标记阶段从一组根元素开始，
    // 递归遍历（一层一层的）这组根元素，
    // 在这个遍历过程中，能访问到的元素称为活动对象，不能访问到的可以判断为垃圾数据。
    function fn() {
      let a = {}
      let b = {}
      a.xx = b
      b.yy = a
    }
    fn()
    //   缺陷：内存碎片化
    //   解决：标记整理（Mark-Compact）算法
    //从根元素开始查找，也就是从全局作用域开始查找，如果查找得到的话，就不会销毁，标记为活动对象，查找不到就销毁，标记为非活动对象
```

#### 4.闭包

 闭包：内层函数引用外层函数中的变量的集合

  闭包=内层函数+外层函数的变量

``` js
// 外部作用域没办法直接访问内层的变量
    //   function out() {
    //     let a = 10
    //   }
    //   out()
    //   console.log(a)

    // 可以让外部作用域访问到函数内部的变量
    function out() {
      let a = 10
      function inner() {
        console.log(a)
      }
      return inner
    }
    //   fn===>out()===>inner() {
    //       console.log(a)
    //     }
    let fn = out()
    fn()
```

闭包的作用：

1. 延伸变量的范围
2. 实现变量的私有化

**闭包的缺陷**

内存泄漏

``` js
 // 闭包产生的问题：
    //  fun全局的，页面内没有关闭的时候，fun不会被销毁，
    // 一路按照箭头的顺序。i是可以从根节点找到的，
    // 所以会被标记清除法标记为活动对象，所以不会被回收，
    // 所以内存泄漏
    //   闭包的缺点：内存泄漏
    function gn() {
      let i = 0
      return function fn() {
        i++
        console.log(i)
      }
    }
    let fun = gn()
    fun()
```

#### 5.函数提升

1. 函数用function声明的函数才存在函数提升在当前作用域的顶部，用函数表达式声明的函数不会提升，因为其本质是声明变量的过程，只不过值是函数而已

2.  function声明的函数，会被提升到当前作用域的最前面

3.  表达式的函数，如果是var声明的，只提升声明，不提升赋值（必须先声明和赋值，再调用）

4. let const 声明的函数必须先声明再调用

---



#### 6.arguments

``` js
  // arguments他是函数独有的，内置的（默认就有的）一个对象
    // 伪数组：属性名为索引，有length，没有pop push等数组的方法
    //   它接收了函数调用的时候 传过来的所有实参
    function sum(a, b, c, d, e) {
      console.log(arguments)
      console.log(arguments.length)
      let count = 0
      for (let i = 0; i < arguments.length; i++) {
        count += arguments[i]
      }
      console.log(count)
      // 错误演示：
      // arguments.push(999)
    }
    sum(1, 2, 3, 4, 5)
    sum(1, 2)
    sum(1, 2, 3, 4, 5, 6, 7, 8, 9)
```

#### 7.剩余参数

``` js
 // 剩余参数
    // ...变量名
    // arr是一个真数组，存的是剩下的实参
    // ...arr只能放在形参位置的最后面

    function fn(...arr) {
      let sum = 0
      arr.forEach(el => sum += el)
      console.log(sum);

    }
    fn(1, 2, 3, 4, 5, 3, 6, 4,)
    fn(1, 2, 3, 4, 5, 3, 6, 4,)
```

#### 8.扩展运算符

**作用**

1. 求最大最小值
2. 合并、复制数组
3. 用途3 ：展开字符串
4. 伪数组转换为真数组

``` js
 // 扩展运算符：...
    let arr = [2, 3, 4, 5]
    //   console.log(arr)
    //   console.log(...arr) // 2 3 4 5
    // 用途1：求最大最小值
    console.log(Math.max(3, 4, 2, 5, 6))
    let arr1 = [3, 4, 5, 6, 7, 8, 9]
    console.log(Math.max(...arr1))

    // 用途2：合并、复制数组
    //   const a1 = [2, 3]
    //   const a2 = a1
    //   a2[0] = 999
    //   console.log(a1) // [999,3]
    const a3 = [5, 6, 7]
    const a4 = [...a3]
    console.log(a4)
    a4[0] = 888
    console.log(a3)

    const a5 = [5, 6, 7]
    const a6 = [8, 9, 10]
    const newArr = a5.concat(a6)
    console.log(newArr)

    const a7 = [...a5, ...a6]
    console.log(a7)

    // 用途3 ：展开字符串
    const str = 'hello world'
    console.log(...str)
    //   字符串的反转
    console.log(str.split('').reverse().join(''))
    console.log([...str].reverse().join(''))
    //   const str1 = 'h?e?l?l?89dw?d'
    //   console.log(str1.split('?'))

    //   用途4:伪数组转换为真数组
    const divs = document.querySelectorAll('div')
    console.log(divs)
    const divs1 = [...divs]
    console.log(divs1)
    divs1.push(666)
    const divs2 = Array.from(divs)
    console.log(divs2)

    //   伪数组转换成真数组：
    //   1:...
    //   2:Array.from
```

#### 9.箭头函数

```js
1. 基本语法
const fn1 = () => {
      console.log(1);

    }
    fn1()
 2.传参
    const fn2 = (x) => {
      console.log(x)

    }
    fn2(2)
   3.只有一个形参的时候可以省略小括号
    const fn3 = x => {
      console.log(1);

    }
    4.函数体里面只有一行代码时可以省略大括号
    const fn4 = x => console.log(x);
    5.当箭头函数需要返回一个对象时，如果要简写，需要把对象用小括号包裹起来
    const fn5 = x => ({ name: xxx })
    6.箭头函数里面没有arguments，没有绑定this，this的指向是当前作用域this的指向，或上一级作用域this的指向
    7.箭头函数中的this指向
     // 普通函数的this：谁调用它，指向谁（跟函数定义的位置无关）
    // 箭头函数的this：没有自己的this，取决于函数定义的位置（与谁调用它无关），
    // 即包裹该箭头函数的第一个普通函数的this，没有包裹它的普通函数，则指向window
```

#### 10.数组解构赋值

``` js
 // 解构赋值：es6允许我们按照一定的模式，从数组、对象中提取出值然后赋值给对应的变量
    // 如果不加let /const关键字，相当于就是var声明的，会成为window的属性，挂到全局
    const arr = [1, 2, 3, 4, 3]
    const [a, b, ...c] = arr
    console.log(a, b);
    //解构赋值，es6允许我们按照一定的模式，从数组、对象中提取出值然后赋值给对应的变量
    // 交换两个变量的值
    let hh = 66
    let ff = 88
      ;[ff, hh] = [hh, ff]
1.注意点
// 右侧不是数组的时候 会报错
    //   let [kk] = 20
    //   console.log(kk)
    //   let [ss] = true
    //   let [vv] = {}
    //   let [ll] = undefined
    //   let [rr] = NaN
2.解构的时候可以设默认值
const arr=[2,3]
const [a=1,b=2]=arr //当arr中，没有这个值时，则a，b就是默认值，有值的话就会覆盖掉默认值
```

#### 11.对象的解构赋值

``` js
  const obj = {
      name: '仙女',
      age: 18,
     yi: {
      pre:12
  }
    }
    let age = 19
    //以前拿对象的属性是用obj.name
    // 对象的解构赋值，是按照属性名来解构的，可以交换位置
    // 解构属性的时候重命名，语法=>旧属性名:新属性名
    const { age: newage, name:uname } = obj     //在解构的同时也能修改变量名 ，name:uname 
    const {yi:{pre}}=obj
```

#### 12.构造函数

**构造函数实例化对象**

``` js
 // 构造函数
    // function 构造函数名(形参1,形参2,形参3) { // 构造函数的形参与对象的普通属性是一般一致的
    //     this.属性名1 = 形参1;
    //     this.属性名2 = 形参2; // 属性的值，一般是通过同名的形参来赋值的
    //     this.属性名3 = 形参3;
    //     this.方法名 = function(){
    //     };
    // }
    // // 调用
    // const obj = new 构造函数名(实参1，实参2，实参3)
    构造函数 相当于一个模板（雪糕的模具）,可以创建一系列具有相同属性名和方法的对象
     实例化：通过构造函数创建对象的这个过程=>new一个对象的过程
     实例：创建好的这对象
     实例对象是相互独立 互不影响的（一个妈生了多个孩子）
```

1.  实例化： 通过构造函数创建对象的过程，实例化
2.  实例: 创建好的那个对象，具体的对象，叫做实例

**构造函数注意点**

1.  构造函数名字首字母一般要大写（为了从视觉上区分构造函数和普通函数）

2.  构造函数里 属性和方法前面必须添加 this

  3. 构造函数不需要 return 就可以返回结果（构造函数的返回值即为新创建的对象）

4. 我们调用构造函数 必须使用 new

---



**new的执行过程**

new 执行过程 当我们执行new的时候，会去执行构造函数里面的代码

 new的执行过程？

1、创建一个空对象{}

2、让this指向这一个空对象：

3、给这个空对象 添加属性和方法

4、 返回这个对象

---

**实例成员和静态成员**

1.实例成员：在实例上(对象)的属性和方法叫实例成员，只能实例自己访问，构造函数访问不了

2.静态成员：在构造函数本身的属性和方法叫静态成员，只能构造函数本身访问  静态成员中的this指向构造函数本身

```js
 // 实例成员
    // 实例对象中的属性和方法称为实例成员
    // 实例成员 只能通过实例本身（生成的那个对象）访问
    function Person(age) {
      this.name = 'ddd'
      this.age = age
      this.sayHi = function () {
        console.log('哈哈哈')
      }
    }
    const p1 = new Person(18)
    // 访问实例成员
    console.log(p.name)

    // 静态成员(直接加在构造函数本身的属性和方法)
    // 静态成员 只能通过构造函数本身访问
    Person.demo = '我是给构造函数添加的静态属性'
    Person.sayHi = function () {
      console.log('hello')
      console.log(this) // 静态成员中的this指向构造函数本身
    }
    console.dir(Person)
    Person.sayHi()

```
#### 13.基本包装类型

就是js本身自带的一些构造函数 Array Object String Number 上自带的静态属性或方法

``` js
 let str = 'abcd'
    str.includes('bc') // true
    str.length // 4
    let num = 123.56
    // toFixed:保留几位小数，四舍五入，返回的是一个字符串（不是数字）
    console.log(num.toFixed(1)) // 123.6
    // 基本包装类型
    // js底层，将基本数据类型，包装成了一个复杂数据类型（对象）
    // toFixed:保留几位小数，四舍五入，返回的是一个字符串（不是数字）
 // 基本包装类型
 // js底层，将基本数据类型，包装成了一个复杂数据类型（对象）
```

#### 14.引用类型的注意点

``` js
 const divs = document.querySelectorAll('div')
   console.log(divs);
     const div1 = [...divs]
     console.log(div1);//这里有666
     div1.push(666)   //数组是引用类型，虽然push在下面，当console时，打印了，当执行完push后，只要操作数组就会实时更新
     div1[0] = 1
```

