# HTML
## HTML5新特性
canvas,video,audio,localStorage,sessionStorage

内容元素： header,footer,nav,article,aside,section
表单控件： calendar,date,time,url,search,email
控件元素： webworker,websocket,Geolocation
区分： doctype声明方式，html5不基于sgml

## XHTML和HTML的区别
xhtml是基于XML的置标语言，html是一种基本的web网页设计语言。
xhtml语法比较严格；
xhtml标签要小写，html大小写不敏感；
xhtml元素必须被正确嵌套；
xhtml元素必须被关闭

## 浏览器内核
浏览器内核负责对网页语法的解释并显示网页，
它决定了浏览器如何显示网页的内容和格式。
Trident：IE浏览器
Gecko：Mozilla，Firefox
Webkit：Safari，Chrome
Blink：Opera，Chrome

## doctype是什么？
告知浏览器的解析器应该用什么文档标准来解析文档，
通常有两种标准：怪异模式（没有声明doctype的情况下）和标准模式

## 标签语义化
利于页面内容结构化，提高代码可读性，利于SEO搜索；
在样式文件未加载时，页面结构清晰，易于用户阅读。

# CSS
## 盒模型
盒模型包括margin,padding,border,content,盒模型的大小有2种计算方式：
标准盒模型content-box(默认)和怪异盒模型border-box.

      行内元素的盒模型：
         1.宽高设置无效；
         2.边框有效；
         3.左右padding正常生效，上下padding效果不一定符合预期；
         4.左右margin正常生效，上下margin无效。

## 什么是BFC?
bfc就是块级格式化上下文，是web页面一块独立的渲染区域，
内部元素的渲染不会影响边界以外的元素。

1，bfc的区域不会与浮动元素重叠；
2，计算bfc的高度时，浮动元素也参与计算；
3，bfc通常用于清浮动，解决垂直方向margin重叠问题。
4，形成条件：1：设置float为除none以外的值，使其浮动；
            2：设置overflow为除visible以外的值；
            3：设置position为absolute或fixed；
            4：设置display为table-cell,inline-block或flex其中之一；

float和position不常用，会导致脱离文档流；
overflow为hidden比较常用；

## 浮动
作用：1：图片浮动之后可以实现文字环绕效果； 
      2：块级元素浮动之后可以排列在同一行；
      3：行内元素浮动之后可以设置宽高；
      4：浮动元素形成了BFC。
特点：浮动元素脱离了标准文档流，不占位置。
影响：浮动元素无法撑开高度，父元素没有设置高度时会塌陷；
      浮动元素会导致页面重排，影响其他元素布局；
      浮动元素的层级提升了半层，会遮盖在标准流块级元素之上。
解决方法： 1：父元素设置overflow：hidden形成bfc区域，清除浮动元素带来的影响；
          2：父元素新增空标签并设置clear：both；
          3：父元素添加一个通用class样式
               .clearfix::after,
               .clearfix::before{
                 content:'';
                 display:table;
                 clear:both;
               }
               .clearfix{
                  *zoom:1;   //兼容低IE版本
               }

## link和@import的区别
1：link属于XHTML标签，而@import只是css的一种方式；
2：link引用的样式会被同时加载，而@import等页面下载完再加载；
3：link没有兼容性问题，而@import不兼容低于ie5的浏览器；
4：link可以通过js控制DOM改变样式，而@import不可以。

## 水平垂直居中
1：position:absolute;
   left:0;
   right:0;
   top:0;
   bottom:0;
   margin:auto;

2: position:absolute;
   left:50%;
   top:50%;
   transform:translate(-50%,-50%);

3: display:flex;    //父元素设置
   justify-content:center;
   align-items:center;

4: display:grid;   //父元素设置
   justify-content:center;
   align-items:center;

5: display: table-cell;   //父元素设置
   text-align:center;
   vertical-align:middle;
   display: inline-block   //子元素设置

# JS
## js的数据类型有哪些？区别是什么？
基本数据类型：Number,String,Boolean,Null,Undefined,Symbol,BigInt;
引用数据类型：Object,Array,Function,Date,Regex;
   基本包装类型：Number,Boolean,String;
   单体内置对象：Global,Math.

