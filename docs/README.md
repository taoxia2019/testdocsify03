### 1. dom对象和jQuery对象的区别
用原生js获取的对象就是DOM对象
```js
var mydiv=document.queryselector("div");
```
用 jQuery获得的对象就是jQuery对象，本质是：$对DOM元素象进行了包装。
```js
$("div");
```

js对象和jQuery对象的 属性和方法不能混用,只能用各自的方法和属性.
 ```js
 //js方法
 js.style.display();
 //jQuery方法
 $("div").hide();
 
 ```
 ### 2. DOM与jQuery对象互相转换
 ```js
 //DOM对象转jQuery对象方法
 var mydiv=document.queryselector("div");
 $(mydiv);
 //jQuery对象转DOM对象
 //方法一
  $(mydiv)[0];
  //方法二
  $(mydiv).get(0);
 
 ```
 
 ### 3. jquery选择器
 ```js
 $(".nav") //类选择器
 $("div") //元素选择器
 $("ul li") //后代元素选择器
 
 //所有div都会被设置新的背景颜色.
 //隐式迭代--jQuery在内部把匹配的所有元素进行了遍历循环,给每个元素添加了ccss样式.
 $("div").css("background","pink")
 ```
 
 ### 4. 获取属性值的方法
 1.获取固有属性值
 ```js
 $("div").prop("href")
 ```
 2.获取自定义属性
 ```js
 $("div").attr("href")
 ```
 3.获取数据缓存data()的属性 HTML5自定义属性
 ```js
 $("div").data("index")
 ```
 
 ### 5.  电梯导航 核心代码
 ```js
//.fixed导航栏的属性 .floor .w所需页面块属性
 $(".fixed").click(function(){
    var current = $(".floor .w").eq($(this).index()).offset().top;
    $("body,html").stop().animate({
        scrollTop: current;
    });
 })
 
 
 ```
 6.本地储存 与字符串对象转换
 ```js
     //数组对象
        var todolist = [{
            "title":"八个馒头",
            "done":false
        },{
            "title":"学习jQuery",
            "done":false
        }];
        //本地存储只能是字符串格式,需要使用JSON.stringify()方法转换
        localStorage.setItem("todo",JSON.stringify(todolist));
        //取值时,需要使用JSON.parse()将字符串转为对象
        var data = JSON.parse(localStorage.getItem("todo"));
        console.log(data[0].title);
    })

    //localStorage 和 sessionStorage 属性允许在浏览器中存储 key/value 对的数据。
    //localStorage 用于长久保存整个网站的数据，保存的数据没有过期时间，直到手动去删除。
    //localStorage 属性是只读的。
    //localStorage的方法有以下几种:
    localStorage.key();//使用 key() 方法，向其中输入索引即可获取对应的键。
    localStorage.setItem();//设置指定储存
    localStorage.getItem();//获取指定储存
    localStorage.removeItem();//清楚指定储存
    localStorage.clear();//清除所有储存
    /*
    * localStorage 的优势
    1、localStorage 拓展了 cookie 的 4K 限制。
    2、localStorage 会可以将第一次请求的数据直接存储到本地，这个相当于一个 5M 大小的针对于前端页面的数据库，相比于 cookie 可以节约带宽，但是这个却是只有在高版本的浏览器中才支持的。 
    localStorage 的局限
    1、浏览器的大小不统一，并且在 IE8 以上的 IE 版本才支持 localStorage 这个属性。
    2、目前所有的浏览器中都会把localStorage的值类型限定为string类型，这个在对我们日常比较常见的JSON对象类型需要一些转换。
    3、localStorage在浏览器的隐私模式下面是不可读取的。
    4、localStorage本质上是对字符串的读取，如果存储内容多的话会消耗内存空间，会导致页面变卡。
    5、localStorage不能被爬虫抓取到。
    localStorage 与 sessionStorage 的唯一一点区别就是 localStorage 属于永久性存储，而 sessionStorage 属于当会话结束的时候，sessionStorage 中的键值对会被清空。
     */
 ```
 
