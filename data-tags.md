# Struts 2 - 数据标签

Struts 2 的 **数据标签**主要用于操作显示在页面中的数据。以下列出的是重要的数据标签：

## 操作标签

该标签允许开发人员通过指定操作名称和可选的名称空间来从 JSP 页面直接调用操作。该标签的主题内容用于呈现来自操作的结果。在 struts.xml 文件中任何为该操作定义的结果处理器都将被忽略，除非指定了 executeResult 参数。

<pre class="prettyprint notranslate">
&lt;div&gt;Tag to execute the action&lt;/div&gt;
&lt;br /&gt;
&lt;s:action name="actionTagAction" executeResult="true" /&gt;
&lt;br /&gt;
&lt;div&gt;To invokes special method  in action class&lt;/div&gt;
&lt;br /&gt;
&lt;s:action name="actionTagAction!specialMethod" executeResult="true" /&gt;
</pre>

[**查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_action_tag.htm)

## 包含标签

这些**包含**标签用于在一个 JSP 页面中包含另一个 JSP 文件。

``` 
<-- First Syntax -->
<s:include value="myJsp.jsp" />
<-- Second Syntax -->
<s:include value="myJsp.jsp">
   <s:param name="param1" value="value2" />
   <s:param name="param2" value="value2" />
</s:include>
<-- Third Syntax -->
<s:include value="myJsp.jsp">
   <s:param name="param1">value1</s:param>
   <s:param name="param2">value2</s:param>
</s:include>
```

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_include_tag.htm)

## bean 标签

这些 bean 标签实例化符合 JavaBeans 规范的类。该标签的主体可以包含一组参数元素来在那个类中设置任何设值方法。如果 var 属性设置在 BeanTag 中，那么它会把初始化的 bean 放到栈的上下文中。

``` 
<s:bean name="org.apache.struts2.util.Counter" var="counter">
   <s:param name="first" value="20"/>
   <s:param name="last" value="25" />
</s:bean>
```

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_bean_tag.htm)

## 日期标签

这些**日期**标签允许你以快速简单的方法设置日期格式。你可以指定一个自定义的格式（如 "dd/MM/yyyy hh:mm"），你可以生成简单的可读符号（如 "in 2 hours, 14 minutes"），或者你也可以用你的属性文件中的键 'struts.date.format' 来后退到预定义的格式。

``` 
<s:date name="person.birthday" format="dd/MM/yyyy" />
<s:date name="person.birthday" format="%{getText('some.i18n.key')}" />
<s:date name="person.birthday" nice="true" />
<s:date name="person.birthday" />
```

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_date_tag.htm)

## 参数标签

**参数**标签用于参数化其他标签。这个标签有以下两个参数。

- name（字符串）——参数的名称

- value（对象）——参数的值


<pre class="prettyprint notranslate">
&lt;pre&gt;
&lt;ui:component&gt;
 &lt;ui:param name="key"     value="[0]"/&gt;
 &lt;ui:param name="value"   value="[1]"/&gt;
 &lt;ui:param name="context" value="[2]"/&gt;
&lt;/ui:component&gt;
&lt;/pre&gt;
</pre>

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_param_tag.htm)

## 属性标签

**属性**标签用于获取值的属性，如果不存在指定的属性，那么就会默认为栈顶的属性。

``` 
<s:push value="myBean">
    <!-- Example 1: -->
    <s:property value="myBeanProperty" />
    <!-- Example 2: -->TextUtils
    <s:property value="myBeanProperty" default="a default value" />
</s:push>
```
[**请查看具体的实例**](http://www.tutorialspoint.com/struts_2/struts_property_tag.htm)

## push 标签：

**push** 标签用于栈中 push 值的简单操作。

``` 
<s:push value="user">
    <s:propery value="firstName" />
    <s:propery value="lastName" />
</s:push>
```

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_push_tag.htm)

## set标签

**set** 标签将一个值赋给指定范围中的变量。当你想要为一个复杂的表达式分配一个变量，每次只需要简单的引用这个变量而不需要引用这个复杂的表达式时，这个标签是非常有用的。可用的范围是 **应用程序** ，**会话** ，**请求** ，**页面** 和 **操作**。

```
<s:set name="myenv" value="environment.name"/>
<s:property value="myenv"/>
```

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_set_tag.htm)

## 文本标签

**文本**标签用于呈现 I18n 文本消息。

<pre class="prettyprint notranslate">
&lt;!-- First Example --&gt;
&lt;s:i18n name="struts.action.test.i18n.Shop"&gt;
    &lt;s:text name="main.title"/&gt;
&lt;/s:i18n&gt;

&lt;!-- Second Example --&gt;
&lt;s:text name="main.title" /&gt;

&lt;!-- Third Examlpe --&gt;
&lt;s:text name="i18n.label.greetings"&gt;
   &lt;s:param &gt;Mr Smith&lt;/s:param&gt;
&lt;/s:text&gt;
</pre>

[**请查看具体的示例**](http://www.tutorialspoint.com/struts_2/struts_text_tag.htm)

## url 标签

**url** 标签用于创建 URL。

``` 
<-- Example 1 -->
<s:url value="editGadget.action">
    <s:param name="id" value="%{selected}" />
</s:url>
<-- Example 2 -->
<s:url action="editGadget">
    <s:param name="id" value="%{selected}" />
</s:url>
<-- Example 3-->
<s:url includeParams="get">
    <s:param name="id" value="%{'22'}" />
</s:url>
```

[**请查看具体示例**](http://www.tutorialspoint.com/struts_2/struts_url_tag.htm)
