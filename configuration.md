# 配置

本章将带你学习一个 Struts 2 应用程序必需的基本配置。在这里，我们将看到一些重要的配置文件：**web.xml**，**struts.xml**，**struts-config.xml** 和 **struts.properties**，它们将被配置。

老实说你可以使用 web.xml 和 struts.xml 配置文件，在前面的章节中你已经看到了我们的例子使用这两个文件进行工作，但是为了你学习知识，我也解释其他文件。

## web.xml 文件

web.xml 配置文件是一个 J2EE 的配置文件，它决定如何用 servlet 容器来处理 HTTP 请求的元素。它不是严格意义上的一个 Struts 2 的配置文件，但它是一个 Struts 2 工作时需要被配置的文件。

如前所述，这个文件为任何 web 应用程序提供了一个入口点。Struts 2 应用程序的入口点是一个在部署描述符（web.xml）中已定义的过滤器。因此，我们将在 web.xml 中定义 FilterDispatcher 类的入口。web.xml 文件需要在 **WebContent/WEB-INF** 文件夹下创建。

如果你在没有生成配置文件的模板或工具（如 Eclipse 或 Maven2）的帮助下开始，那么 web.xml 是你需要配置的第一个配置文件。下面是在我们最后一个例子中使用的 web.xml 文件的内容。

``` 
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xmlns="http://java.sun.com/xml/ns/javaee" 
   xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
   xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
   http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
   id="WebApp_ID" version="3.0">  
   <display-name>Struts 2</display-name>
   <welcome-file-list>
      <welcome-file>index.jsp</welcome-file>
   </welcome-file-list>  
   <filter>
      <filter-name>struts2</filter-name>
      <filter-class>
         org.apache.struts2.dispatcher.FilterDispatcher
      </filter-class>
   </filter>
   <filter-mapping>
      <filter-name>struts2</filter-name>
      <url-pattern>/*</url-pattern>
   </filter-mapping>
</web-app>
```

注意，我们映射 Struts 2 的过滤器为 /*，而不是 **/*.action**，这意味着所有的 urls 将被 struts 的过滤器解析。当我们进入注解这一章时，我们将讨论这个。

## struts.xml 文件

**struts.xml** 文件包含配置信息，随着动作的开发，你将会修改这些配置信息。这个文件可以用来重写应用程序的默认设置，例如 struts.devMode = false，还有定义在属性文件中的其他设置。这个文件可以在文件夹** WEB-INF/classes** 下创建。

让我们来看看在前面的章节中已经解释的 Hello World 例子中创建的 struts.xml 文件。

``` 
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE struts PUBLIC
   "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
   "http://struts.apache.org/dtds/struts-2.0.dtd">
<struts>
   <constant name="struts.devMode" value="true" />
   <package name="helloworld" extends="struts-default">  
      <action name="hello" 
            class="com.tutorialspoint.struts2.HelloWorldAction" 
            method="execute">
            <result name="success">/HelloWorld.jsp</result>
      </action>
      <-- more actions can be listed here -->
   </package>
   <-- more packages can be listed here -->
</struts>
```

要注意的第一件事是 **DOCTYPE**。所有的 struts 配置文件需要有正确的 doctype，正如我们的小例子所示。<struts> 是根标签的元素，在它的下面我们使用 <package> 标签声明不同的包。在这里，<package> 允许配置的分离和模块化。当你有一个大项目，并且该项目被划分成不同的模块时，它是非常有用的。

也就是说，如果你的项目有三个域 - business_applicaiton，customer_application 和 staff_application，你可以创建三个包，并且在适当的包中存储相关的动作。包标签具有以下的属性：

<table class="table table-bordered"> 
<tr>
<th style="width:25%">属性</th>
<th>描述</th>
</tr> 
<tr>
<td>name (required)</td>
<td>包的唯一标识符。</td>
</tr> 
<tr>
<td>extends</td>
<td>这个包是由哪个包扩展的?默认情况下,我们使用 struts-default 作为基础包。</td>
</tr> 
<tr>
<td>abstract</td>
<td>如果标记为 true，对于终端用户消费来说，这个包是不可用的。</td>
</tr> 
<tr>
<td>namesapce</td>
<td>动作的唯一命名空间。</td>
</tr> 
</table>

	
带着 name 和 value 属性的**常量**标签将被用于重写任何 **default.properties** 中定义下面的属性，就如我们刚刚设置 **struts.devMode** 属性的过程。设置 **struts.devMode** 属性允许我们在日志文件中看到更多的调试信息。

我们定义对应于每一个我们要访问的 URL 的**动作**标签，我们定义了一个带有 execute() 方法的类，每当我们访问相应的 URL 时，它将被访问。

在动作被执行后，结果决定把得到的哪些返回给浏览器。从动作中返回的字符串应该是一个结果的名称。同上，每次执行动作，结果都被配置，或者都作为一个 “global” 的结果，包中的每个动作都是可用的。结果有可选的 **name** 和 **type** 属性。默认名称的值为 “success”。