### 7.todolist 综合练习
#### 1.html 代码
```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <title>ToDoList—最简单的待办事项列表</title>
    <link rel="stylesheet" href="css/index.css">
    <script src="js/jquery.min.js"></script>
    <script src="js/todolist.js"></script>
</head>
<body>
    <header>
        <section>
            <label for="title">ToDoList</label>
            <input type="text" id="title" name="title" placeholder="添加ToDo" required="required" autocomplete="off" />
        </section>
    </header>
    <section>
        <h2>正在进行 <span id="todocount"></span></h2>
        <ol id="todolist" class="demo-box">
        </ol>
        <h2>已经完成 <span id="donecount"></span></h2>
        <ul id="donelist">
        </ul>
    </section>
    <footer>
        Copyright &copy; 2014 todolist.cn
    </footer>
</body>
</html>
```
#### 2.css样式
```css
body {
    margin: 0;
    padding: 0;
    font-size: 16px;
    background: #CDCDCD;
}

header {
    height: 50px;
    background: #333;
    background: rgba(47, 47, 47, 0.98);
}

section {
    margin: 0 auto;
}

label {
    float: left;
    width: 100px;
    line-height: 50px;
    color: #DDD;
    font-size: 24px;
    cursor: pointer;
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

header input {
    float: right;
    width: 60%;
    height: 24px;
    margin-top: 12px;
    text-indent: 10px;
    border-radius: 5px;
    box-shadow: 0 1px 0 rgba(255, 255, 255, 0.24), 0 1px 6px rgba(0, 0, 0, 0.45) inset;
    border: none
}

input:focus {
    outline-width: 0
}

h2 {
    position: relative;
}

span {
    position: absolute;
    top: 2px;
    right: 5px;
    display: inline-block;
    padding: 0 5px;
    height: 20px;
    border-radius: 20px;
    background: #E6E6FA;
    line-height: 22px;
    text-align: center;
    color: #666;
    font-size: 14px;
}

ol,
ul {
    padding: 0;
    list-style: none;
}

li input {
    position: absolute;
    top: 2px;
    left: 10px;
    width: 22px;
    height: 22px;
    cursor: pointer;
}

p {
    margin: 0;
}

li p input {
    top: 3px;
    left: 40px;
    width: 70%;
    height: 20px;
    line-height: 14px;
    text-indent: 5px;
    font-size: 14px;
}

li {
    height: 32px;
    line-height: 32px;
    background: #fff;
    position: relative;
    margin-bottom: 10px;
    padding: 0 45px;
    border-radius: 3px;
    border-left: 5px solid #629A9C;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.07);
}

ol li {
    cursor: move;
}

ul li {
    border-left: 5px solid #999;
    opacity: 0.5;
}

li a {
    position: absolute;
    top: 2px;
    right: 5px;
    display: inline-block;
    width: 14px;
    height: 12px;
    border-radius: 14px;
    border: 6px double #FFF;
    background: #CCC;
    line-height: 14px;
    text-align: center;
    color: #FFF;
    font-weight: bold;
    font-size: 14px;
    cursor: pointer;
}

footer {
    color: #666;
    font-size: 14px;
    text-align: center;
}

footer a {
    color: #666;
    text-decoration: none;
    color: #999;
}

@media screen and (max-device-width: 620px) {
    section {
        width: 96%;
        padding: 0 2%;
    }
}

@media screen and (min-width: 620px) {
    section {
        width: 600px;
        padding: 0 10px;
    }
}
```
#### 3.js代码实现
```js
$(function () {
    //打开初始页面时,渲染加载数据
    loaddata();
    $("#title").on("keydown",function (e) {
        //判断按下的是否Enter键
        if(e.keyCode===13){
            if($("#title").val()===""){
                alert("请输入你需要办理的事项!")
            }else{
                //获取原来的数组
               var data = getdata();
               //将新的内容添加到数组对象中
               data.push({title : $("#title").val(),done:false})
                //保存到本地储存
                savedata(data);
               //重新加载数据
               loaddata();
               //设置输入框内容为空
               $(this).val("");
            }
        }
    });

    //1.获取本地储存数据
    function getdata() {
        //获取本地存储数据
        var data=localStorage.getItem("todolist");
        //判断
        if(data!==null){
            //当数据不为空时,使用转换方法将字符串数据以对象数据返回
            return JSON.parse(data);
        }else{
            //返回空数组对象
            return [];
        }
    }

    //2.保存数据到本地
    function  savedata(data) {
        //由于本地数据为字符串格式,需要将对象转换为JSON格式
        localStorage.setItem("todolist",JSON.stringify(data))

    }
    //3.删除数据
    $("ol,ul").on("click","a",function () {
        var data=getdata();
        //获得索引值
        var index = $(this).attr("id");
        //删除索引为index的数据
        data.splice(index,1);
        // 保存到本地存储
        savedata(data);
        // 重新渲染页面
        loaddata();
    })

    //4. toDoList 正在进行和已完成选项操作
    $("ol,ul").on("click","input",function () {
        // 先获取本地存储的数据
        var data =getdata();
        //获取兄弟元素的id属性值
        var index = $(this).siblings("a").attr("id");
        // 修改数据
       data[index].done=$(this).prop("checked");
        // 保存到本地存储
       savedata(data);
        // 重新渲染页面
        loaddata();
    });

    //5.渲染加载数据
    function  loaddata() {
        // 读取本地存储的数据
        var data = getdata();
        // 正在进行的个数
        var todocount=0;
        // 已经完成的个数
        var donecount=0;
        // 遍历之前先要清空ol里面的元素内容
        $("ol,ul").empty();
        // 遍历这个数据
        $.each(data,function (i,n) {
            if(n.done) {
                //在ul中向前添加li元素.li元素有三个子元素 input/p/a元素
                $("ul").prepend("<li><input type='checkbox' checked='"+n.done+"'><p>"+n.title+"</p><a href='javascript:;' id='"+i+"'></a></li>");
                donecount++;
            }else {
                $("ol").prepend("<li><input type='checkbox'><p>" + n.title + "</p><a href='javascript:;' id='" + i + "'></a></li>")
                todocount++;
            }
        });
        //完成个数
        $("#donecount").text(donecount);
        //代办个数
        $("#todocount").text(todocount)
    }
})
```
#### 4.js代码实现步骤
- 获取本地存储数据 get函数
   -  通过localstorage.getitem获取到数据;
   -  判断是或否为空;
   -  如果为空,返回空数组.
   -  不为空,使用JSON.prase将字符串转为数组对象.
