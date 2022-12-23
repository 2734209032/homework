#### 1.查文档步骤

1. 语法， 先大致了解

2. 作用， 看这个方法是干嘛的 

3. 参数， 熟悉参数

4. 返回值，看这个方法是否有返回值

5. 描述  注意事项

6. 示例代码  自己尝试一下 

---

#### 2.原型的五大规则

``` js
// 语法糖
// const obj = {}   ===>  const obj = new Object()
// const arr = []      ===>  const arr = new Array()

 1. 所有的引用类型（数组对象函数），都具有对象的特性，可以自由的扩展属性。
const obj = {}        // obj.a = 1 
const arr = []        // arr.b = 2
const fn = function(){}   // fn.c = 3

 2. 所有的对象，都有一个__proto__属性，属性值是一个普通的对象。 （__proto__ 隐式原型）
console.log(obj.__proto__)
console.log(arr.__proto__)
console.log(fn.__proto__)

 3. 所有的函数，都有一个prototype属性，属性值也是一个普通的对象  (prototype 显示原型)
console.log(fn.prototype)   

 4. 所有对象的隐式原型（__proto__） 指向它的构造函数的显示原型（prototype）
obj.__proto__ === Object.prototype
arr.__proto__ === Array.prototype
fn.__proto__ === Function.prototype

 5. 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__中寻找
```

#### 3.静态方法

1. 静态方法是构造函数本身上的方法
2. 只有构造函数本身能调用
3. 静态方法中的this指向构造函数

``` js
  function Person(name, age){
            this.name = name 
            this.age = age 
        }
        const p = new Person('淞桑', 6)
        console.log(p)
        // Person 是构造函数 ，它也有对象的特性，可以自由扩展属性和方法
        Person.sayHi = function(){
            console.log('hi')
            // console.log(this) // 指向的是构造函数
        }
        console.dir(Person)

        // 静态方法：给构造函数本身上添加的方法
        Person.sayHi()
        // 相当于是Person调用的这个sayHi，所以sayHi里面的this 指向的是Person
```

#### 4.构造函数存在的问题以及解决办法

1. 存在的问题：浪费内存

   ``` js
     // 构造函数存在浪费内存的问题（方法）
           function Star(name, age){
               this.name = name 
               this.age = age 
               this.sing = function(){
                   console.log('唱歌')
               }
           }
           const kk = new Star('坤坤', 18)
           const jl = new Star('杰伦', 20)
           console.log(kk)
   
           kk.sing()
           jl.sing()
           console.log(kk.sing === jl.sing) // false
           // 每创建一个对象，都会在堆内存中新开辟一个空间，存储方法
           // 这个时候，就存在浪费空间的问题。
   ```

   

2. 解决办法：将实例的方法放到构造函数的原型对象上

``` js
  function Star(name, age){
            this.name = name 
            this.age = age 
        }
        // 公共的方法写到原型上
        Star.prototype.sing = function(){
            console.log('唱歌')
        }
        const ldh = new Star('刘德华', 20)
        const zxy = new Star('张学友', 18)
        ldh.sing()
        zxy.sing()

        // sing是一个方法，引用类型，比较的是地址是否相等，是否是同一个对象
        console.log(ldh.sing === zxy.sing) // true 表示内存上是同一个方法

        // ==> 公共的属性，定义到构造函数里面
        // ==> 公共的方法，定义到原型上
```

#### 5.原型

``` js
 原型：原型就是一个对象，也叫原型对象。
        // 原型对象 prototype(显式原型)

        // 1. 所有的函数，都有一个prototype属性（显式属性），这个属性是一个指针，指向原型对象。
        // 指针：地址，门牌号
        function Star(){}
        console.dir(Star)

        // 原型对象 // prototype这个属性值指向的对象，就是原型对象
        // Star.prototype = {
        //     constructor: Star
        // } 

        // 2. 原型对象上默认有一个constructor属性，指向构造函数本身

        // 3. 我们可以往这个原型对象上添加属性和方法。所有通过构造函数创建的实例，都共享原型上的属性和方法

        Star.prototype.sing = function(){
            console.log('sing')
        }
        console.dir(Star)
```

