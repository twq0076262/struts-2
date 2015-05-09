# Struts2 - 主题 & 模板

在开始本章教程之前，让我们看几个 *http://struts.apache.org* 给出的定义：

<table class="table table-bordered"> 
<tr>
<th style="width:25%">项</th>
<th>描述</th>
</tr> 
<tr>
<td><b>标签</b></td>
<td>从JSP，FreeMarker 或 Velocity 内部执行的代码小片段</td>
</tr> 
<tr>
<td><b>模板</b></td>
<td>一小段代码，通常在 FreeMarker 中编写，并且通过某种标签能够被呈现出来（HTML 标签）</td>
</tr> 
<tr>
<td><b>主题</b></td>
<td>打包到一起的模板的集合，用来提供自定义功能的。</td>
</tr> 
</table>

我还建议浏览 [**Struts2 本地化**](http://www.tutorialspoint.com/struts_2/struts_localization.htm)章节，因为我们会再次采用相同的例子来完成我们的实践。

当你在你的 web 页面上使用一个 Struts 2 标签时，如 <s:submit...>，<s:textfield...> 等，Struts 2 框架会生成 HTML 代码和预配置的样式及布局。Struts 2 有三种内置的主题：

<table class="table table-bordered"> 
<tr>
<th style="width:25%">主题</th>
<th>描述</th>
</tr> 
<tr>
<td><b>simple theme</b></td>
<td>一个最小的主题，不带有 "bells and whistles"。例如，文本框标签呈现不带有标记，验证，错误报告，或其他任何格式化或功能的 HTML &lt;input/&gt; 标签。</td>
</tr> 
<tr>
<td><b>xhtml theme</b></td>
<td>这是 Struts 2 使用的默认的主题，提供了所有简单主题提供的基础，并添加了几个功能，如为 HTML 添加的标准的两列表布局，为每个 HTML 添加的标记，验证和错误报告等等。</td>
</tr> 
<tr>
<td><b>css_xhtml theme</b></td>
<td>这个主题提供了所有简单主题提供的基础，并添加了几个功能，如标准的两列基于 CSS 的布局，为 HTML Struts 标签使用 &lt;div&gt;，为每个 HTML Struts 标签添加布局，根据 CSS 样式表替换。</td>
</tr> 
</table>

正如上面提到的，如果你没有指定一个主题，那么 Struts 2 会使用默认的 xhtml 主题。例如这个 Struts 2 选择标签：

``` 
<s:textfield name="name" label="Name" />
```

产生如下所示的 HTML 标记：

``` 
<tr>
<td class="tdLabel">
   <label for="empinfo_name" class="label">Name:</label>
</td><td>
   <input type="text" name="name" value="" id="empinfo_name"/>
</td>
</tr>
```

这里 **empinfo** 是在 struts.xml 文件中定义的操作名。

## 选择主题

你可以在每个 Struts 2 标签基础上选择主题或者你可以使用下述方法中的一个来指定 Struts 2 要用的主题：

- 特定标签上的主题属性

- 在标签的环绕表单标签上的主题属性

- 命名为“主题”的限定页面范围的属性

- 命名为“主题”的限定请求范围的属性

- 命名为“主题”的限定会话范围的属性

- 命名为“主题”的限定应用范围的属性

- 在 struts.properties 中的 struts.ui.theme 属性 (xhtml 的默认值)

如果你不想为不同的标签使用不同的主题，以下是在标签级别指定一个主题的语法：

``` 
<s:textfield name="name" label="Name" theme="xhtml"/>
```

由于在每个标签上都使用主题是不太实际的，所以简单来说，我们可以使用下列标签在 **struts.properties** 文件中指定规则：

<pre class="prettyprint notranslate">
# Standard UI theme
struts.ui.theme=xhtml
# Directory where theme template resides
struts.ui.templateDir=template
# Sets the default template type. Either ftl, vm, or jsp
struts.ui.templateSuffix=ftl
</pre>

以下是我们从本地化章节中选取的结果，我们使用了默认的主题并设置了 **struts-default.properties** 文件中的 **struts.ui.theme=xhtml**，该文件是 struts2-core.xy.z.jar 文件中默认的。

![](images/helloworldstruts14.gif)

## 主题怎样工作？

对于一个给定的主题，每一个 struts 标签都有一个相关的模板，如 **s:textfield -> text.ftl** 和 **s:password -> password.ftl** 等。这些模板文件压缩到 struts2-core.xy.z.jar 文件中。这些模板文件为每个标签保存一个预定义的 HTML 布局。所以 Struts 2 框架用 Sturts 标签和相关的模板生成最终的 HTML 标记代码。

``` 
Struts 2 tags + Associated template file = Final HTML markup code.
```

默认的模板已经被写入 FreeMarker 中并且它们有扩展版本 **.ftl**。你可以使用 velocity 或 JSP 来设计自己的模板，因此可以使用 **struts.ui.templateSuffix** 和 **struts.ui.templateDir** 在 struts.properties 中设置配置。

## 创建新的主题

创建新主题的最简单的方式是复制任何现存的主题/模板文件并做一些必需的修改。所以让我们以在 *WebContent/WEB-INF/classes* 中创建一个命名为 **template** 的文件夹开始，并创建一个我们的新的主题命名的子文件夹，如 *WebContent/WEB-INF/classes/template/mytheme*。从这里开始，你可以构建模板，或者你可以从 Struts2 发行版中复制模板并根据需要修改它们。

处于学习的目的，我们要修改一些现存的默认的模板 **xhtml**。所以现在让我们复制 *struts2-core-x.y.z.jar/template/xhtml* 的内容到我们的主题目录中并只修改 *WebContent/WEB-INF/classes/template/mytheme/control.ftl* 文件。当我们打开 **control.ftl** 时，它会有如下所示的行：

<pre class="prettyprint notranslate">
&lt;table class="${parameters.cssClass?default('wwFormTable')?html}"&lt;#rt/&gt;
&lt;#if parameters.cssStyle??&gt; style="${parameters.cssStyle?html}"&lt;#rt/&gt;
&lt;/#if&gt;
&gt;
</pre>

让我们修改上述文件 **control.ftl**，使得它包含以下内容：

``` 
<table style="border:1px solid black;">
```

如果你检查 **form.ftl**，你会发现 **control.ftl** 正在该文件中使用，而 form.ftl 文件正在从  xhtml 主题引用该文件。所以让我们做出如下所示的修改：

<pre class="prettyprint notranslate">
&lt;#include "/${parameters.templateDir}/xhtml/form-validate.ftl" /&gt;
&lt;#include "/${parameters.templateDir}/simple/form-common.ftl" /&gt;
&lt;#if (parameters.validate?default(false))&gt;
  onreset="${parameters.onreset?default('clearErrorMessages(this);\
  clearErrorLabels(this);')}"
&lt;#else&gt;
  &lt;#if parameters.onreset??&gt;
  onreset="${parameters.onreset?html}"
  &lt;/#if&gt;
&lt;/#if&gt;
&gt;
<span style="color:red; font-weight:bold;">&lt;#include "/${parameters.templateDir}/mytheme/control.ftl" /&gt;</span>
</pre>

我假设你不太理解 **FreeMarker** 模板语言，但是你仍然能知道通过浏览 .ftl 文件需要做什么。但是，让我们保存上述改变，然后回到我们的本地化实例中，并创建 **WebContent/WEB-INF/classes/struts.properties** 文件，其内容如下所示：

<pre class="prettyprint notranslate">
# Customized them
struts.ui.theme=mytheme
# Directory where theme template resides
struts.ui.templateDir=template
# Sets the template type to ftl.
struts.ui.templateSuffix=ftl
</pre>

现在，做出改变之后，鼠标右键单击项目名，点击 **Export > WAR File** 来创建一个 War 文件。然后将这个 WAR 文件部署到 Tomcat 的 web 应用程序目录中。最后，启动 Tomcat 服务器并尝试访问 URL http://localhost:8080/HelloWorldStruts2。这将显示如下所示的画面：

![](images/helloworldstruts19.gif)

你可以在表单组件的周围看到一个边界，这是从 xhtml 主题中复制主题并做出改变的结果。如果你没有学习 FreeMarker，那么你可以很容易的创建或修改你的主题。至少现在你对 Sturts 2 主题和模板有一个基本的了解，不是吗？