- 获取输入的数据
   - 获取事件的动作,如果动作为keycode===13,即按下了回车键
   - 如input框不等于空,那么将数据push到数组当中
   - 调用save函数保存到本地存储
   - 调用load函数重现渲染表格
- 保存数据到本地 save函数
   - 通过localstorage.setitem设置值到本地
   - 转换数据存储格式 数组对象转为字符串
- 删除对应的事项-委派事件
   - 获取本地存储的数据
   - 获取对应事项的索引值,此前在li>a中自定义属性 "id".
   - 使用数组方法splice删除对象
   - 保存到本地
   - 重新渲染到表格
- 代办与已办事项进行切换 事件委派
   - 获取对应索引值
   - 获取对应的checked的值
   - 修改保存到本地存储
   - 重新渲染到表格
-表格渲染 load函数
   - 获取数据
   - 遍历数据
   - 根据done属性的值选择添加到列表
      - done为TRUE 在 **ul** 中prepend添加li元素
      元素中包含input/p/a元素<a>标签添加自定义属性 id值为索引值.p标签中值为该对象的title属性值.input类型为checkbox 渲染个数自增
      - done为TRUE 在 **ol** 中prepend添加li元素
      元素中包含input/p/a元素<a>标签添加自定义属性 id值为索引值.p标签中值为该对象的title属性值.input类型为checkbox 渲染个数自增
    - 将li个数分别添加到span元素中

 
 

