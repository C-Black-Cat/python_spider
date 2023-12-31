# jQuery基本学习

**学习目标**

- 能够知道jQuery的作用及优点


- 能够知道jQuery的引入方式
- 能够说出两种jQuery入口函数的写法
- 能够使用jQuery选择器获取标签元素


- 能够使用选择器进行标签过滤


- 能够说出2种选择集转移方法


- 能够知道获取和设置元素内容的操作


- 能够知道获取和设置元素属性的操作


- 能够说出两个常用的jQuery事件


- 能够知道事件代理的使用方式


- 能够知道JavaScript对象有两种创建方式


- 能够知道json的格式


- 能够知道ajax的作用

## 一、jQuery的介绍

### 1. jQuery的定义

jQuery是对JavaScript的封装，它是免费、开源的JavaScript函数库，jQuery 极大地简化了 JavaScript 编程。

### 2. jQuery的作用

jQuery和JavaScript它们的作用一样，都是负责网页行为操作，增加网页和用户的交互效果的，只不过jQuery简化了JavaScript编程，jQuery实现交互效果更简单。

### 3. jQuery的优点

- jQuery兼容了现在主流的浏览器，增加了程序员的开发效率。
- jQuery简化了 JavaScript 编程，代码编写更加简单。

### 4. 小结

- jQuery是一个免费、开源的JavaScript函数库
- jQuery的作用和JavaScript一样，都是负责网页和用户的交互效果。
- jQuery的优点就是兼容主流、浏览器，代码编写更加简单。







## 二、jQuery的用法

### 1. jQuery的引入

```
<script src="js/jquery-1.12.4.min.js"></script>

```

### 2. jQuery的入口函数

我们知道使用js获取标签元素，需要页面加载完成以后再获取，我们通过给onload事件属性设置了一个函数来获取标签元素，而jquery提供了**ready函数**来解决这个问题，保证获取标签元素没有问题，**它的速度比原生的 window.onload 更快**。

#### JQuery与window.onload对比

**jQuery 入口函数:**

```
$(document).ready(function(){
    // 执行代码
});
或者
$(function(){
    // 执行代码
});
```

**JavaScript 入口函数:**

```
window.onload = function () {
    // 执行代码
}
```

jQuery 入口函数与 JavaScript 入口函数的区别：

-  jQuery 的入口函数是在 html 所有标签(DOM)都加载之后，就会去执行。
-  JavaScript 的 window.onload 事件是等到所有内容，包括外部图片之类的文件加载完后，才会执行。

![img](D:\Typora\my_file\图片\20171231003829544.jpeg)

**入口函数示例代码:**

```
<script src="js/jquery-1.12.4.min.js"></script>
<script>
    window.onload = function(){
        var oDiv = document.getElementById('div01');
        alert('原生就是获取的div：' + oDiv);
    };
    $(document).ready(function(){
        var $div = $('#div01');
        alert('jquery获取的div：' + $div);
    });
</script>

<div id="div01">这是一个div</div>
```

**入口函数的简写示例代码:**

```
<script src="js/jquery-1.12.4.min.js"></script>
<script>
    window.onload = function(){
        var oDiv = document.getElementById('div01');
        alert('原生就是获取的div：' + oDiv);
    };

    /*
    $(document).ready(function(){
        var $div = $('#div01');
        alert('jquery获取的div：' + $div);
    });
    */

    // 上面ready的写法可以简写成下面的形式：
    $(function(){
        var $div = $('#div01');
        alert('jquery获取的div：' + $div);
    }); 
</script>

<div id="div01">这是一个div</div>
```

### 3. 小结

- 引入jQuery

- 获取标签元素需要在入口函数来完成，它的速度比原生的 window.onload 更快

- jQuery入口函数有两种写法:

  ```
    // 完整写法
    $(document).ready(function(){
         ...
    });
  
    // 简化写法
    $(function(){
         ...
    });
  ```

## 三、jQuery选择器

### 1. jQuery选择器的介绍

jquery选择器就是快速选择标签元素，获取标签的，选择规则和css样式一样。

### 2. jQuery选择器的种类

1. 标签选择器
2. 类选择器
3. id选择器
4. 层级选择器
5. 属性选择器

**示例代码:**