区别：在内存中的存储方式不同，
     基本类型数据存储在栈中，占据空间小，属于被频繁使用的数据；
     引用类型数据存储在堆内存中，占据空间大。

判断数据类型的方法：
     typeof: 常用于判断基本类型数据，但是在检测Null时返回‘object’；
             判断引用类型数据返回‘object’，但是检测Function类型返回‘function’；
     instanceof： 常用于判断引用类型数据；
     constructor： 常用于判断引用类型数据；
     Object.prototype.toString.call():  可判断所有类型数据，最精准。

## Null和Undefined的区别：
undefined是全局对象的一个属性，当一个变量被定义但是没有赋值（初始化）的时候，就是undefined。
null表示一个空的对象引用。
undefined == null    undefined !== null

null和undefined在和其他数据进行相等性比较时返回值都是false
(除了null和undefined互相比较之外)
null == false   // false
null == ''      // false
null == undefined  // true

如果定义的变量准备在将来用于保存对象，最好初始化为null
if(car != null) { ... 执行某些操作...}

ECMAScript中所有类型的值都有一个等价的Boolean值，可以调用转型函数Boolean（）查看其布尔值。
布尔值为true的数据类型：true，非空字符串，非零数字，非空对象，n/a;
布尔值为false的数据类型: false, " "(空字符串)，0和NaN，null，undefined。

## 判断数组类型的方法
1: arr instanceof Array       
        Array.prototype.isPrototypeOf(arr)     Object.getPrototypeOf(arr) === Array.prototype
2: arr.constructor === Array
3: arr.__proto__ === Array.prototype
4. Array.isArray(arr)
5. Object.prototype.toString.call(arr) === '[object Array]'

## 将类数组转化为数组的方法：
1. Array.from(args)
2. [... args]
3. Array.prototype.slice.call(args)   //亦可用于浅拷贝数组

## 数组去重的方法：
1. arr = [ ... new Set(arr)]
2. arr = arr.reduce((prev,curr) => prev.includes(curr) ? prev : prev.concat(curr) , [])
3. Array.prototype.myuniq = function(){
      var arr =[]
      var flag = true
      this.forEach(function(item){
         if(item != item){
            flag && arr.indexOf(item) === -1 ? arr.push(item) : ''
            flag = false
         }else{
            arr.indexOf(item) === -1 ? arr.push(item) : ''
         }
      })
      return arr
   }

## 冒泡排序和快速排序：
   function maopaoSort(arr){
      for(var i = 0; i < arr.length; i++){
         for(var j = 0; j < arr.length - i -1; j++){
            if(arr[j] < arr[j+1]){
               var temp = arr[j]
               arr[j] = arr[j+1]
               arr[j+1] = temp
            }
         }
      }
      return arr
   }

   function quickSort(arr){
      if(arr.length <= 1) return arr
      var left = [], right = []
      for(var i = 1; i < arr.length; i++){
         arr[0] < arr[i] ? right.push(arr[i]) : left.push(arr[i])
      }
      return arguments.callee(left).concat(arr[0], arguments.callee(right))
   }

转换方法      join()    //返回间隔插入某个字符之后的字符串
重排序方法    reverse()     sort() ==>   arr.sort((a,b) => a-b)   //改变原数组
拼接方法      concat()                                            //合并数组
截取方法      slice(start, end)                                   //不改变原数组
操作方法      splice(start, deleteNumber, insertItem ...)         //改变原数组     删除，插入，替换
位置方法      indexOf()                                           //indexOf(NaN)永远返回-1
迭代方法      every((item,index,arr) => true or false)            //判定方法
             some((item,index,arr) => true or false)             //部分判定方法
             filter((item,index,arr) => 返回符合条件的项组成的数组)//筛选方法
             forEach((item,index,arr) => 执行某些操作)            //没有返回值
             map((item,index,arr) => 返回由操作后的结果组成的数组) //比如可以对数组每一项乘以2
归并方法      reduce((prev,curr,index,arr) => return prev+curr, 0)

