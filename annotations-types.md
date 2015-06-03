# Struts 2 注解类型

Struts 2 应用程序可以使用 Java 5 注解作为 XML 和 Java 属性配置的一个替代。这里是和不同类别相关的最重要的注解列表：

##Namespace 注解（动作注解）

@Namespace 注解允许在 **Action** 类中允许定义一个动作的 namespace，而不是基于 Zero 配置的约定。

``` 
@Namespace("/content")
public class Employee extends ActionSupport{
  ...
}
``` 

##Result 注解 -（动作注解）

@Result 注解允许在 Action 类中定义动作结果，而不是在一个 XML 文件中。

```
@Result(name="success", value="/success.jsp")
public class Employee extends ActionSupport{
 ...
}
```

##Results 注解 -（动作注解）

@Results 注解为一个 Action 定义了一组结果。

```
@Results({
   @Result(name="success", value="/success.jsp"),
   @Result(name="error", value="/error.jsp")
})
public class Employee extends ActionSupport{
 ...
}
```

##After 注解 -（拦截注解）

@After 注解标记一个在主动作方法之后需要调用的动作方法，并且结果被执行。返回值将被忽略。

```
public class Employee extends ActionSupport{
   @After
   public void isValid() throws ValidationException {
      // validate model object, throw exception if failed
   }
   public String execute() {
      // perform secure action
      return SUCCESS;
   }
}
```

##Before 注解 -（拦截注解）

@Before 注解标记一个在主动作方法之前需要调用的动作方法，并且结果被执行。返回值将被忽略。

```
public class Employee extends ActionSupport{
   @Before
   public void isAuthorized() throws AuthenticationException {
      // authorize request, throw exception if failed
   }
   public String execute() {
      // perform secure action
      return SUCCESS;
   }
}
```

##BeforeResult 注解 -（拦截注解）

@BeforeResult 注解标记一个在结果之前需要执行的动作方法。返回值将被忽略。

```
public class Employee extends ActionSupport{
   @BeforeResult
   public void isValid() throws ValidationException {
    // validate model object, throw exception if failed
   }
   public String execute() {
      // perform action
      return SUCCESS;
   }
}
```

##ConversionErrorFieldValidator 注解 -（验证注解）

这个验证注解检查一个字段是否有任何转换错误，如果转换错误存在，则应用它们。

```
public class Employee extends ActionSupport{
   @ConversionErrorFieldValidator(message = "Default message", 
                        key = "i18n.key", shortCircuit = true)
   public String getName() {
       return name;
   }
}
```

##DateRangeFieldValidator 注解 -（验证注解）

这个验证注解检查一个日期字段有一个值在指定的范围内。

```
public class Employee extends ActionSupport{
   @DateRangeFieldValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true, 
   min = "2005/01/01", max = "2005/12/31")
   public String getDOB() {
       return dob;
   }
}
```

##DoubleRangeFieldValidator 注解 -（验证注解）

这个验证注解检查一个 double 字段有一个值在指定的范围内。如果设置的既不是最小的也不是最大的，那么什么都不要做。

```
public class Employee extends ActionSupport{
   @DoubleRangeFieldValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true, 
   minInclusive = "0.123", maxInclusive = "99.987")
   public String getIncome() {
       return income;
   }
}
```

##EmailValidator 注解 -（验证注解）

这个验证注解检查一个字段是一个有效的 e-mail 地址，如果它包含一个非空的字符串。

```
public class Employee extends ActionSupport{
   @EmailValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true)
   public String getEmail() {
       return email;
   }
}
```

##ExpressionValidator 注解 -（验证注解）

这个非字段级验证器验证一个提供的正则表达式。

```
@ExpressionValidator(message = "Default message", key = "i18n.key", 
shortCircuit = true, expression = "an OGNL expression" )
```

##IntRangeFieldValidator 注解 -（验证注解）

这个验证注解检查一个数字字段有一个值在指定的范围内。如果设置的既不是最小的也不是最大的，那么什么都不要做。

