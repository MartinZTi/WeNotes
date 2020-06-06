# (Ajax)服务器和html的json数据交互
###### <font color=gold>①服务器发送json响应数据</font>
```java
//后端服务器servlet
@WebServlet(name = "JSONServlet", urlPatterns = "/JSONServlet")
public class JSONServlet extends HttpServlet {
   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        //给前台响应一个JSON字符串
        response.getWriter().write("{\"name\":\"孙悟空\",\"age\":520}");
    }
}
```  

```html
<!--html页面：-->
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
![](_v_images/20200507122007808_19129.png =600x)
:::alert-light
**注意点：**
<font color=red>**jQuery中的Ajax方法可以自动转换json格式的响应数据**</font>
![](_v_images/20200507125239472_26599.png =600x)

:::
***
###### <font color=tomato>②前端请求提交json格式数据</font>