字符串方法    charAt()   //返回指定位置的字符      indexOf()   //返回指定字符的位置
             slice(start，end)和substring()一样返回指定起始与结束位置之间的字符
             substr(start, number)返回起始位置起指定数量的字符
             trim()        toLowerCase()   toUpperCase()
             match(regEx)    //模式匹配方法，与正则类似
             text.match(regEx)      ===>   regEx.exec(text)
             text.search(regEx)    //模式匹配方法，返回第一个匹配的字符串所在的位置
             replace()方法     text.split(" , ")返回分割后的数组
             String.fromCharCode(104,101,108,108,111)==='hello'  //静态方法（构造函数方法）Math.max()

## 继承：
      1.通过原型链的方式实现继承 Student.prototype = new People()  //使原型对象等于父类的实例
        本质是重写原型对象，父类实例中的属性和方法，现在也存在于子类的原型对象中。
        优点：代码简单，容易理解；缺点：包含引用类型值的实例属性会被所有实例共享，并且在创建实例
        时，无法向超类型的构造函数传递参数。
      2.借用构造函数（经典继承） SuperType.call(this)    
        在子类型函数作用域中，执行超类型构造函数代码来继承它的属性。
        优点：解决了原型链继承所存在的2个问题；缺点：在构造函数中定义的方法不能做到函数复用，而且超类型的原型上的方法没有继承下来。
      3.组合继承   结合原型链和经典继承
        SuperType.call(this,name)       //继承实例属性
        SubType.prototype = new SuperType()           //继承原型属性和方法
        SubType.prototype.constructor = SubType
        优点：每个实例都有自己的属性，并且方法实现了函数复用，解决了上面2个继承方式的缺点；
        缺点：超类型构造函数会被调用2次，第一次调用继承的属性存在于子类型的原型中，第二次调用继承的属性存在于实例中，
        第二次继承的属性会屏蔽第一次继承的同名属性。
      4.原型式继承    Object.create(SuperType,descriptor)    //本质是实现对象的浅拷贝
        优点：不需要创建子类型构造函数；缺点：包含引用类型值的实例属性会被所有实例共享。
      5.寄生式继承          拷贝对象，将之增强后返回。
        优点：不需要创建子类型构造函数；缺点：方法不能做到函数复用。
      6.寄生组合式继承      通过借调构造函数继承实例属性，通过寄生式继承复制超类型原型对象来继承方法。
        SuperType.call(this,name)
        var subPrototype = Object.create(superType.prototype)
        subPrototype.constructor = subType
        subType.prototype = subPrototype
        优点：只需要调用一次超类型构造函数，避免了在子类型原型对象上继承重复的实例属性，并且原型链保持不变。
        缺点：代码复杂。
      7.ES6  Class实现继承
        Class Person{
         constructor(name,age){
            this.name = name
            this.age = age
         }
        }
        Class Student extends Person{
         constructor(name,age,sex){
            super(name,age)
            this.sex = sex
         }
        }
        优点：语法简单易懂；缺点：不是所有的浏览器都支持Class关键字。

## new关键字会发生什么？
1.创建一个新的空对象；     
{}.__proto__ = Constructor.prototype    ===>   Constructor.prototype.isPrototypeOf({})
                                        ===>   Object.getPrototypeOf({}) === Constructor.prototype
2.将构造函数的作用域赋给新对象，即this指向了新对象；
3.执行构造函数中的代码，为新对象添加属性；
4.返回新对象。

箭头函数没有arguments，没有原型和super。
不能用作构造函数，所以不能使用new关键字，所以没有this，只能从外部获取this。

## this指向
函数的调用方式决定了this的值：                  //函数调用时所处于的作用域（执行环境）即为this的值
1.在全局环境中调用函数，this指向window，严格模式下是undefined。
2.通过一个对象调用内部的方法，this指向对象本身。
3.箭头函数的this要从外部获取。
4.定时器和匿名函数以及立即执行函数的this指向window，因为它们具有全局性。
5.call，apply和bind方法可以改变this的值，即改变函数调用时的作用域（执行环境）。