```html
$('#myId') //选择id为myId的标签
$('.myClass') // 选择class为myClass的标签
$('li') //选择所有的li标签
$('#ul1 li span') //选择id为ul1标签下的所有li标签下的span标签
$('input[name=first]') // 选择name属性等于first的input标签

<div id="div1" class='myClass'>这是一个div元素</div>
<input type="text" name="first" id="input1" value="20px">
<a href="#" id="myId" class="sty01">这是一个链接</a>
```

> 补充：对于多个class属性的标签，怎么定位到该标签
>
> ![image-20230917151540552](D:\Typora\my_file\图片\image-20230917151540552.png)
>
> 1. 只写其中一个属性值。
> 2. 多个属性值间使用 `.` 连接
>
> ![image-20230917151823513](D:\Typora\my_file\图片\image-20230917151823513.png)

**说明:**
可以使用length属性来判断标签是否选择成功, 如果length大于0表示选择成功，否则选择失败。

```
$(function(){
    result = $("div").length;
    alert(result);
});

```

### 3. 小结

- jQuery选择器就是选择标签的
- 标签选择器是**根据标签名来选择标签**
- 类选择器是**根据类名来选择标签**
- id选择器是**根据id来选择标签**
- 层级选择器是**根据层级关系来选择标签**
- 属性选择器是**根据属性名来选择标签**



## 四、选择集过滤

### 1. 选择集过滤的介绍

选择集过滤就是在选择标签的集合里面过滤自己需要的标签

### 2. 选择集过滤的操作

- has(选择器名称)方法，表示选取包含指定选择器的标签
- eq(索引)方法，表示选取指定索引的标签

**has方法的示例代码:**

```
<script>
    $(function(){
        //  has方法的使用
        var $div = $("div").has("#mytext");
        //  设置样式
        $div.css({"background":"red"});
    });
</script>

<div>
    这是第一个div
    <input type="text" id="mytext">
</div>

<div>
    这是第二个div
    <input type="text">
    <input type="button">
</div>
```

**eq方法的示例代码:**

```
<script>
    $(function(){
        //  has方法的使用
        var $div = $("div").has("#mytext");
        //  设置样式
        $div.css({"background":"red"});

        //  eq方法的使用
        var $div = $("div").eq(1);
        //  设置样式
        $div.css({"background":"yellow"});
    });
</script>

<div>
    这是第一个div
    <input type="text" id="mytext">
</div>

<div>
    这是第二个div
    <input type="text">
    <input type="button">
</div>
```

### 3. 小结

- 选择集过滤可以使用has方法和eq方法来完成
- jquery给标签设置样式使用css方法





## 五、获取和设置元素内容

### 1. html方法的使用

jquery中的html方法可以获取和设置标签的html内容

**示例代码:**

```
<script>
    $(function(){

        var $div = $("#div1");
        //  获取标签的html内容
        var result = $div.html();
        alert(result);
        //  设置标签的html内容，之前的内容会清除
        $div.html("<span style='color:red'>你好</span>");
        //  追加html内容
        $div.append("<span style='color:red'>你好</span>");

    });
</script>

<div id="div1">
    <p>hello</p>
</div>
```

**说明:**

给指定标签追加html内容使用**append方法**

### 2. 小结

- 获取和设置元素的内容使用: html方法
- 给指定元素追加html内容使用: append方法



## 六、获取和设置元素属性

### 1. prop方法的使用

之前使用css方法可以给标签设置样式属性，那么设置标签的其它属性可以使用prop方法了。

**示例代码:**

```
<style>
    .a01{
        color:red;
    }
</style>

<script>
    $(function(){
        var $a = $("#link01");
        var $input = $('#input01')

        // 获取元素属性
        var sId = $a.prop("id");
        alert(sId);

        // 设置元素属性
        $a.prop({"href":"http://www.baidu.com","title":'这是去到百度的链接',"class":"a01"});

        //  获取value属性
        // var sValue = $input.prop("value");
        // alert(sValue);

        // 获取value属性使用val()方法的简写方式
        var sValue = $input.val();
        alert(sValue);
        // 设置value值
        $input.val("222222");
    })
</script>

<a id="link01">这是一个链接</a>
<input type="text" id="input01" value="111111">
```

**说明:** 获取value属性和设置value属性还可以通过**val方法**来完成。

### 2. 小结