随着时间的推移，Struts.xml 文件可以扩展，用包阻止它是一种使它模块化的方式，但是 struts 提供了另一种使 struts.xml 文件模块化的方式。你可以将文件分割成多个 xml 文件，并且用下列的方式导入它们。

``` 
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
    "http://struts.apache.org/dtds/struts-2.0.dtd">
<struts>
     <include file="my-struts1.xml"/>
     <include file="my-struts2.xml"/>
</struts>
```

我们还没有重写的其他的配置文件是 struts-default.xml。这个文件包含了 Struts 的标准配置设置，你就不必要为了你的项目的 99.99％ 修改这些设置。为此，我们不打算详细地介绍这个文件。如果你有兴趣，可以在 struts2-core-2.2.3.jar 文件中有效的 **default.properties** 文件里看到它。

## struts-config.xml 文件

struts-config.xml 配置文件是在 Web 客户端中视图和模型组件之间的链接，但是你就不必要为了你的项目的 99.99％ 而修改这些设置。基本配置文件包含下面的主要内容：

<table class="table table-bordered"> 
<tr>
<th style="width:5">序号 </th>
<th>拦截器 &amp; 描述</th>
</tr> 
<tr>
<td>1</td>
<td><b>struts-config</b>
<p>它是配置文件的根节点。</p>
</td>
</tr> 
<tr>
<td>2</td>
<td><b>form-beans</b>
<p>它是你把 ActionForm 子类映射到名称上的位置。你使用这个名字作为 ActionForm 的别名，贯穿 struts-config.xml 的其余部分，甚至在 JSP 页面中。</p>
</td>
</tr> 
<tr>
<td>3</td>
<td><b>global forwards</b>
<p>这个部分把 web 应用的页面映射到名称上。你可以使用该名称来引用实际的页面。这个避免了在 web 页面上硬编码 URLs。</p>
</td>
</tr> 
<tr>
<td>4</td>
<td><b>action-mappings</b>
<p>它是你声明表单处理程序的位置，他们也被称为<b>动作映射</b>。</p>
</td>
</tr> 
<tr>
<td>5</td>
<td><b>controller</b>
<p>这个部分配置 Struts 内部，而且很少在实际情况中使用。</p>
</td>
</tr> 
<tr>
<td>6</td>
<td><b>plug-in</b>
<p>这个部分告诉 Struts 在哪里找到包含提示和错误信息的属性文件。</p>
</td>
</tr> 
</table>


下面是示例 struts-config.xml 文件：

<pre class="prettyprint notranslate">
&lt;?xml version="1.0" encoding="ISO-8859-1" ?&gt;
&lt;!DOCTYPE struts-config PUBLIC
"-//Apache Software Foundation//DTD Struts Configuration 1.0//EN"
"http://jakarta.apache.org/struts/dtds/struts-config_1_0.dtd"&gt;

&lt;struts-config&gt;

   &lt;!-- ========== Form Bean Definitions ============ --&gt;
   &lt;form-beans&gt;
      &lt;form-bean name="login" type="test.struts.LoginForm" /&gt;
   &lt;/form-beans&gt;

   &lt;!-- ========== Global Forward Definitions ========= --&gt;
   &lt;global-forwards&gt;
   &lt;/global-forwards&gt;

   &lt;!-- ========== Action Mapping Definitions ======== --&gt;
   &lt;action-mappings&gt;
      &lt;action
         path="/login"
         type="test.struts.LoginAction" &gt;

         &lt;forward name="valid" path="/jsp/MainMenu.jsp" /&gt;
         &lt;forward name="invalid" path="/jsp/LoginView.jsp" /&gt;
      &lt;/action&gt;
   &lt;/action-mappings&gt;

   &lt;!-- ========== Controller Definitions ======== --&gt;
   &lt;controller 
      contentType="text/html;charset=UTF-8"
      debug="3"
      maxFileSize="1.618M"
      locale="true"
      nocache="true"/&gt;

&lt;/struts-config&gt;
</pre>


关于 struts-config.xml 文件更多的详细信息，请查看你的 struts 文档。

## struts.properties 文件

这个配置文件提供了一种改变框架的默认行为的机制。实际上，包含在 **struts.properties** 配置文件内的所有属性也可以在 **web.xml** 中使用 **init-param** 被配置，同样也可以在 **struts.xml** 配置文件中使用 **constant** 标签。但是如果你喜欢保持事情分离和有更多特定的 struts，你就可以在文件夹 **WEB-INF/classes** 下创建这个文件。

在这个文件中配置的值将重写在 **default.properties** 中配置的默认值，default.properties 包含在 struts2-core-x.y.z.jar 分布中。这里有几个属性，你可能会考虑使用 **struts.properties** 文件改变它们：

<pre class="prettyprint notranslate">
### When set to true, Struts will act much more friendly for developers
struts.devMode = true

### Enables reloading of internationalization files
struts.i18n.reload = true

### Enables reloading of XML configuration files
struts.configuration.xml.reload = true

### Sets the port that the server is run on
struts.url.http.port = 8080
</pre>


在这里，任何以井号（＃）开始的行会被假定为注释，它将被 Struts 2 忽略。
