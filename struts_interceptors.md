# Struts 2 - 拦截器

拦截器在概念上和servlet过滤器或JDKs代理类一样。拦截器允许横切功能在动作和框架中单独实现。你可以使用拦截器实现下面的内容：

- 在动作被调用之前提供预处理逻辑。

- 在动作被调用之后提供预处理逻辑。

- 捕获异常，以便可以执行交替处理。

Struts2 框架提供的许多功能都是使用拦截实现的；例如包括异常处理，文件上传，生命周期回调和验证等。事实上，由于 Struts2 是许多拦截器功能的基础，所以每次动作不是不可能有 7 个或 8 个拦截器被分配。

## Struts2 框架的拦截器

Struts 2 框架提供了一列开箱即用的拦截器来预先设定和准备使用。下面列出了几个重要的拦截器：

<table class="table table-bordered"> 
<tr>
<th style="width:5">序号 </th>
<th>拦截器及描述</th>
</tr>
<tr>
<td>1</td>
<td><b>alias</b>
<p>允许参数有不同的跨请求的别名。</p>
</td>
</tr> 
<tr>
<td>2</td>
<td><b>checkbox</b>
<p>通过为没有被检查的复选框添加一个参数值 false 来协助管理复选框。</p>
</td>
</tr> 
<tr>
<td>3</td>
<td><b>conversionError</b>
<p>把从字符串转化为参数类型的错误信息放置到动作的字段错误中。</p>
</td>
</tr> 
<tr>
<td>4</td>
<td><b>createSession</b>
<p>如果不存在 HTTP 会话，则自动创建一个 HTTP 会话。</p>
</td>
</tr> 
<tr>
<td>5</td>
<td><b>debugging</b>
<p>为开发人员提供几种不同的调试屏幕。</p>
</td>
</tr> 
<tr>
<td>6</td>
<td><b>execAndWait</b>
<p>当动作在后台执行的时侯，把用户定向到一个中间的等待页面。</p>
</td>
</tr> 
<tr>
<td>7</td>
<td><b>exception</b>
<p>映射动作抛出的异常到一个结果中，通过重定向允许自动异常处理。</p>
</td>
</tr> 
<tr>
<td>8</td>
<td><b>fileUpload</b>
<p>有利于简单的文件上传。</p>
</td>
</tr> 
<tr>
<td>9</td>
<td><b>i18n</b>
<p>在用户的会话期间，跟踪选定的语言环境。</p>
</td>
</tr> 
<tr>
<td>10</td>
<td><b>logger</b>
<p>通过输出被执行的动作的名称提供简单的日志。</p>
</td>
</tr> 
<tr>
<td>11</td>
<td><b>params</b>
<p>设置动作的请求参数。</p>
</td>
</tr> 
<tr>
<td>12</td>
<td><b>prepare</b>
<p>它通常是用来做预处理工作，如设置数据库连接。</p>
</td>
</tr> 
<tr>
<td>13</td>
<td><b>profile</b>
<p允许记录动作的简单的配置信息。</p>
</td>
</tr> 
<tr>
<td>14</td>
<td><b>scope</b>
<p>在会话或应用程序的范围中存储和检索动作的状态。</p>
</td>
</tr> 
<tr>
<td>15</td>
<td><b>ServletConfig</b>
<p>为行动提供了各种基于 servlet 信息的访问。</p>
</td>
</tr> 
<tr>
<td>16</td>
<td><b>timer</b>
<p>以动作需要多长时间执行的形式提供了简单的配置信息。</p>
</td>
</tr> 
<tr>
<td>17</td>
<td><b>token</b>
<p>为有效的标记检查动作用来防止重复地表单提交。</p>
</td>
</tr> 
<tr>
<td>18</td>
<td><b>validation</b>
<p>为动作提供了验证支持。</p>
</td>
</tr> 
</table>

关于上面提到的拦截器的完整信息，请查看 Struts 2 的文档。但是我会告诉你通常如何在你的 Struts 应用程序中使用一个拦截器。

## 如何使用拦截器？

让我们来看看如何在我们的 “Hello World” 程序中使用已存在的拦截器。我们将使用 **timer** 拦截器，它的目的是测量它多长时间执行一个动作的方法。同时我使用 **params** 拦截器，它的目的是给动作发送请求参数。你可以尝试在你的例子中不使用这个拦截器，你将会发现 **name** 属性没有被设置，因为参数是无法达到动作中的。

我们将保留 HelloWorldAction.java，web.xml，HelloWorld.jsp 和index.jsp 文件，因为他们已经在 Examples 章节被创建了，但是让我们修改 **struts.xml** 文件，添加一个拦截器，如下所示：

<pre class="prettyprint notranslate"> 
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE struts PUBLIC
   "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
   "http://struts.apache.org/dtds/struts-2.0.dtd"&gt;
