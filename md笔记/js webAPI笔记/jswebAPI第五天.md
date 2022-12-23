#### 1.本地储存localStoragr

``` js
1.生命周期
/生命周期，一个对象创建到清除的过程，这个数据存在的周期
//存储大小 5M
 生命周期:数据是永久存在的，除非我们手动删除，或者卸载浏览器
// 2. 数据共享： localStorage的数据可以多窗口共享，同一个浏览器，同一个域名（地址）
// 3. 数据以键值对的形式，存储在浏览器中。 存的数据的类型 ==>  字符串
 2.扩展
  vle[i].value?.trim()    如果 vle[i].value没有就是undefined 不能用trim()方法，加个问号就是，如果有才用这个方法
```

``` js
1. 存数据 localStorage.setItem('key'，value) (如果key存在，修改数据')
2.获取数据 localStorage.getItem('key')
3.删除数据 localStorage.remove('key')
4. localstorage.clear()  全部删除
```

``` js
面试题
 如果问 localStorage 和 sessionStorage 的区别？
        // 1. 生命周期 一个是永久存在， 一个是关掉页面就不存在了（sessionStorage）
        // 2. 数据共享  localStorage 多个窗口数据共享的（同一个浏览器同一个地址）， sessionStorage 只在当前窗口下数据共享
        // 3. 他们的大小都是5M
```

#### 2.map()

``` js
let newarr=arr.map(function(el,i){
   return el+10        
})
map()方法 用于主要操作数组
1.el是arr中的每一个数组元素
2.i 是索引号
3.必须return 返回每个操作完后的新数组元素
4.返回值是操作过的新数组，需要接收
```

#### 3.箭头函数

``` js
 // 1.箭头函数
    const fn1 = () => {
      console.log(1);
    }
    fn1()
    // 2.如果只有一个形参，小括号可以省略
    const fn2 = b => {
      console.log(b);
    }
    fn2(2)
    // 3.如果只有一行代码，我们可以省略大括号{}  和省略return
    const fn3 = b => console.log(b);

    fn3(2)
    4.箭头函数可以直接返回一个对象，但是需要小括号把返回的对象包裹起来
    const fn = name => ({username:name})
    fn('xii')
    ``` css
//     箭头函数本身没有this，它的this指向的是上层作用域中的this
//  作用域 ： 全局作用域/局部作用域(函数作用域)/ 块级作用域
// 对象没有作用域
```

#### **4.js 线程和进程**

``` js
JS 是一门单线程的语言  
        // 同一时间只能做一件事，前一件事情做完了，才做下一件事情。

        // 为什么JS是一门单线程的语言呢？
        // JS设计之初为了操作DOM元素的， 我们不能同时去添加或者删除同一个DOM.

        // 2. 线程 和 进程 
        // 线程 ： thread  是操作系统能够进行运算调度的最小单位
        // 进程 ： process 是系统进行资源分配和调度的基本单位
        
        // 进程 ==> 可以理解为正在运行着的程序 
        // 线程 ==> 程序中不同的小任务
        // 进程 比作 火车  ， 火车 由 车厢
        // 线程 一节一节的车厢 。

        // 一个正在生产着运行着的工厂 。。 ==> 进程。
        // 工厂里面 不同的流水线，  ===> 线程 

        // 1. 线程必须依附进程才能运行
        // 2. 一个进程可以有多个线程
```

#### 5.js同步异步

``` js
同步和异步
        // 同步：同一时间只有一个任务再执行，前一个任务执行完，才能执行后一个任务。 串联
        // 异步：可以同时执行多个任务，可以提高程序的性能。 并联
 同步任务
        // 同步任务会在主线程上执行， 形成一个执行栈。

        // 异步任务
        // JS的异步主要由回调函数实现 
        // 1. 事件：click，resize 监听
        // 2. 资源加载 load DOMContentLoaded
        // 3. 定时器  setInterval / setTimeout
```

#### 6.js执行机制

``` js
  // 1. 首先判断JS任务是同步的还是异步的，同步任务会在主线程的执行栈中依次执行
        // 2. 异步任务会提交给异步进程处理，（比如setTimeout,click事件等，）当满足触发条件的时候，
        //    异步进程会把异步任务（回调函数）放到任务队列中
        // 3. 当主线程执行完所有的，所有的，所有的同步任务后，会去任务队列中查找，看是否有可以执行的异步任务，如果有，
        //    放到主线程中执行，执行完之后再去任务队列中查看，依次循环。
```

#### 7.location对象

``` js
location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分
 常用属性和方法：
 href 属性获取完整的 URL 地址，对其赋值时用于地址的跳转
 search 属性获取地址中携带的参数，符号 ？后面部分
 hash 属性获取地址中的啥希值，符号 # 后面部分
 reload 方法用来刷新当前页面，传入参数 true 时表示强制刷新

```

#### 8. navigator对象

``` js
navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息
 常用属性和方法：
 通过 userAgent 检测浏览器的版本及平台
// 检测 userAgent（浏览器信息）
!(function () {
const userAgent = navigator.userAgent
// 验证是否为Android或iPhone
const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
// 如果是Android或iPhone，则跳转至移动站点
if (android || iphone) {
location.href = 'http://m.itcast.cn'
}
})()

```

#### 9.  histroy对象

``` js
history 的数据类型是对象，主要管理历史记录， 该对象与浏览器地址栏的操作相对应，如前进、后退、历史记录等
```

![image-20221205192117793](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221205192117793.png)

​	
