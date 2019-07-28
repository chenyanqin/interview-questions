# 前端面试题
### [CSS部分](#par1)
1. 谷歌浏览器如何显示12px
   ```
   font-size: 12px;
   -webkit-transform: scale(0.8);
   -webkit-transform-origin: 0, 0;
   ```
2. 让一个元素水平垂直居中
   ```
   display: flex;
   justify-content: center;
   align-items: center;
   ```
3. 用伪类实现箭头，箭头朝右
   ```
   <span class="arrow-right"></span>

   .arrow-right:after {
	content: '';
	display: inline-block;
	width: 10px;
	height: 10px;
	border-top: 2px solid #ddd;
	border-right: 2px solid #ddd;
	transform: rotate(45deg);
   }
   ```
4. 浮动特点，及如何使浮动元素居中
   #### 浮动特点
   1. 不占据文档流
   2. 浮动的元素会影响下面的元素，不会影响上面的元素
   3. 浮动会影响元素的显示方式
    ```
    <div class="wrap">
        <div class="inner">sfsdfef</div>
    </div>

    .wrap {
        float: left;
        position: relative;
        left: 50%;
    }
    .inner {
        position: relative;
        right: 50%;
    }
    ```
5. css实现三角形
    ```
    <span class="trangle-up"></span>

   .trangle-up {
        width: 0;
        height: 0;
        border-left: 50px solid transparent;
        border-right: 50px solid transparent;
        border-bottom: 50px solid #ddd;
    }
    ```
6. css为页面中所有class为icon-xx添加样式
    ```
    子串值（Substring value）属性选择器, 又称伪正则选择器

    [class^="icon"]  // 选择class属性的值以 icon 开头（包括 icon）的元素
    ```
7. 移动Web实现1像素边框
    - border-image图片
        ```
        缺点: 需制作图片, 圆角的时候会出现模糊
        .border-image-1px {
            border-width: 1px 0px;
            -webkit-border-image: url(src) 2 0 stretch;
        }
        ```
    - viewport+rem
    - box-shadow
        ```
        .border {
            height: 5px;
            box-shadow:0 1px 1px -1px rgba(0, 0, 0, 0.5);
        }
        ```
    - transform: scale(0.5)
        ```
        .border {
            height:1px;
            background:#000;
            transform: scaleY(0.5);
            transform-origin:0 0;
        }
        ```
8. 怎样理解BFC(https://zhuanlan.zhihu.com/p/25321647)
 - BFC概念
    ```
    块级格式化上下文。它属于定位方案的普通流(指元素按照其在HTML中的先后位置至上而下布局, 在这个过程中, 行内元素水平排列, 直至当行被占满然后换行, 块级元素则会被渲染为完整的一个新行), 具有BFC特性的元素可以看作是隔离了的独立容器, 容器里面的元素不会在布局上影响到外面的元素, 并且BFC具有普通容器所没有的一些特性。
    ```
 - 触发BFC
    - body根元素
    - 浮动元素: float除none以外的值
    - 绝对定位元素: position(absolute、fixed)
    - display为inline-block、table-cells、flex
    - overflow除了visible以外的值(hidden、auto、scroll)
 - BFC特性及应用
    - 同一个BFC下外边距会发生折叠
    - BFC可以包含浮动的元素(清除浮动)
    - BFC可以阻止元素被浮动元素覆盖


9. CSS样式权重
    #### !important>行内样式>ID选择器 > 类选择器 | 属性选择器 | 伪类选择器 > 元素选择器
### [JS部分](#par2)
1. var、let、const的区别
    ```
    在JS函数中的var声明，其作用域是函数体的全部
    for(var i=0;i<10;i++){
          var a = 'a';
    }

    console.log(a); // 已经跳出 for 循环了，却还可以访问到 for 循环内定义的变量 a ，甚至连 i 都可以被放访问到

    for (var i = 0; i < 3; i++) {
      setTimeout(function () {
        console.log(i)
      }, 1000);
    }
    // 输出的结果为3个3, 而不是预想的0、1、2
    循环本身及三次 timeout 回调均共享唯一的变量 ** i 。当循环结束执行时，i 的值为3。所以当第一个 timeout 执行时，调用的 i 当让也为 3

    let声明的变量拥有块级作用域
    let声明的全局变量不是全局对象的属性
    形如for(let x...)的循环在每次迭代时都为x创建新的绑定
    用let重定义变量会抛出一个语法错误

    const用来定义常量
    const a;  // 报错
    const b = 'a'; b = 'b'; // 重复定义
    const c = {'a': a}; c.a = b; // 显示正常, c绑定的是对象指针, c.a对象指针没变, 指针指向的内容可以随意改变
    ```
2. 多维数组变一维(递归)
    ```
   let arr = [1,[2,[[3,4],5],6]];
   let newArr = [];
   fun(arr) {
	 for (let i = 0; i < arr.length; i++) {
		if(Array.isArray(arr[i])) {
			fun(arr[i]);	
		} else {
			newArr.push(arr[i])
		}
   	}
   }
   ```
  
3. 实现数组反转方法
   ```
   arr.reverse();
   ```
4. 列举5个基本数据类型
   number、String、boolean、null、undefined
5. 1除于0等于多少，0.1+0.2为什么不等于0.3
    Infinity.因为计算机用位来储存及处理数据
    0.1 = 0.00011001100...
    0.2 = 0.00110011...
    0.3 = 0.0100110011001100110011001100110011001100110011001101
6. 请写出几个立即执行函数
    ```
    (function(){}())
    (function(){})()
    var foo = function(){}()
    ```
7. 在1~31中随机取出7个不相等的数，以数组的形式返回
    ```
    var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31];
    var newArr = [];
    for (let i = 0; i < 7; i++) {
        let num = Math.floor(Math.random()*arr.length);
        newArr.push(arr[num]);
        arr.splice(num, 1);
    }
    ```
8. 怎么理解闭包
    一个函数内部定义了另一个函数，且这个函数访问父函数作用域的变量
9. 数组[1, 2, 3]调用toString()api后会变成什么样，[{id: 1}, {id: 2}, {id: 3}]调用toString后会变成什么样
	"1,2,3"  "[object Object],[object Object],[object Object]"
