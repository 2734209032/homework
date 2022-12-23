#### 1.echarts

``` js
  echarts.js  地址 https://echarts.apache.org/zh/index.html
<style>
        .line{
            width: 800px;
            height: 500px;
            margin: 100px auto;
        }
    </style>
<body>
    <div class="line"></div>
    <script src="./echarts.min.js"></script>
<script>
        // 立即执行函数IIFE 
        ;(function(){
        // 1. 初始化echarts实例
        const myChart = echarts.init(document.querySelector('.line'))
        // 2. 指定配置项option
        const option = {
            // 1. 颜色 数组
            // color: ['pink', 'blue', 'green', 'skyblue', 'red'],
            // ['#5470c6', '#91cc75', '#fac858', '#ee6666', '#73c0de', '#3ba272', '#fc8452', '#9a60b4', '#ea7ccc']
            // 1. 标题
            title: {
                text: '我的折线图321',

            },
            // 2. 提示框组件
            tooltip: {
                show:true,
                trigger: 'axis' // item
            },
            // 3. 图例组件 data里面的名字需要和series数据里面的名字一一对应
            legend: {
                // data可以不写，会默认取series系列里面的数据name
                // data: ['直播营销', '联盟广告', '视频广告', '直接访问']
            },
            // 4. 工具栏组件
            toolbox: {
                feature: {
                    // 保存图片
                    saveAsImage: {},
                    // 切换图的类型
                    magicType: {
                        type: ['line', 'bar','stack']
                    },
                    // 数据区域缩放。
                    dataZoom: {
                        show:true
                    },
                    // 数据展示
                    dataView: {
                        show:true
                    }
                }
                },
            // 6. grid 直角坐标系内绘图网格
            // 作用： 控制图表的大小
            grid: {
                left: '6%',
                right: '6%',
                bottom: '3%',
                // 决定 grid 区域是否包含坐标轴的刻度标签。
                // 刻度标签就是刻度上的文字
                containLabel: true // 一般情况下为true
            },

            // 7. xAxis x轴的配置项
            xAxis: {
                // 类型 , 类目
                // 类目 :  类, 一类. 目: 系列,一个一个的. 具有共同属性的一组数据 元素集合.
                type: 'category',   // 种类
                // 坐标轴两边留白策略 true，这时候刻度只是作为分隔线
                // 标签和数据点都会在两个刻度之间的带(band)中间。
                boundaryGap: false, // false好看点
                // 都属于星期, 类目数据
                // 刻度标签
                data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
            },
            yAxis: {
                type: 'value'
            },
            // 8. 系列  
            // series 是一个数组， 里面的每一个对象就是一条数据

            // 我们的数据放到这里的
            series: [
                {
                    // 和tooltip  , legend 有对应关系
                    name: '直播营销',
                    // 图表类型是线形图  line bar 
                    type: 'line',
                    stack:'总量',    // 堆叠
                    data: [120, 132, 101, 134, 90, 230, 210]
                },
                {
                    name: '联盟广告',
                    type: 'line',
                    stack:'总量',
                    data: [220, 182, 191, 234, 290, 330, 310]
                },
                {
                    name: '视频广告',
                    type: 'line',
                    stack:'总量',
                    data: [150, 232, 201, 154, 190, 330, 410]
                },
                {
                    name: '直接访问',
                    type: 'line',
                    stack:'总量',
                    data: [320, 332, 301, 334, 390, 330, 320]
                },
            ]
        };
        // 3. 将配置项传给echarts实例
        myChart.setOption(option)
        })()
```

**  适配echarts*

``` js
 myChart.setOption(option);
    window.addEventListener('resize', function () {
      myChart.resize()
```





#### 2.图片边框

![image-20221209103209492](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20221209103209492.png)

``` css
div{
width: 400px;
height: 300px;	
* 边框图片一定要有border *
border:15px solid orange;
* 1.引入边框图片 *
border-image-source: url(./new-project/images/border.jpg);
 *2。切割边框图片，按照 上右下左 一定不要带单位! !!*/
border-image-slice: 167 167 167 167:
* 3铺排方式 ==> stretch 默认 round repeat*border-image-repeat: round;
* 4。边框图片的宽度 如果不写，默认就是border的宽度
* border-iamge-width 不挤压文字
 *border-image-width: 50px;
}
/* 组合式写法*/
border-image: url("images/border.jpg") 167/20px round;
/*分开式写法*/
border-image-source: url("images/border.jpg");
border-image-slice: 167 167 167 167;
border-image-width: 20px;
border-image-repeat: round;
/*解释*/
/*
边框图片资源地址
裁剪尺寸（上 右 下 左）单位默认px，可使用百分百。
边框图片的宽度，默认边框的宽度。
平铺方式：
stretch 拉伸（默认）
repeat 平铺，从边框的中心向两侧开始平铺，会出现不完整的图片。
round 环绕，是完整的使用切割后的图片进行平铺*/
```

