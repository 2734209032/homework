####  1.// 事件监听的三要素
​      ` ``` //  1. 事件源： 谁， 谁被点击了，谁触发了这个事件   ==> btn  ```
​       ` //  2. 事件类型： 什么事件， 比如这里叫点击事件 ，再比如说键盘按下的事件，鼠标滚动的`事件`
​     ```   //  3. 事件处理程序：我们要干嘛```
​        // 变量声明 语义化一些，看到这个名字，我就直到它是用来干嘛的

---



#### 2.js 代码回收机制
   ``回收机制，当在函数声明一个变量  函数内部声明的这个num变量，当函数执行完后，不再使用了，会`被垃圾回收程序回收掉``
   ` 全局变量是当 页面关闭 时被销毁`

---



#### 3.js注册事件的两种方法及解绑
``` js
// 第一种 dom0
   `` btn.onclick = function () {      //第一种的做法，如果后面再加一个事件，前面的会被最后`面那个被覆盖 相当于重新赋值了
      console.log(1);
    }
1.第一种事件解绑
btn.onclick =null
    // 第二种 dom2
    // 可以给一个事件源添加多个事件，不会覆盖
function fn() {
      console.log(1);
​    }
    btn.addEventListener('click',fn )
2.第二种事件解绑
 btn.removeEventListener('click',fn ) //匿名函数无法解绑
3.事件解绑
<script>
    const btn = document.querySelector('button')
    // 1.传统的注册事件解绑
    btn.onclick = function () {
      console.log(1);
      btn.onclick = null      //相当于重新赋值

    }
    // addEventListener注册事件解绑
    btn.addEventListener('click', fn)
    function fn() {
      console.log(1);
      btn.removeEventListener('click', fn)  //固定写法，第一个参数是事件类型，第二个参数是函数名。匿名函数无法解绑

    }
  </script>
```

---



  ####  4.keydown 注意点
  // 注意：==> keydown里面的回调函数，在我们的文本还没有落入到input框的时候就触发了
        // 比如，第一次输入a, 在a落入到input框之前，监听keydown的这个函数就已经执行了

---



#### 5.回调函数 ：

``` js	
####  
回头再调用的函数 ， 一开始不执行， 间隔时间到了，再回去调用执行的函数 
另一个定义，作为参数传递到另一个函数的函数叫做回调函数
```



---



#### 6.自定义属性
``` js
```<div data-demo-test='666'></div>`      //多个相连，采用驼峰命名获取
const div=document.querySelector('div')
获取自定义属性
方法1： div.dataset.demoTest     
方法2： div.dataset['demoTest']
// 1. div.getAttribute('属性名')   获取自定义属性
// 2. div.setAttribute('属性名', 值)  ==> 设置自定义属性，不用手动在html上添加了
// 3. div.removeAttribute('属性名')  删除自定义属性
```

```js
2.获取自定义属性 element.getAttribute('属性名')

<body> 
    <a href="http://www.baidu.com" target="_blank" person="我也是自定义" data-test="2"></a>
</body>
获取属性值
const  a=document.querySelector('a')
console.log(a.href)  //"http://www.baidu.com"
console.log(a.target)  //"_blank"
console.log(a.dataset)  //2
获取自定义属性
==> element.getAttribute('属性名')
console.log(a.getAttribute( 'demo'))
console.log(a.getAttribute('href')) //"http://www.baidu.com"

console.log(a.getAttribute('target'))
console.log(a.getAttribute('data-test')) data-
```

```js
3.设置自定义属性element.setAttribute('属性名', 值)
// 2. 设置自定义属性
    // 1. 本身自带的属性可以设置
    // 2. 自定属性也可以设置
    // 3. data- 也可以设置
    // ==> element.setAttribute('属性名', 值)
    a.setAttribute('href', 'http://jd.com')
    a.setAttribute('testDemo', '123')
    a.setAttribute('test-emo', '123')
```

``` js
4.移除自定义属性  element.removeAttribute('属性名')
//  移除属性
    // element.removeAttribute('属性名')
    a.removeAttribute('href')
    a.removeAttribute('test-emo')


    // ===>
 总结
    // 1. 获取属性  el.getAttribute('属性名')
    // 2. 设置属性  el.setAttribute('属性名', 值)
    // 3. 移除属性  el.removeAttribute('属性名')

    // data- ==> 如果我们要设置自定义属性，建议大家使用 data-
```

---



#### 6.检测数据类型
``` js
1. typeof
2. instanceof
3. Object.prototype.toString.call()
```

---



#### 7.伪类选择器
<style> 
input：focus{       //css选择器，当input获取焦点时，宽度变为300px
  width:300px;      //如果一个动画既可以css实现，又可以js实现，则推荐css，因为性能更好
}
input:checked{
        //选择复选框选中的元素
    }



</style>

---



#### 8.事件对象 e      

**当事件触发的时候，和这个事件相关的所有信息都存在这个对象中，它叫event， 简写e。**

**=> 事件绑定的时候，回调函数的第一个参数**

``` js
  