- 获取和设置元素属性的操作可以通过prop方法来完成
- 获取和设置元素的value属性可以通过val方法来完成，更加简单和方便



## 七、jQuery事件

### 1. 常用事件

- click() 鼠标单击
- blur() 元素失去焦点
- focus() 元素获得焦点
- mouseover() 鼠标进入（进入子元素也触发）
- mouseout() 鼠标离开（离开子元素也触发）
- ready() DOM加载完成

**示例代码:**

```
<script>
    $(function(){
        var $li = $('.list li');
        var $button = $('#button1')
        var $text = $("#text1");
        var $div = $("#div1")

        //  鼠标点击
        $li.click(function(){             
            // this指的是当前发生事件的对象，但是它是一个原生js对象
            // this.style.background = 'red';

            // $(this) 指的是当前发生事件的jquery对象
            $(this).css({'background':'gold'});
            // 获取jquery对象的索引值,通过index() 方法
            alert($(this).index());
        });

        //  一般和按钮配合使用
        $button.click(function(){
            alert($text.val());
        });

        //  获取焦点
        $text.focus(function(){
            $(this).css({'background':'red'});

        });

        //  失去焦点
        $text.blur(function(){
            $(this).css({'background':'white'});

        });

        //  鼠标进入
        $div.mouseover(function(){
            $(this).css({'background':'gold'});

        });

        //  鼠标离开
        $div.mouseout(function() {
            $(this).css({'background':'white'});
        });
    });
</script>

<div id="div1">
    <ul class="list">
        <li>列表文字</li>
        <li>列表文字</li>
        <li>列表文字</li>
    </ul>

    <input type="text" id="text1">
    <input type="button" id="button1" value="点击">
</div>
```

**说明:**

- this指的是当前发生事件的对象，但是它是一个原生js对象
- $(this) 指的是当前发生事件的jquery对象

### 2. 小结

jQuery常用事件:

- click() 鼠标单击
- blur() 元素失去焦点
- focus() 元素获得焦点
- mouseover() 鼠标进入（进入子元素也触发）
- mouseout() 鼠标离开（离开子元素也触发）
- ready() DOM加载完成





## 八、json

### 1. json的介绍

json是 JavaScript Object Notation 的首字母缩写，翻译过来就是javascript对象表示法，这里说的json就是**类似于javascript对象的字符串**，它同时是一种**数据格式**，目前这种数据格式比较流行，逐渐替换掉了传统的xml数据格式。

### 2. json的格式

json有两种格式：

1. 对象格式
2. 数组格式

**对象格式:**

对象格式的json数据，使用一对大括号({})，大括号里面放入key:value形式的键值对，多个键值对使用逗号分隔。

**对象格式的json数据:**

```
{
    "name":"tom",
    "age":18
}
```

**格式说明:**

> json中的(key)属性名称和字符串值需要用**双引号**引起来，用单引号或者不用引号会导致读取数据错误。

**数组格式:**

数组格式的json数据，使用一对中括号([])，中括号里面的数据使用逗号分隔。

**数组格式的json数据:**

```
["tom",18,"programmer"]
```

**实际开发的json格式比较复杂,例如:**

```
{
    "name":"jack",
    "age":29,
    "hobby":["reading","travel","photography"]
    "school":{
        "name":"Merrimack College",
        "location":"North Andover, MA"
    }
}
```

### 3. json数据转换成JavaScript对象

**json本质上是字符串**，如果在js中操作json数据，可以将json字符串转化为JavaScript对象。

**示例代码:**

```
var sJson = '{"name":"tom","age":18}';
var oPerson = JSON.parse(sJson);

// 操作属性
alert(oPerson.name);
alert(oPerson.age);
```

### 4. 小结

- json就是一个javascript对象表示法，json本质上是一个字符串。
- json有两种格式：1. 对象格式, 2. 数组格式



## 九、ajax

### 1. ajax的介绍

ajax 是 Asynchronous JavaScript and XML的简写，ajax一个前后台配合的技术，它可以**让 javascript 发送异步的 http 请求，与后台通信进行数据的获取**，ajax 最大的优点是**实现局部刷新**，ajax可以发送http请求，当获取到后台数据的时候更新页面显示数据实现局部刷新，在这里大家只需要记住，**当前端页面想和后台服务器进行数据交互就可以使用ajax了。**

