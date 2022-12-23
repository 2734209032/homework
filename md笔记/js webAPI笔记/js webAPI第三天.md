 #### 1.页面滑动效果 

就是做返回顶部，让画面带点动画效果

``` css

/* 让页面是滑动的效果 */
html {
  scroll-behavior: smooth;
}
/*滤镜*/
 html {
    /* filter: blur(10px);      变模糊 */
    /* filter: saturate(1)      饱和度*/
    /* filter: grayscale(1);       全页面变灰色 */
  }
```

---

#### 2.属性选择器

``` css
1. input[value]{       /* 这句话的意思是只选择input 带有value属性的input*/
color:red
}
2. input[type=text]{   
     color:red                     /* 这句话的意思是只选择input 带有type属性且属性值等于text的input*/
}
 属性选择器
 //<input type="text" value="123" data-id="0" data-name="andy">
 // <input type="password">
      // 1. 先写标签名[] []方括号里面写上属性
      const input = document.querySelector('input[type="password"]')
      console.log(input)

      // 2. [] 方括号中的引号可以省略  ==> 如果属性值是数字，不能省略引号
      const input2 = document.querySelector('input[type=text]')
      console.log(input2)

      // 3. 可以直接写属性，不要标签名
      const input3 = document.querySelector('[data-name=andy]')
      console.log(input3)

      // 4. 单独写属性名，不写属性值
      const input4 = document.querySelector('[data-id]')
      console.log(input4)

      // ==> 方括号一定要写，属性选择器 []
```

---

#### 3.各大属性 scrollTop 和offsetTop



![image-20221130191557808](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221130191557808.png)



``` js
1 常用的话 scrollTop常用于获取页面滚动了多少
window.addEventListener('scroll', function () {
     1. console.log(document.documentElement.scrollTop)
    2.window.pageYOffset  //只可读，不可写，就是说不能设置
    })
```



``` js
2. offsetTop
const div = document.querySelector('div')
    console.log(div.offsetTop);
//这句话的意思是获取div距离自己带有定位的父级的上偏移，没有的话就以body为准
```

``` js
3. //视口==> 可视区域的窗口
    //getBoundingClientRect()
    //返回的是一个对象
    // width=width+padding+border
    //这个方法是根据视口来断定 top left的
    const div = document.querySelector('div')
    console.log(div.getBoundingClientRect());
    2. element.getBoundingClientRect()
方法返回元素的大小及其相对于视口的位置的对象
```



#### 4.隐式转化

1. ++  --   一元运算符 可以把其他数据类型隐式转换为number

2. 在其他数据类型加个+ 号也能隐式转换为number  ：true：1，false：0，null：0，undefined：NaN

3. 任何和字符串相加的数据类型，都会被隐式转化为字符串类型

    

---



#### 5.scroll事件

1. **scroll 对于window 和document 能生效**

   1. **对于获取页面被卷去的头部 用1.document.documentElement.scrollTop (获取html) 2. window.pageYOffset  **

   ``` js
   1. window.addEventListener('scroll', function(){
           const n = document.documentElement.scrollTop
           const m = window.pageYOffset  
           console.log(n, m)
           // console.log(n)
           // console.log(typeof n) // number 不带单位
   
           // 1. scrollTop 的返回值是number类型，不带单位
         })
   
         // 2. scrollTop 是可读写的 , 也可以设置值
         document.documentElement.scrollTop = 900
         页面被卷去的头部   //这两种都能获取页面被卷去的头部
         document.documentElement.scrollTop
         window.pageYOffset  //只可读，不可写，就是说不能设置
   ```


---



#### 6.滚动特效

``` js
// 点击返回顶部 
    const backTop = document.querySelector('#backTop')
    backTop.addEventListener('click', function(){
      // 1. scrollTop 是可读写的
      // document.documentElement.scrollTop = 0

      // 2. 平滑滚动
      window.scrollTo(x-coord,y-coord )
      // 接收两个参数，x横坐标，y纵坐标 
      window.scrollTo(0, 0)
      // 设置滚动行为改为平滑的滚动
      window.scrollTo({
          top: 0,
          behavior: "smooth"
      })

      // 3. window.scroll(x, y)  
      //    window.scroll({})
      window.scroll({
          top: 0,
          behavior: 'smooth' // safari 不支持平滑
        })

    })
```

``` css
  /* 让页面是滑动的效果 */
html {
  scroll-behavior: smooth;
}
```

---



#### 7.resize事件和clientWidth

``` js
//resize事件 检测屏幕变化触发事件
3. const div = document.querySelector('div')
    console.log(div.clientWidth);      //clientWidth返回的是盒子内容大小加padding 不含边框
    window.addEventListener('resize', function () {
      let n = document.documentElement.clientWidth
      console.log(n);

    })
```

---



#### 8.立即执行函数

``` js
1. 立即执行函数的两种写法
1. //第一种写法  
(function(){})()              //多个立即执行函数 用;隔开
2.//第二种写法
(function(){}())
立即执行函数的作用  ： 创建一个独立的作用域，防止变量名冲突，避免变量污染
立即执行函数中的this指向window
没有事件对象
```

``` js
//扩展
 6. 注意，特例
        ;(function(){
            // 如果立即执行函数(包括普通函数)中的这个变量，不用关键字声明, 这个变量会成为window对象的属性 全局变量
            abc = 77
            console.log(abc)
        })()
        console.log(window.abc)  //77
```

---



#### 9.var let const 扩展

``` js
  var let const
        const ab = 100
        let abc = 200
        var abcd = 300

        // function fn(){
        //     console.log(ab)
        //     console.log(abc)
        //     console.log(abcd)
        // }
        // fn()    // fn其实也是window上的方法  因为调用的话其实是window.fn()
        console.log(window.ab)
        console.log(window.abc)
        console.log(window.abcd)
        // console.log()

        // 1. let / const 声明的变量，不会挂载到window对象上  挂载 ==> 成为window对象的属性
        // 2. 全局作用域下var声明的变量会 挂载到window对象上
        console.log(window)


        function abcde(){
            console.log('我是函数')
        }
        console.log(window)

        // 3. 用function声明的函数，也会挂载到window对象上

        const abcdef = function(){
            console.log()
        }
        console.log(window)

        // 4. 本身window对象上就有 name，top等属性，不建议使用var声明这类变量名
        var name = 123
        var top = 333
```

---



####  10.什么时候加分号

``` js
//34. 什么时候加分号
        // 没有应该不应该，只有你自己喜欢不喜欢  -- 尤雨溪
        // 真正会导致上下行解析出问题的 token 有 5 个：括号，方括号，正则开头的斜杠，加号，减号。

    // 1. ()
    // 2. []
    // 3. / 
    // 4.  +
    // 5. -

    // 只需要记住这两种情况 () [] 开头，给我们的代码加上分号
    // ;()
    // ;[]

    const arr = [1, 2, 3]
    arr.forEach(function(el){
        console.log(el)
    })

    ;[3, 4, 5].forEach(function(el){
        console.log(el)
    })

```







# 今日单词

| 单词 | 说明 | 解释 |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |
|      |      |      |

