---
layout: post
title:  "如何在监听器中使用spring容器"
date:   2016-06-02 15:25:50 +0800
categories: jekyll update
---
第一步： 在web.xml定义 request的上下文
#代码如下：
<!-- request上下文监听 -->
---
<listener>
<listener-class>org.springframework.web.context.request.RequestContextListener</listener-class>
</listener>
---
第二步 通过request上下文得到servletContext，从而得到applicationContext（注：可以将该代代码封装到工具类中）
#代码如下：

{% codeblock lang:java %}
HttpServletRequestrequest =((ServletRequestAttributes)RequestContextHolder.getRequestAttributes()).getRequest();
applicationContext= WebApplicationContextUtils.getRequiredWebApplicationContext(request.getServletContext());

publicclassApplicationContextUtils {
   privatestatic ApplicationContext applicationContext;
   publicstatic ApplicationContextgetApplicationContext(){
      if(applicationContext ==null){
         HttpServletRequestrequest = ((ServletRequestAttributes)RequestContextHolder.getRequestAttributes()).getRequest();
         applicationContext = WebApplicationContextUtils.getRequiredWebApplicationContext(request.getServletContext());
       }
      returnapplicationContext;
   }
}
{% endcodeblock%}
[文章出处](http://blog.csdn.net/zcl1199/article/details/51232196)