这里提示一下大家, **在html页面使用ajax需要在web服务器环境下运行, 一般向自己的web服务器发送ajax请求。**

### 2. ajax的使用

jquery将它封装成了一个方法$.ajax()，我们可以直接用这个方法来执行ajax请求。

**示例代码:**

```
<script>
    $.ajax({
    // 1.url 请求地址
    url:'https://image.baidu.com/search/acjson?tn=resultjson_com&logid=9427531757301067696&ipn=rj&ct=201326592&is=&fp=result&fr=ala&word=%E5%9B%BE%E7%89%87&queryWord=%E5%9B%BE%E7%89%87&cl=2&lm=-1&ie=utf-8&oe=utf-8&adpicid=&st=&z=&ic=&hd=&latest=&copyright=&s=&se=&tab=&width=&height=&face=&istype=&qc=&nc=&expermode=&nojc=&isAsync=&pn=120&rn=30&gsm=78&1685437399327=',
    // 2.type 请求方式，默认是'GET'，常用的还有'POST'
    type:'GET',
    // 3.dataType 设置返回的数据格式，常用的是'json'格式
    dataType:'JSON',
    // 4.data 设置发送给服务器的数据, 没有参数不需要设置

    // 5.success 设置请求成功后的回调函数
    success:function (response) {
        console.log(response);    
    },
    // 6.error 设置请求失败后的回调函数
    error:function () {
        alert("请求失败,请稍后再试!");
    },
    // 7.async 设置是否异步，默认值是'true'，表示异步，一般不用写
    async:true
});
</script>
```

**注意：** 由于版本的不同回调方法有一定的差异，请求成功也有可能是done，请求失败是fail

**ajax方法的参数说明:**

1. url 请求地址
2. type 请求方式，默认是'GET'，常用的还有'POST'
3. dataType 设置返回的数据格式，常用的是'json'格式
4. data 设置发送给服务器的数据，没有参数不需要设置
5. success 设置请求成功后的回调函数
6. error 设置请求失败后的回调函数
7. async 设置是否异步，默认值是'true'，表示异步，一般不用写
8. 同步和异步说明
   - 同步是一个ajax请求完成另外一个才可以请求，需要等待上一个ajax请求完成，好比线程同步。
   - 异步是多个ajax同时请求，不需要等待其它ajax请求完成， 好比线程异步。

**ajax的简写方式:**

$.ajax按照请求方式可以简写成$.get或者$.post方式

**ajax简写方式的示例代码:**

```
 <script>
    $(function(){
        /*
         1. url 请求地址
         2. data 设置发送给服务器的数据, 没有参数不需要设置
         3. success 设置请求成功后的回调函数
         4. dataType 设置返回的数据格式，常用的是'json'格式, 默认智能判断数据格式
        */ 
        $.get("http://www.liulongbin.top:3006/api/getbooks", function(dat,status){
            console.log(dat);
            console.log(status);
            alert(dat);
        }).error(function(){
            alert("网络异常");
        });

        /*
         1. url 请求地址
         2. data 设置发送给服务器的数据, 没有参数不需要设置
         3. success 设置请求成功后的回调函数
         4. dataType 设置返回的数据格式，常用的是'json'格式, 默认智能判断数据格式
        */ 
        $.post("test.php", {"func": "getNameAndTime"}, function(data){
            alert(data.name); 
            console.log(data.time); 
        }, "json").error(function(){
            alert("网络异常");
        }); 
    });


</script>
```

**多种发送ajax请求的方法:**https://blog.csdn.net/dy1717/article/details/121460836

**$.get和$.post方法的参数说明:**

$.get(url,data,success(data, status, xhr),dataType).error(func)
$.post(url,data,success(data, status, xhr),dataType).error(func)

1. url 请求地址
2. data 设置发送给服务器的数据，没有参数不需要设置
3. success 设置请求成功后的回调函数
   - data 请求的结果数据
   - status 请求的状态信息, 比如: "success"
   - xhr 底层发送http请求XMLHttpRequest对象
4. dataType 设置返回的数据格式
   - "xml"
   - "html"
   - "text"
   - "json"
5. error 表示错误异常处理
   - func 错误异常回调函数

### 3. 小结

- ajax 是发送http请求获取后台服务器数据的技术
- ajax的简写方式可以使用$.get和$.post方法来完成