## Ajax Asynchronous Javascript And XML (异步的javascript和XML)
- ajax 不是新的编程语言，而是一种使用现有标准的新方法
- ajax最大的优点是 在不重新加载整个页面的情况下，可以与服务器交互数据并更新网页内容
- ajax不需要任何插件 但需要用户允许Javascript在浏览器执行

创建快速动态网页的技术
通过在后台服务器进行少量数据交互，ajax可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新

Ajax基于现有的Internet标准
- XMLHttpRequest 对象(异步的与服务器交换数据)
- JS DOM
- CSS
- XML 作为转换的格式(一般使用JSON数据)

### 创建XMLHttpRequest对象
1. 浏览器支持情况 
  所有的浏览器都支持XMLHttpRequest对象(IE5,IE6使用ActiveObject)
2. 创建XMLHttpRequest对象
```
// 为了应对所有的浏览器，以下是兼容的写法
var xmlhttp;
if (window.XMLHttpRequest){
  xmlhttp = new XMLHttpRequest();
}else{
  <!-- 兼容IE5，IE6 -->
  xmlhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
```
3. 向服务器发送请求 
  如需将请求发送到服务器，使用XMLHttpRequest对象的open()和send()方法
  ```
  xmlhttp.open("GET","ajax_info.txt",true)
  <!-- 
    参数说明：
      1. method 发送请求的方法 GET/POST
      2. URL 文件在服务器上的位置
      3. async true（异步） false（同步）
   -->
  xmlhttp.send()
  <!-- 
    参数说明：
      string：仅用于POST请求
   -->
  ```
  **GET还是POST**
  与POST相比，GET更简单也更快 并且在大部分情况下都能用
  在以下情况下，请使用POST请求：
    1. 无法使用缓存文件（更新服务器的文件或数据库）
    2. 向服务器发送大量数据（POST没有数据限制）
    3. 发送未知字符的用户输入时，POST比GET更稳定也更可靠

  发送GET请求
    xmlhttp.open("GET","/try/ajax/demo_get.php",true)
    或者：
    上面的例子可能得到的是缓存的结果，如要避免这种情况 请向URL添加一个唯一的ID
    xmlhttp.open("GET","/try/ajax/demo_get.php?t=" + Math.random(),true)
    或者：通过GET发送信息
    xmlhttp.open("GET","/try/ajax/demo_get2.php?fname=Henry&lname=Ford",true);

  发送POST请求
    xmlhttp.open("POST","/try/ajax/demo_post.php",true);
    如果需要像表单提交的POST数据，请使用setrequestHeader()来添加HTTP头，然后在send方法中规定要发送的数据
    xmlhttp.open("POST","/try/ajax/demo_post2.php",true);
    xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
    xmlhttp.send("fname=Henry&lname=Ford");
  setRequestHeader(header,value)

  当async=true时，请规定 在响应处于 onreadystatechange事件中的就绪状态时 执行的函数 
  ```
  xmlhttp.onreadystatechange = function(){
    if (xmlhttp.readyState == 4 && xmlhttp.status == 200){
      document.getElementById("myDiv").innerHTML = xmlhttp.reponseText;
    }
  }
 xmlhttp.open("GET","/try/ajax/ajax_info.txt",true);
 xmlhttp.send();
  ```