---

#### 6.构造函数和原型对象的方法this指向

1. 构造函数中的this.name 就已经说明了，当new时，构造函数内部将this指向实例了
2. 而原型中的方法，调用是实例.方法，所以原型对象中的this指向实例

``` js
  let that 
        function Star(name){
            this.name = name 
            console.log(this)
            that = this
        }

        // 当我们new执行完之后，this是不是就会被释放掉了，是释放的了
        // 我们可以声明一个全局变量，来存this, 最后再看that是不是等于我们的实例

        const ldh = new Star('刘德华')
        console.log(that)
        // const zjl = new Star('周杰伦')
        // 1. 构造函数里面的this指向的是实例对象


        // 2. 原型对象的方法中，this指向 还是实例对象 
        Star.prototype.sing = function(){
            console.log('sing唱歌')
            console.log(this)
        }
        ldh.sing()
```

#### 7.constructor属性及应用

**每个原型对象都默认有一个constructor属性，指回构造函数本身**

``` js
  function Star(name,age){
            this.name = name 
            this.age = age 
        }
        const xss = new Star('小淞桑', 20)

        console.dir(Star)

        // 1. 每个原型对象上都默认有一个constructor属性，指回构造函数本身的。
        console.log(Star.prototype.constructor === Star)

        // ==> 表示我这个原型，和哪个构造函数相关联，是哪个构造函数的原型

        // 2. 实例的隐式原型 等于 构造函数的显式原型
        xss.__proto__ === Star.prototype
```

**应用**

利用这个属性让其重新指回该构造函数

``` js
 // 如果我们直接给原型对象赋值一个对象，相当于整个替换了原型对象里面的所有内容，
        // 原型内的constructor就丢失了。那我们也就不知道这个原型是和哪个构造函数相关联了
        // 所以，可以手动的利用constructor指回原来的构造函数
        Star.prototype = {
            constructor: Star, // 手动添加回来
            sing: function(){
                console.log('sing')
            },
            dance: function(){
                console.log('跳舞')
            },
            rap: function(){
                console.log('rapper')
            }
        }
```

---

#### 8.隐式原型 __proto__

``` js
 function Star(name, age){
            this.name = name 
            this.age = age 
        }
        // 公共方法写在原型上
        Star.prototype.sing = function(){
            console.log('我会唱歌')
        }
        const ldh = new Star('刘德华', 18)
        // ldh.sing()
        console.log(ldh)
        // 1. 方法属性的查找规则 
        // 首先看ldh这个对象身上是否有sing方法，如果有，就执行对象上的这个方法。
        // 如果没有sing这个方法，就会通过__proto__去实例的原型上查找。

        // 2. __proto__隐式原型
        // 实例通过__proto__ 访问（链接）到了它的原型对象
        // ==>  ldh.__proto__  ===> 访问到了原型
        // ==>  Star.prototype ===> 访问到了原型
        ldh.__proto__ === Star.prototype

        // 3. __proto__ 它就相当于是一个桥梁， 我们创建的实例、对象，可以通过它访问原型。
        // 表示 实例与原型(对象)之间的一个关系
        // ldh（实例）   ===>    Star.prototype (原型)

        // ==>  实例对象.__proto__ === 构造函数.prototype
```

---

#### 9.构造函数 实例 原型对象 关系

1. 当new时，构造函数实例化了对象
2. 构造函数中的prototype属性指向原型对象
3. 原型对象里面有constructor属性指回构造函数
4. 实例中的隐式原型(__proto_)指向构造函数的原型对象

``` js
  // 构造函数-实例-原型（对象）
        function Person(name){
            this.name = name 
        }
        const person = new Person('贵儿桑')
        // 四条线 
        // 1. 构造函数有prototype属性，指向原型对象
        // 2. 原型对象默认有一个constructor属性，指向构造函数
        // （构造函数和原型相互指向）

        // 3. 构造函数 new 创建一个实例
        // 4. 实例通过__proto__访问到原型（对象）
        // 高程四 P250 : 实例与原型之间有直接的联系(__proto__)，但实例与构造函数之间没有。
```

![image-20221223185156067](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221223185156067.png)