&lt;struts&gt;
   &lt;constant name="struts.devMode" value="true" /&gt;
   &lt;package name="helloworld" extends="struts-default"&gt;
      &lt;action name="hello" 
         class="com.tutorialspoint.struts2.HelloWorldAction"
         method="execute"&gt;
         &lt;interceptor-ref name="params"/&gt;
         &lt;interceptor-ref name="timer" /&gt;
         &lt;result name="success"&gt;/HelloWorld.jsp&lt;/result&gt;
      &lt;/action&gt;
   &lt;/package&gt;
&lt;/struts&gt;
</pre>  

右键单击项目名称，并且单击 **Export > WAR File** 来创建一个 War 文件。然后在 Tomcat 的 webapps 目录下部署这个 WAR。最后，启动 Tomcat 服务器和尝试访问 URL http://localhost:8080/HelloWorldStruts2/index.jsp。将会给出下面的画面：

![](images/helloworldstruts4.jpg)

现在，在给定的文本框中输入任何单词，并且单击 Say Hello 按钮执行已定义的动作。现在，如果你查看生成的日志，就会发现下面的文字：

```
INFO: Server startup in 3539 ms
27/08/2011 8:40:53 PM 
com.opensymphony.xwork2.util.logging.commons.CommonsLogger info
INFO: Executed action [//hello!execute] took 109 ms.
```

在这里最后一行是因为 **timer** 拦截器生成长的，它告诉动作被执行的时间的 109ms。

## 创建自定义的拦截器

在你的应用程序中使用自定义的拦截器是一种提供横切的应用功能的简洁的方式。创建一个自定义的拦截器是很容易的，需要扩展的接口是下面的 **Interceptor** 接口：

```
public interface Interceptor extends Serializable{
   void destroy();
   void init();
   String intercept(ActionInvocation invocation)
   throws Exception;
}
```

正如名称所显示的，init() 方法提供了一种初始化拦截器的方法，而destroy() 方法提供了一种清理拦截器的工具。与动作不同的是，拦截器在请求之间被重用，而且需要是线程安全的，尤其是 intercept() 方法。 

**ActionInvocation** 对象提供运行时环境的访问。它允许访问动作本身和方法来调用该动作，并判定动作是否已经被调用。

如果你不需要初始化或清理代码，可以扩展 **AbstractInterceptor** 类。它提供了一个对 init() 和 destroy() 方法的默认的无操作实现。

## 创建拦截器类
让我们在 **Java Resources > src** 文件夹中创建下面的**MyInterceptor.java**：

```
package com.tutorialspoint.struts2;
import java.util.*;
import com.opensymphony.xwork2.ActionInvocation;
import com.opensymphony.xwork2.interceptor.AbstractInterceptor;
public class MyInterceptor extends AbstractInterceptor {
   public String intercept(ActionInvocation invocation)throws Exception{
      /* let us do some pre-processing */
      String output = "Pre-Processing"; 
      System.out.println(output);
      /* let us call action or next interceptor */
      String result = invocation.invoke();
      /* let us do some post-processing */
      output = "Post-Processing"; 
      System.out.println(output);
      return result;
   }
}
```

如你注意到的，实际的动作将通过使用拦截器调用 **invocation.invoke()** 来执行。所以，你可以根据你的需求做一些预处理和一些后处理。

这个框架本身通过第一次调用 ActionInvocation 对象的 invoke() 来启动过程。每次 **invoke()** 被调用，ActionInvocation 查询它的状态，并且执行接下来的拦截器。当所有已配置的拦截器已经被配置时，invoke() 方法将引发这个动作本身被执行。下面的图通过请求流显示了相同的概念：

![](images/actioninvocation.jpg)

## 创建动作类

让我们在 **Java Resources > src**　中名为 **com.tutorialspoint.struts2** 的包下创建一个 java 文件HelloWorldAction.java，它的内容在下面给出。

```
package com.tutorialspoint.struts2;
import com.opensymphony.xwork2.ActionSupport;
public class HelloWorldAction extends ActionSupport{
   private String name;
   public String execute() throws Exception {
      System.out.println("Inside action....");
      return "success";
   }  
   public String getName() {
      return name;
   }
   public void setName(String name) {
      this.name = name;
   }
}
```

我们已经在前面的例子中看到这个相同的类。我们对于 “name” 属性有标准的 getters 和 setters 方法，还有返回字符串 “success” 的 execute 方法。

## 创建视图

让我们在 eclipse 项目的 WebContent 文件夹中创建下面的 jsp 文件 **helloWorld.jsp**。

<pre class="prettyprint notranslate">
&lt;%@ page contentType="text/html; charset=UTF-8" %&gt;
&lt;%@ taglib prefix="s" uri="/struts-tags" %&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Hello World&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
   Hello World, &lt;s:property value="name"/&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

## 创建主页面

我们还需要在 WebContent 文件夹中创建 **index.jsp**。这个文件将作为初始动作 URL，用户可以点击它告诉 Struts 2 框架调用HelloWorldAction 类定义的方法，并且呈现 HelloWorld.jsp 视图。