ul.addEventListener('click', function(e){ 
    // ==> e.target.tagName 
    if (e.target.tagName === 'LI'){ 
        // 处理逻辑  
    }      
    // e.target.className  类名 
    // 事件对象的常用属性  
    1. e.type  返回事件的类型 
    2. e.target  触发事件的元素 也就是我们点了谁
    3. e.currentTarget  事件源，绑定事件的元素
    4. e.pageX, e.pageY   鼠标在页面文档上的坐标
    5. e.key ==> 判断按下了哪个按键  
    6. e.keyCode ==> ASIIC  也可以判断按下了哪个键，不推荐 
    7.e.pageoffsetX  e.pageoffsetY  鼠标在绑定事件的那个元素中的位置
    // 事件对象需要记住两个方法   
    1. e.stopPropagation()  阻止事件冒泡 
    2. e.preventDefault()   阻止默认行为  
    this ==>  事件源    })
 
})
```

---



#### 9.trim() 去除字符串2侧的空格

---



#### 10.this
``` js
// this 就是一个变量，值是一个对象， 程序运行时内部自动生成的，代表着当前的运行环境。
this的指向，在定义的时候不能确定的，只有执行调用的时候才能确定它的指向。
 粗略规则：谁调用，fn内部的this，就指向谁
 this指向 当前的事件源 
 e.target 是返回当前点击的元素
 e.currentTarget===this //true    都是返回当前事假源，或当前调用函数的对象
// 1. 全局作用域 / 普通函数调用 / 定时器    this ==> window
// 2. 函数作为对象的方法调用   ==> 谁调用，指向谁  
objconst obj = { 
fn: function()
    {console.log(this)  
 }
}
obj.fn()
// 3.  事件注册  this指向的就是事件源，给谁绑定 指向谁
4.箭头函数中的this指向
箭头函数本身没有this，它的this指向的是上层作用域中的this，上层没有的话就一直向上去查找
```

---



#### 11.作用域 

``` js
 全局作用域/局部作用域(函数作用域)/ 块级作用域
{}就算一个作用域，除了对象的{},其他都算一个作用域
```

---



#### 12.forEach



``` js
 #### forEach

  arr.forEach(function (value, index, arr1) {    //forEach 接收 3个参数 第一个参数是数组的每一个元素，第二个参数是所有数组元素的索引号，第三个参数是返回原数组
```

---



####  13.arr.includes(数组元素)
``` js
判断数组中是否包含某个元素
// arr.includes()
        // 作用：判断一个数组是否包含一个指定的值，有，返回 true，否则返回 false。
```

---



#### 14.事件流
``` js
// 事件流： 事件执行过程中的流动路径。
    // 事件流描述的是元素在页面中接收事件的顺序。
    事件流有三个阶段 1.捕获阶段 2.当前目标阶段 3.冒泡阶段
      // div.addEventListener(type, listener, useCapture);
    // 1. type 事件类型
    // 2. listener 回调函数
    // 3. useCapture 是否使用捕获 如果使用，传true, 否则 false (如果这个参数不传，默认是false)不传参 默认就是冒泡
   `` 阻止冒泡 e.stopPropagation()`
  `` 阻止默认行为  e.preventDefault()`
```

---



#### 15.mouseenter  mouseleave  和mouseover  mouseout的区别

``` js
// 鼠标经过事件，鼠标离开
mouseenter  mouseleave 没有事件冒泡的
const father = document.querySelector('.father')
father.addEventListener('mouseenter', function(){console.log('鼠标经过了|)}
father .addEventListener( 'mouseleave', function(){ [console.log('鼠标离开了)}
鼠标经过事件 离开事件
==> 有事件冒泡(事件再传播，从内到外)mouseover mouseout
father.addEventListener('mouseover', function()!console.log('鼠标经过了·)
father .addEventListener('mouseout' function()console.log('鼠标离开了·)
事件在传播，son这个盒子也有mouseover这个事件，只是我们没有监听它而已，这个mouseover这个事件向上传播（冒泡）到father这个盒子，监听到了这个事件，所以打印log一句话
                                                          /// 事件一直在DOM元素之间传播，虽然没有给son绑定mouseover这个事件，但是经过这个son盒子的时候，也触发了mouseover，
      // 然后这个事件往上冒泡，被father监听到了,然后father上有一个注册的事件 就触发了
<script>
```

---



#### 16.事件委托

``` js
事件委托的原理:利用事件冒泡，我们给父元素绑定事件，当点击了子元素冒泡到父元素上，父元素有事件，触发事件
==> 触发事件的元素e .target==> 绑定事件的元素
this
e.currentTarget ==> 绑定事件的元素
/e.target.tagName === 标签名 (大写) 用它来判断点击的是否是某些标签
也可以用e.target.className==='类名' 来判断是否点击的某些标签
  事件委托的好处： 减少注册事件的次数 提高程序的性能
```

---



#### 17.页面加载事件

``` js
1.window.addEventListener('load'){
}            //当页面的所有资源包括外联的资源全部加载完毕，再执行里面的代码
```

``` js
2.document.addEventListener('DOMContentLoaded', fn)
             //仅当DOM元素加载完成，执行里面的代码
```

#### 18.定时器

``` js
let n=setInterval(function(){
    
},1000)
1.停止定时器
clerInterval(n)
```





## 今日单词

| 单词             | 说明                         | 解释 |
| :--------------- | ---------------------------- | ---- |
| mouseenter       | 鼠标经过事件                 |      |
| mouseleave       | 鼠标离开事件                 |      |
| e.target.tagName | 点击当前元素的标签名（大写） |      |
| click            | 点击                         |      |
| e.key            | 用户按下了键                 |      |
| keyup            | 键盘弹起触发                 |      |
| keydown          | 键盘按下触发                 |      |
| focus            | 获得焦点事件                 |      |
| blur             | 失去焦点事件                 |      |