```
public class Employee extends ActionSupport{
   @IntRangeFieldValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true, 
   min = "0", max = "42")
   public String getAge() {
       return age;
   }
}
```

##RegexFieldValidator 注解 -（验证注解）

这个注解使用一个正则表达式来验证一个字符串字段。

```
@RegexFieldValidator( key = "regex.field", expression = "yourregexp")
```

##RequiredFieldValidator 注解 - 验证注解）

这个验证注解检查一个字段是非空的。这个注解必须应用在方法层。

```
public class Employee extends ActionSupport{
   @RequiredFieldValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true)
   public String getAge() {
       return age;
   }
}
```

##RequiredStringValidator 注解 -（验证注解）

这个验证注解检查一个字符串字段不是空的（即非空，长度 > 0）。

```
public class Employee extends ActionSupport{
   @RequiredStringValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true, trim = true)
   public String getName() {
       return name;
   }
}
```

##StringLengthFieldValidator 注解 -（验证注解）

这个验证器检查一个字符串字段是正确的长度。假定该字段是一个字符串。如果设置的既不是最小长度也不是最大长度，那么什么都不要做。

```
public class Employee extends ActionSupport{
   @StringLengthFieldValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true, 
   trim = true, minLength = "5",  maxLength = "12")
   public String getName() {
       return name;
   }
}
```

##UrlValidator 注解 -（验证注解）

这个验证器检查一个字段是一个有效的 URL。

```
public class Employee extends ActionSupport{
   @UrlValidator(message = "Default message", 
   key = "i18n.key", shortCircuit = true)
   public String getURL() {
       return url;
   }
}
```

##Validations 注解 -（验证注解）

如果你想使用多个相同类型的注解，这些注解必须在 @Validations() 注解中嵌套。

```
public class Employee extends ActionSupport{
  @Validations(
   requiredFields =
      {@RequiredFieldValidator(type = ValidatorType.SIMPLE, 
      fieldName = "customfield", 
      message = "You must enter a value for field.")},
   requiredStrings =
      {@RequiredStringValidator(type = ValidatorType.SIMPLE, 
      fieldName = "stringisrequired", 
      message = "You must enter a value for string.")}
   )
   public String getName() {
       return name;
   }
}
```

##CustomValidator 注解 -（验证注解）
这个注解可以用于自定义验证器。使用 ValidationParameter 注解来提供额外的参数。

```
@CustomValidator(type ="customValidatorName", fieldName = "myField")
```

##Conversion 注解 -（类型转换注解）

在类型层中，这是类型转换的一个标记注解。Conversion 注解必须应用在类型层。

```
@Conversion()
   public class ConversionAction implements Action {
}
```

##CreateIfNull 注解 - 类型转换注解）

这个注解为类型转换设置为 CreateIfNull。CreateIfNull 注解必须应用在字段或方法层。

```
@CreateIfNull( value = true )
private List<User> users;
```

##Element 注解 -（类型转换注解）

这个注解为类型转换设置为 Element。Element 注解必须应用在字段或方法层。

```
@Element( value = com.acme.User )
private List<User> userList;
```

##Key 注解 -（类型转换注解）

这个注解为类型转换设置为 Key。Key 注解必须应用在字段或方法层。

```
@Key( value = java.lang.Long.class )
private Map<Long, User> userMap;
```

##KeyProperty 注解 -（类型转换注解）

这个注解为类型转换设置为 KeyProperty。KeyProperty 注解必须应用在字段或方法层。

```
@KeyProperty( value = "userName" )
protected List<User> users = null;
```

##TypeConversion 注解 -（类型转换注解）

这个注解的注解用于类和应用程序范围的转换规则。TypeConversion 注解必须应用在属性或方法层。

```
@TypeConversion(rule = ConversionRule.COLLECTION, 
converter = "java.util.String")
public void setUsers( List users ) {
   this.users = users;
}
```