<pre class="prettyprint notranslate">
&lt;%@ page language="java" contentType="text/html; charset=ISO-8859-1"
   pageEncoding="ISO-8859-1"%&gt;
&lt;%@ taglib prefix="s" uri="/struts-tags"%&gt;
   &lt;!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd"&gt;
&lt;html&gt;
&lt;head&gt;
&lt;title&gt;Hello World&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
   &lt;h1&gt;Hello World From Struts2&lt;/h1&gt;
   &lt;form action="hello"&gt;
      &lt;label for="name"&gt;Please enter your name&lt;/label&gt;&lt;br/&gt;
      &lt;input type="text" name="name"/&gt;
      &lt;input type="submit" value="Say Hello"/&gt;
   &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>

上面的视图文件中定义的 hello 动作将使用 struts.xml 文件映射到 HelloWorldAction 类和它的 execute 方法中。

## 配置文件

现在，我们需要注册我们的拦截器，然后调用它，就如我们已经在前面的例子中调用了默认的拦截器一样。为了注册一个新定义的拦截器，可以把 <interceptors>...</interceptors> 标签直接放置在 **struts.xml** 文件 <package> 标签内。对于默认的拦截器，你可以跳过这一步，就像我们在前面的例子中一样。但在这里让我们注册和使用它，如下所示：

<pre class="prettyprint notranslate"> 
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE struts PUBLIC
    "-//Apache Software Foundation//DTD Struts Configuration 2.0//EN"
    "http://struts.apache.org/dtds/struts-2.0.dtd"&gt;

&lt;struts&gt;
   &lt;constant name="struts.devMode" value="true" /&gt;
   &lt;package name="helloworld" extends="struts-default"&gt;

      &lt;interceptors&gt;
         &lt;interceptor name="myinterceptor"
            class="com.tutorialspoint.struts2.MyInterceptor" /&gt;
      &lt;/interceptors&gt;

      &lt;action name="hello" 
         class="com.tutorialspoint.struts2.HelloWorldAction" 
         method="execute"&gt;
         &lt;interceptor-ref name="params"/&gt;
         &lt;interceptor-ref name="myinterceptor" /&gt;
         &lt;result name="success"&gt;/HelloWorld.jsp&lt;/result&gt;
      &lt;/action&gt;

   &lt;/package&gt;
&lt;/struts&gt;
</pre>

应该注意的是，你可以在 **<package>** 标签内注册多个拦截器，并且同时你可以在 **<action>** 标签内调用多个拦截器。你可以用不同的动作调用相同的拦截器。

web.xml 文件需要在 WebContent 的 WEB-INF 文件夹下创建，如下所示：

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

右键单击项目名称，并且单击 **Export > WAR File** 来创建一个 War文件。然后在 Tomcat 的 webapps 目录下部署这个 WAR。最后，启动Tomcat 服务器和尝试访问 URL http://localhost:8080/HelloWorldStruts2/index.jsp。将会给出下面的画面：

![](images/helloworldstruts4.jpg)

现在，在给定的文本框中输入任何单词，并且单击 Say Hello 按钮执行已经定义的动作。现在，如果你查看生成的日志，就会在底部发现下面的文字：

```
Pre-Processing
Inside action....
Post-Processing
```

## 堆叠多个拦截器

可想而知，为每个动作配置多个拦截器很快就会变得非常难以管理。为此，拦截器用拦截器栈进行管理。这儿有一个例子，直接来自 struts-default.xml 文件：

```
<interceptor-stack name="basicStack">
   <interceptor-ref name="exception"/>
   <interceptor-ref name="servlet-config"/>
   <interceptor-ref name="prepare"/>
   <interceptor-ref name="checkbox"/>
   <interceptor-ref name="params"/>
   <interceptor-ref name="conversionError"/>
</interceptor-stack>
```

上面的栈被称为 **basicStack**，它可以用在你的配置中，如下所示。这个配置节点被放置在 <package.../> 节点下。每个 <interceptor-ref.../> 标签引用一个拦截器或在当前的拦截器栈之前已配置的拦截器栈。因此，当配置初始的拦截器和拦截器栈时，确保在所有拦截器和拦截器栈配置中这个名称是唯一的，这是非常重要的。
 
我们已经看到了如何应用拦截器到动作中，应用拦截器栈是没有什么不同的。实际上，我们完全使用相同的标签：

```
<action name="hello" class="com.tutorialspoint.struts2.MyAction">
   <interceptor-ref name="basicStack"/>
   <result>view.jsp</result>
</action
```

上述注册的 “basicStack” 将完整地注册所有带有 hello 动作的 6 个拦截器。应该指出的是，拦截器按照已配置的顺序执行。例如，在上述情况下，将首先执行异常，第二个执行的是 servlet 配置等等。