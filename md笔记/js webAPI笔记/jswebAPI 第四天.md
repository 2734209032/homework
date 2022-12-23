#### 1.实例化对象

**实例化对象的方法**

``` js
1.利用字面量实例化对象
const obj={}
2.利用关键字new
const obj=new Object()
3.构造函数实例化对象
```



``` js
  // 1. 创建对象
        // 字面量的方式创建对象   
        // 字面量  ==>  字面意思，看见{}就知道 哦 这是一个对象 
                //   ==>  []  这个就是一个数组 ，  ''  ==> 字符串
        const obj = {
            name:'贵儿桑',
            age:18
        }

        // 2. 通过new Object()
        const obj2 = new Object({name:'贵儿桑2', age:19})

        // 3. 通过构造函数来创建
        // 构造函数就相当于是一个模板，我们可以把一些公共的属性放到构造函数中
        // 约定：构造函数首字母大写
        function Star(name, age){
            // 固定写法
            this.name = name 
            this.age = age 
        }

        // new 一个对象 
        const ldh = new Star('刘德华', 18)
        const zxy = new Star('张学友', 19)
        console.log(ldh)
        console.log(zxy)

        // 实例化： 通过构造函数创建对象的过程就叫做实例化
        // 实例： 实际的例子，具体的某一个对象
```

---

#### 2.日期对象

** 使用前必须实例化日期对象**  **const date=new Date()**

![image-20221202191641079](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221202191641079.png)

``` js
// 1. new Date() 不传参数       // 得到的是当前的时间
2. // 获取当前的时分秒 另一种方法 toLocaleString()
---
// 1. new Date() 不传参数 
      // 得到的是当前的时间
      const date = new Date()
      console.log(date)

      // 2. new Date() 传参
      // 如果传参，可以得到指定的某个时刻 （时间）
      const date2 = new Date('2022-12-08 00:00:00')
      console.log(date2)
2. // 获取当前的时分秒 另一种方法 toLocaleString()
      const div = document.querySelector('div')

      const date = new Date()
      div.innerHTML = date.toLocaleString()

      setInterval(function(){
        // 每隔一秒，重新获取一下日期对象
        const date = new Date()
        div.innerHTML = date.toLocaleString()
      }, 1000)
```

---



#### 3.时间戳

``` js
 // 时间戳 ===> 邮戳 盖章  独一无二的
      // ==> 当前时间到1970年1月1日 00:00:00 那一刻的毫秒数
获取时间戳的方法
      // 1. date.getTime()
      const date = new Date()
      console.log(date.getTime())


      // 2. +new Date()
      console.log(+new Date())


      // 3. Date.now()
      console.log(Date.now())

      // ==> 推荐使用 +new Date() 可以传入某一个时刻
      const future = +new Date('2022-12-08 09:00:00')     //传参的话就是获取参数里面的时间到1970的总毫秒，一般用来做倒计时
      console.log(future)
      const now = +new Date() // 当前时刻到1970哪个时间点的毫秒数
      console.log(future - now)
公式
    //let d = parseInt(time / 60 / 60 / 24) // 天
    //   let h = parseInt(time / 60 / 60 % 24) // 小时
    //   let m = parseInt(time / 60 % 60) // 分
    //   let s = parseInt(time % 60 )

```

---



#### 4.倒计时实际开发

[dayjs]: https://dayjs.fenxianglu.cn/



``` js

<script src="./dayjs.min.js"></script>
    <script>
        // moment.js 体积稍微大一些 濒临淘汰
        // dayjs  ==> 推荐使用它

        // 1. 引入js文件
        // 2. 根据文档来使用
        const res = dayjs().format('YYYY-MM-DD HH:mm:ss')
        console.log(res)
    </script>
```

---

#### 5.节点

``` js
1.node.parentNode //父节点
2.node.previousElementSibling    // 前一个兄弟元素节点
3.node.nextElementSibling      //后一个兄弟元素节点
4. node.childNodes             // 返回的所有的子节点，得到的是伪数组。注意包括了==> 文本节点
5.节点类型 nodeType
6. node.children   //只返回子元素节点，其余节点不返回
7.node.cloneNode(true)  //克隆节点  当不传参或传false时 ，浅拷贝(只复制标签)，当传true时，深拷贝(既复制标签又复制内容)
8.document.createElement('标签名')  //创建节点
9.node.appendChild(Child)   //在父元素的最后添加节点
10.node.insertBefore(要插入的元素, 放到哪个元素的前面)  还可以上下移动
11.node.removeChild(child) //删除节点 ，只能删亲儿子
```

**node.insertBefore的另一种用法**

![image-20221208190846086](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221208190846086.png)

``` js
//node.parentNode
// 文档 document  一个页面就是一个文档
    // 元素 element  页面上所有的标签都叫元素
    // 节点 node   页面上所有的内容都可以叫做节点   元素节点/文本节点/属性节点/注释节点

    const son = document.querySelector('.son')

    // 父节点 node.parentNode
    // ==> 返回最近的一个父节点, 如果找不到了 返回null
    // 可以多次找爷爷
```

---

#### 6.兄弟节点

``` js
  // 获取ul中第二个li标签
        const li_2 = document.querySelector('ul li:nth-child(2)')
        console.log(li_2)

        // 想获取li_2 
        // 前一个兄弟元素节点
        // 1. node.previousElementSibling
        // previous 前一个 Element 元素  Sibling 兄弟
        console.log(li_2.previousElementSibling)

        // 2. 后一个兄弟元素节点
        // node.nextElementSibling
        console.log(li_2.nextElementSibling)
```

---

#### 7.子节点

``` js
 // ul下的所有li标签
      const lis = document.querySelectorAll('ul li')
      console.log(lis)

      // 1. 子节点   （元素、文本、属性、注释）
      // node.childNodes    node 代表父节点
      // 返回的所有的子节点，得到的是伪数组。注意包括了==> 文本节点
      const ul = document.querySelector('ul')
      console.log(ul.childNodes)

      // 2. 节点类型 nodeType
      console.dir(ul.childNodes[1])
      // console.log(ul.childNodes[0].nodeType)  // 3  ==> 文本节点
      // console.log(ul.childNodes[1].nodeType)  // 1  ==> 元素节点

      // 元素节点 nodeType  1 
      // 属性节点 2
      // 文本节点 3 
      // 注释节点 8 
      
      // 找到元素节点
      for(let i = 0; i < ul.childNodes.length; i++){
        if(ul.childNodes[i].nodeType === 1){
          console.log(ul.childNodes[i])
        }
      }
3. node.children   //只返回子元素节点，其余节点不返回
```

#### 8.移动端

``` js
 移动端的事件，一定要注意切换到移动端
    const div = document.querySelector('div')

    // 1. touchstart 当手指触摸到dom元素的时候触发
    div.addEventListener('touchstart', function () {
      console.log('我触摸到了这个div---touchstart')
    })
    // 2. touchmove 手指在dom元素上移动的时候触发
    div.addEventListener('touchmove', function () {
      console.log('我的手指在这个div上移动---touchmove')
    })
    // 3. touchend 手指离开dom元素了
    div.addEventListener('touchend', function () {
      console.log('我的手指离开了div---touchend')
    })
#### 移动端插件  swiper https://www.swiper.com.cn/
//    1. 先查官网的基础样式，找到自己想要的某种形式，记下编号
    //    2. 在我们下载好的文件中找到demo文件夹，找到具体的哪个html
    //    3. 查看那个html的源代码 

    // ===> 
    //    1. 引入 css / js
    //    2. cv  CSS中的style
    //    3. cv  html结构
    //    4. cv  JS
```





