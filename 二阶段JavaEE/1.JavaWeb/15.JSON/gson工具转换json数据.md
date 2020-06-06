# gson工具转换json数据
###### <font color=gold>情景①：gson将object对象--> json字符串</font>
需求：前端页面请求服务器, 接收json字符串格式的响应数据
```java
response.setContentType("text/html;charset=UTF-8");
//给前台响应一个JSON字符串
//response.getWriter().write("{\"name\":\"孙悟空\",\"age\":520}");
//假设从数据库中查询出来了一个学生的信息
Student stu = new Student(1, "白骨金", 18);
//转json字符串
//工具：gson
Gson gson = new Gson();
//将Student对象转换为json字符串
String stuJsonStr = gson.toJson(stu);
response.getWriter().write(stuJsonStr);
```
html页面：
```html
        $(function () {
            //给按钮绑定单击事件
            $("#btn").click(function () {
                //设置请求地址
                var url = "JSONServlet";
                //发送ajax请求
                $.post(url,function (res) {
                    alert(res);
                });
            });
        });
    </script>
</head>
<body>
    <button id="btn">发送Ajax请求接收json字符串格式的响应数据</button>
</body>
```
效果：
![](_v_images/20200507123736045_30016.png =600x)  
<font color=gold>**html发送异步请求动态拼接展示数据**</font>
1.原先是通过将数据对象list 存放于request域，转发 jsp 页面，利用JSTL的forEach展示所有对象信息；-- jsp展示数据的方式

2.html实现方式：ajax异步请求，利用gson将数据list转换为json字符串响应给html页面，利用js (jQuery)拼接`<table>`标签中的元素信息展示所有信息。

![](_v_images/20200507140006945_7228.png =600x)

***
###### <font color=gold>情景②：gson将json字符串--> object对象</font>