## call apply bind
call方法和apply方法改变了函数运行时的作用域，并且立即执行函数，          //使用call或apply的好处在于对象不需要与方法有耦合关系
bind方法返回一个指定了作用域的函数，不会立即执行函数，需要调用之后再执行。
//(bind方法把this给闭包了)

call方法接收多个参数，其第一个参数为要绑定的this对象；
apply方法的第一个参数为要绑定的this对象，其他参数会以数组形式作为第二个参数；
bind方法的第一个参数为要绑定的this对象，他的参数会传递给内部所返回的函数。

应用场景：1.call方法用于将类数组转为真数组: Array.prototype.slice.call(args);
                   判断数据类型： Object.prototype.toString.call(xxx)；
                   实现经典继承：   function Student(name){
                                 People.call(this,name)
                               }。
         2.apply方法用于查找数组最大值：  Math.max.apply(Math,arr)；
                   合并数组：   Array.prototype.push.apply(arr1,arr2)。
         3.bind方法可以保存this变量并返回一个函数，无论该函数被如何调用，this的值都不会改变。
           //(类似call方法实现继承)

## 什么是闭包
当在函数内部定义了其他函数时，就创建了闭包，闭包可以访问包含函数的参数、arguments和局部变量。
原理：闭包的作用域链包含着它自己的作用域、包含函数的作用域和全局作用域。
缺点：通常情况下，函数的作用域及其所有变量会在函数执行后被销毁，但是当它创建了闭包后，
      闭包会携带包含函数的作用域，变量不会被销毁，因此可能会导致内存溢出，除非解除对闭包的引用（闭包变量名=null）。
应用：模仿块级作用域(立即执行函数)，在构造函数中定义特权方法，设置缓存（模块模式），防抖节流。

## cookie localStorage sessionStorage
他们都是浏览器的本地存储，区别在于六个地方：
1.写入方式：  cookie由服务器端写入，另外2个由前端写入；
2.生命周期：  cookie的生命周期是服务器端在写入的时候设置好的，
             localStorage是写入后就一直存在，除非手动清除，
             sessionStorage是页面关闭后就自动清除了。
3.存储大小：  cookie比较小，大概4kb。另外2个比较大，5M左右。
4.数据共享：  他们都遵循同源原则，sessionStorage还限制必须是同一个页面。
5.发送请求时是否携带数据：  前端向后端发送请求时会自动携带cookie中的数据，但不会携带另外2个的数据。
6.应用场景：  cookie一般用于存储登录验证信息sessionID或token，
             localStorage常用于存储不易变动的数据，减轻服务器的压力，
             sessionStorage可用来检测用户是否是刷新进入页面，如音乐播放器恢复播放进度条的功能。

## GET和POST的区别
1.get存储小，不超过2kb；  post没有限制；
2.get不安全，请求参数显示在地址栏；  post安全性较高，通过body传递参数；
3.get可以缓存，post不能缓存；
4.get效率高， post需要加密解密，速度慢。
5.get常用于数据查询或者提交一些不重要的信息，
  post常用于增加、删除或修改数据，以及上传文件等操作。

## 前端优化性能的手段：
使文件加载更快：1. 压缩图片和文件，
               2.减少网络请求次数：雪碧图精灵图，防抖节流，
               3.减少渲染次数：http缓存，本地缓存，vue的keep-alive缓存
使页面渲染更快：1. 提前渲染：ssr服务器端渲染，
               2.避免阻塞：css放在head中，js放在body底部，
               3.避免无用渲染：懒加载，
               4.减少渲染次数：对dom查询进行缓存，合并dom操作，使用减少重排的标签。

## 跨域是什么，如何解决跨域？
当页面中某个接口请求的地址和该页面的协议、域名、端口不一样时，就造成了跨域。
跨域是浏览器为了保证网页安全而给出的同源协议策略。
解决方法：1.cors，通过后端设置允许跨域；
         2.node中间件和nginx反向代理；
         3.jsonp，利用的原理是script标签可以跨域请求资源，将回调函数作为参数拼接在url中，后端
         收到请求，调用该回调函数，并将数据作为参数返回去。
         4.postmessage，H5新增api，通过发送和接受api实现跨域通信。
跨域场景：前后端分离式开发，调用第三方接口。
