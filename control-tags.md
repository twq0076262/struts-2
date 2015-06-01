# 控制标签

Struts 2 有一组标签使得控制页面执行流非常容易。以下是重要的 Struts 2 控制标签的列表：

## if 和 else 标签

该标签实现基本的能够在每种语言中找到的条件流。'If' 标签能够单独使用或与 'Else If' 标签一起使用，单个/多个 'Else' 标签如下所示：

``` 
<s:if test="%{false}">
    <div>Will Not Be Executed</div>
</s:if>
<s:elseif test="%{true}">
    <div>Will Be Executed</div>
</s:elseif>
<s:else>
    <div>Will Not Be Executed</div>
</s:else>
```

## 迭代标签

**迭代**标签会迭代一个值。一个迭代的值可以是任何 java.util.Collection 或 java.util.Iterator。当迭代一个值时，你可以使用 **Sort** 标签来把结果分类或者使用 **SubSet** 标签得到列表或数组的子集。

以下例子检索了值栈中当前对象的 getDays() 方法的值，并用它迭代。<s:property/> 标签输出了当前迭代的值。

<pre class="prettyprint notranslate">
&lt;s:iterator value="days"&gt;
  &lt;p&gt;day is: &lt;s:property/&gt;&lt;/p&gt;
&lt;/s:iterator&gt;
</pre>

## 融合标签

**融合**标签将两个或多个列表作为参数并把它们融合在一起，如下所示：

``` 
<s:merge var="myMergedIterator">
     <s:param value="%{myList1}" />
     <s:param value="%{myList2}" />
     <s:param value="%{myList3}" />
</s:merge>
<s:iterator value="%{#myMergedIterator}">
     <s:property />
</s:iterator>
```

## 附加标签

**附加**标签将两个或多个列表作为参数并把它们附加在一起，如下所示：

``` 
<s:append var="myAppendIterator">
     <s:param value="%{myList1}" />
     <s:param value="%{myList2}" />
     <s:param value="%{myList3}" />
</s:append>
<s:iterator value="%{#myAppendIterator}">
     <s:property />
</s:iterator>
```

## 生成器标签

**生成器**标签生成基于提供的 val 属性的迭代器。下面的例子中，生成器标签生成了一个迭代器并用迭代器标签把它输出出来。

``` 
<s:generator val="%{'aaa,bbb,ccc,ddd,eee'}">
 <s:iterator>
     <s:property /><br/>
 </s:iterator>
</s:generator>
```

