jstl是一组标准的已定制好的操作，它们应用于各种功能领域。在JSR-52（Java   Specification   Request）中的定义中，jstl包含了   expression   language（EL）、流程控制   和Tag   Library较验器。有关最终版本，你可以产看   http://www.jcp.org/jsr/detail/52.jsp   上的最终草案     
    
  jstl需要运行在JSP   1.2的容器下,它是用来简化JSP的开发,提供更加的方式处理和访问应用数据.     
    
  jstl包含了多中Tag   Library的描述定义(TLDs),这些描述位于一个JAR文件中.这些TLDs涵盖了大多数的功能操作,下面我们会逐一列举,不过在此之前,我们会重点讨论expression   language,它可能算是jstl中最重要的特征了.     
    
  expression   language   (EL)其实是由制定JSR-152(Java   Server   Pages   1.3   Specification)的专家组制定的,事实上很可能EL就将会是JSP   1.3的重要组成部分.EL(目前还是叫SPEL:Simplest   Possible   Expression   Language   )提供了一些简单的语法来直接访问应用数据,支持操作符、Bean、集合，还有类型自动转换、属性的默认值定义等等。     
    
    
  EL的用法：     
  EL总处在在${...}中（就象JSP   在<%...%>中那样）。在属性中只允许出现一个表达式，例如：     
    
  <c:if   test="${product.price   >=   customer.limit}">     
  ...     
  </c:if>     
    
  在上面的例子中，我们使用EL进行比较操作，它还可以和静态文本混合使用，可以看看下面这个例子：     
    
  <c:forEach   var="current">     
  <c:out   value="Product-${current}"/>     
  </c:forEach>     
    
  在这个例子中我们循环遍历一个集合，把current值按一定的文本形式显示出来，结果如下：     
    
  Product-1     
  Product-2     
  Product-3...     
    
  从这个例子你也能看出，使用EL比以前的编码简单了很多。在出现jstl之前，你需要通过先定义对象、了解对象类型、使用相应的脚本来完成一个很简单的操作。     
    
  现在有了jstl，可以使用更加简单的语法进行操作，你看这个例子：     
    
  <jsp:useBean   id="customer"   type="sample.Customer"   scope="request"/>   ...     
  Customer   Name:   <%=customer.getName()%>     
  ...     
  <%   if   (customer.getState().equals("CO")){   %>     
  ...     
  <%}%>     
    
  现在可以使用EL写成:     
    
  Customer   Name:   ${   customer.   name}     
  <c:if   test="${customer.   state   ==   param.   state}">     
  ...     
  </c:if>     
    
  EL支持直接访问所有的JSP数据域（JSP   scopes）的变量，比如我们使用${foo}来代替pageContext.findAttributes("foo")的写法，EL是使用"."号来使用bean的属性，比如：     
    
  ${user.address.city}     
  ${products.[product.id]}     
  ${products.["Part-010"]}     
    
  EL包含了多种操作符:==,   !=,   <,>,   <=,   and   >=,   &&,   ||,   !   .为了避免和XML冲突，还有一些如lt,   gt,   le,   ge,   eq,   和   ne的操作符，以及+、-、/、*、%等算数运算符，还有Boolean运算符and,   or,   not,   和   empty.EL的另一个特征就是自动类型转换,比如:int   value   =   "${request.myValue}",不会报错,EL会把string   转化成int     
    
  另外EL还为变量提供默认的值.这样会避免出现"对空数据操作"的异常.如下的例子显示了如何给变量设置默认值   <c:set   var="city"   value="${user.address.city}"   default="N/A"   />     
    
  现在我们来了解一下EL所支持的操作：     
    
  核心操作     
  EL处在核心tag库中，使用<c:out>tag来表示把EL表达式输出到当前的JspWriter中，它很像JSP的<%=   scripting   exp   %>   表达式。比如下面这个例子：     
    
  <c:out   value="${customer.name}"   default="N/A"   />     
    
  EL还可以设置和删除某个值域中的变量，默认的值域是Page值域（JSP所支持的值域包括application   \session\page   等值域）,例如我们使用<c:set   var="customer"   value=${customer}"   />来设置一个Page值域的变量，然后可以使用<c:remove   var="customer"   />来删除它     
    
  我们还可以使用jstl的tag来catch   ava.lang.Throwable，比如：<c:catch   var="myError"   />，该tag用于统一page中的异常处理。它并意味着完全代替了JSP的出错机制，只是使用这样的tag可以更富条例的控制异常；不需要把作有的错误都导入出错页面，有些错误不需要这样处理，使用<c:catch>   tag可以设计更友好的用户交互     
    
  条件操作     
  相比JSP代码，EL在条件控制上也很强大，使用<c:if>tag就可以构造一个条件表达式，看这个例子：     
    
  <c:if   test="${user.visitCount   ==   1}">     
  Welcome   back!     
    
  </c:if>     
    
  你可以看到这是一个   if   语句，当然还有其他的条件控制符,<c:choose>,   <c:when>,和   <c:otherwise>tag也可以表达出   "if/then/else"的功能     
    
  让我们来看这样一个例子，如果我们需要处理一些结果,可以使用这些tag来为相应的情况显示相应消息：     
    
  <c:choose>     
  <c:when   test="${count   ==   0}">     
  No   records   matched   your   selection.     
  </c:when>     
  <c:otherwise>     
  <c:out   value="${count}"/>   records   matched   your   selection.     
  </c:otherwise>     
  </c:choose>     


**循环操作**
  jstl中最有用的特性就是循环操作了，jstl中支持循环操作的tag是   <c:forEach>,   <c:forToken>,   和   <x:forEach>,还有一些模仿了核心tag用于XML操作的tags，我们稍后介绍，先来看看这些核心tag中的循环操作.     
    
  这些操作支持所有的标准的J2SE的集合类型，包括   List,   LinkedList,   ArrayList,   Vector,   Stack,   和   Set。还包括java.util.Map类的对象比如HashMap,   Hashtable,   Properties,   Provider,   和   Attributes。当然还可以循环遍历对象或基本类型的数组。当使用基本类型时注意，在数组中的项目是它们相应的包装类，比如一个int数组中的元素是Integer，每次循环输入两个对象：当前的元素和循环状态，让我们来看看下面这个例子：     
```html
  <table>     
  <c:forEach   var="product"     
  items="${products}"     
  varStatus="status">     
  <tr>     
  <td><c:out   value="${status.count}"/></td>     
  <td><c:out   value="${product.name}"/></td>     
  </tr>     
  </c:forEach>     
  </table>     
```
  从这个例子我们可以看出，EL把products变量作为集合，每一次输出的当前项设为product，当前状态设为status。     

<c:forEach>,   标签具有以下一些属性： 

           var：迭代参数的名称。在迭代体中可以使用的变量的名称，用来表示每一个迭代变量。类型为String。 

           items：要进行迭代的集合。对于它所支持的类型将在下面进行讲解。 

           varStatus：迭代变量的名称，用来表示迭代的状态，可以访问到迭代自身的信息。 

           begin：如果指定了items，那么迭代就从items[begin]开始进行迭代；如果没有指定items，那么就从begin开始迭代。它的类型为整数。 

           end：如果指定了items，那么就在items[end]结束迭代；如果没有指定items，那么就在end结束迭代。它的类型也为整数。 

           step：迭代的步长。 

           标签的items属性支持Java平台所提供的所有标准集合类型。此外，您可以使用该操作来迭代数组（包括基本类型数组）中的元素。它所支持的集合类型以及迭代的元素如下所示： 

           java.util.Collection：调用iterator()来获得的元素。 

           java.util.Map：通过java.util.Map.Entry所获得的实例。 

           java.util.Iterator：迭代器元素。 

           java.util.Enumeration：枚举元素。 

           Object实例数组：数组元素。 

           基本类型值数组：经过包装的数组元素。 

           用逗号定界的String：分割后的子字符串。 

           javax.servlet.jsp.jstl.sql.Result：SQL查询所获得的行。 

           不论是对整数还是对集合进行迭代，的varStatus 属性所起的作用相同。和var属性一样，varStatus用于创建限定了作用域的变量（改变量只在当前标签体内起作用）。不过，由varStatus属性命名的变量并不存储当前索引值或当前元素，而是赋予javax.servlet.jsp.jstl.core.LoopTagStatus类的实例。该类包含了一系列的特性，它们描述了迭代的当前状态，如下这些属性的含义如下所示： 

           current：当前这次迭代的（集合中的）项。 

           index：当前这次迭代从0开始的迭代索引。 

           count：当前这次迭代从1开始的迭代计数。 

           first：用来表明当前这轮迭代是否为第一次迭代，该属性为boolean类型。 

           last：用来表明当前这轮迭代是否为最后一次迭代，该属性为boolean类型。 

           begin：begin属性的值。 

           end：end属性的值 

           step：step属性的值 
　限制 

　　·假若有begin属性时，begin必须大于等于 0 

　　·假若有end属性时，必须大于begin 

　　·假若有step属性时，step必须大于等于0 

　　Null 和 错误处理 

　　·假若items为null时，则表示为一空的集合对象 

　　·假若begin大于或等于items时，则迭代不运算 

　　说明 

　　如果要循序浏览一个集合对象，并将它的内容显示出来，就必须有items属性。 
------------------------------
  URL操作     
  除了循环操作，核心tag中还包括URL相关的操作。它提供了诸如hyPerlinks,   resource   import,   和   redirect   的功能。使用<c:url>tag可以方便的处理URL的rewriting   和   encoding，让我们来看看下面这个例子：     
    
  <c:url=http://mysite.com/reGISter   var="myUrl">     
  <c:param   name="name"   value="${param.name}"/>     
  </c:url>     
  <   a   href='<c:out   value="${myUrl}"/>'>Register<   /a>     
    
  在jstl中resource   imports也是一项强大的功能，可以方便的指定绝对或相对的路径的外部资源以及FTP资源，我们来看一些例子：     
    
  Absolute   URL:   <c:import   url="http://sample.com/Welcome.html"/>     
  Relative   URL   (to   the   current   context):   <c:import   url="/copyright.html"/>     
  Relative   URL   with   a   foreign   context:   <c:import   url="/myLogo.html"   context="/common"/>     
  FTP   resource:   <c:import   url="ftp://ftp.sample.com/myFile"/>     
    
  从这些例子我们可以看出，<c:import>提供了比<jsp:include>更多的功能,它另外一个优点是可以避免资源内容被多次读入，比如，当你在格式转换(transformation,比如XML通过XSL转换)中使用<jsp:include>来import资源,在include时读入一次,然后所有内容被写入JspWriter，在格式转换中还要被读入一次，使用<c:import>，内容只被读入一次,不写入JspWriter，然后再交由格式转换tag处理     
    
  我们还可以把导入的资源作为一个String或Reader对象来使用,使用varReader或var属性来定义对象名。这个对象是可重用的，并自己有自己的缓冲(cache).使用Reader的可以直接读取数据而没任何暂存(buffering),使用声明过的Reader,必须把它嵌入在   <c:import>   和   </c:import>中使用,比如像下面这个例子     
    
  <c:import   url=http://sample.com/customers   varReader="customers">     
  <mytag:process   in="${customers}"/>     
  </c:import>     
    
  国际化问题     
  jstl中的另一个重要功能是它的国际化格式支持(I18N)。该功能可以对一个特定的语言请求作出相应的响应。它使用了J2SE   的ResourceBundle来保持各种翻译过的语言编码,jstl会根据不同的地区选择适合的ResourceBundle。<fmt:setLocale>用来设置地区，比如<fmt:setLocale   value="es_Es"/>，这等与设定了语言和国家代码。当然还可以指定ResourceBundle，比如：<fmt:bundle   basename="ApplicationResource_fr"/>     
    
  一旦设定了locale（地区）或ResourceBundle,就可以使用<fmt:message>来把原文进行相应的转化,同时还可以进行参数替换,比如:     
    
  <fmt:message   key="welcome">     
  <fmt:param   value="${visitCount}"   />     
  <fmt:message/>     
    
  You   can   also   use   <   fmt:requestEncoding/>   to   set   the   request's   character   encoding.     
  你还可以使用<   fmt:requestEncoding/>来设定请求的字符编码     
    
  能正确显示字符,还只是国际化问题的一半.还必须解决数字和时间的格式解析。不同的地区有不同的显示方法。使用<fmt:formatNumber>   或<fmt:parseNumber>   可以按当地的格式显示数字、货币金额、百分比。同时还可以制定模式（pattern）参数，比如<fmt:formatNumber   value="12.3"   pattern=".00"/>会输出"12.30."     
    
  时间和日期使用<fmt:formatDate>,   <fmt:timeZone>,   <fmt:setTimeZone>,   和   <fmt:parseDate>来处理     
    
  SQL操作     
  SQL操作支持直接访问数据源。在MVC模式中这种做法是会受到警告的，我个人也反对在产品中使用这样的tag，不过对一些快速、小型、简单的开发，他还是会有一些作用，不过不要把它应用到大型应用系统中去。我们来看看SQL操作提供了一些什么功能     
    
  可以使用这些tag来设定数据源、查询数据库、很容易的访问查询结果并可以事务性的更新数据。看下面这个例子如何设定数据源：     
 
  <sql:setDataSource   var="datasource"   driver="org.gjt.mm.MySQL.driver"   url="JDBC:mysql://localhost/db"   />     
     
  <sql:setDataSource>仅仅是封装了JDBC   DriverManager的功能。datasource的属性可以是String或JNDI的相对路径或JDBC   参数串.然后在查询中我们可以这样使用datasource：<sql:query   datasource="${datasource}"   ...   />     
    
  我们来看一个综合使用的例子：     
```
  <sql:query   var="customer"   datasource="${datasource}"     
  SELECT   *   FROM   customers   WHERE   state   =   'CO'   ORDER   BY   city     
  </sql:query>     
  <table>     
  <c:forEach   var="row"   items="${customers.row}">     
  <tr>     
  <td><c:out   value="${row.custName}"   /></td>     
  <td><c:out   value="${row.address}"   /></td>     
  </tr>     
  </c:forEach>     
  </table>     
```
  使用事务性的更新现在很简单了，比如我们现在定义一个事务，你可以把所有需要的更新操作包括在内：     
```html
  <sql:transaction   dataSource="${dataSource}">     
  <sql:update>     
  UPDATE   account   SET   Balance   =Balance   -?   WHERE   accountNo   =   ?     
  <sql:param   value="${transferAmount}"/>     
  <sql:param   value="${accountFrom}"/>     
  </sql:update>     
  </sql:transaction>     
```
  <sql:dateParam>   tag   可以设定在   SQL语句中java.util.Date类型的   "?"(   parameter   markers).在这个例子中没有展示事务级的设定,事务级在java.sql.Connection中设定,如果没有设定事务级,然后在tag中使用它，就会抛出JspTagException.     
    
  XML操作     
  最后我们来看看XML操作，XML操作集是在核心、流程控制、转向操作外的一个操作集，它是建立在Xpath上的。使用Xpath表达式。     
    
  XML   的核心操作很像jstl中核心操作,包括<x:out>,   <x:set>,   和<x:parse>，不同是这些操作tag支持的是XPath表达式的。<x:parse>用来把XML文档解析成数据，数据由XPath引擎处理,如果我们有一个描述一本书的XML文件，我们可以解析它，并使用XPath表达式显示它     
```html
  <c:import   url="http://oreilly.com/book?id=1234"   var="xml"/>     
  <x:parse   source="${xml}"   var="bookInfo"/>     
  <x:out   select="$bookInfo/title"/>     
  <x:out   select="$bookInfo/author"/>     
```
  XML的流程控制也类似于核心集，包括了：if,   choose,   when,   otherwise,   和   forEach   tag，不同的是他们使用XPath表达式.结果对象会按XPath的语义定义转化成相应的boolean值，这些语义规定是：     
  当且仅当一个数是非零正数或非NaN（无穷大）时为true     
  当且仅当一个节点不为空时，值为true     
  当且仅当一个字串的长度不为零时该子串为true     
  XML的转换操作是把XML文档用XSL样式文件显示，但不能获得这些结果，把它们存储在某个变量或值域的属性中，这样的操作只是引入XML和   XSL   文件并完成转换     
```
  <c:import   url="/books"   var="xml"/>     
  <c:import   url="/Web-INF/xslt/bookDisplay.xsl"   var="xslt"/>     
  <x:transform   source="${xml}"   xslt="${xslt}"/>     
```

  如果要设定一些转换的参数，可以使用<x:param>来指明参数名和值empty 空值判断
 <c:if test="${empty type_div}">${type_div}</c:if>
 
**jstl c:choose**
* 空属性判断
* 空值判断
* 0值判断
* 除法结果取整
```jstl
                <!-- 调用数浮动比例 -->
                <c:choose>
                    <c:when test="${not empty appItem.avgTotalCount && appItem.avgTotalCount > 0}">
                        <fmt:parseNumber var="totalCountRatio" integerOnly="true" value="${(appItem.totalCount-appItem.avgTotalCount)  / appItem.avgTotalCount * 100}" />
                    </c:when>
                    <c:otherwise>
                        <fmt:parseNumber var="totalCountRatio" integerOnly="true" value="${0}" />
                    </c:otherwise>
                </c:choose>
                <!-- 5xx状态浮动比例 -->
                <c:choose>
	                <c:when  test="${not empty appItem.avgStatus5xxCount && appItem.status5xxCount > 0 && appItem.avgStatus5xxCount > 0}">
	                     <fmt:parseNumber var="status5xxCountRatio" integerOnly="true" value="${(appItem.status5xxCount-appItem.avgStatus5xxCount) / appItem.avgStatus5xxCount * 100}" />
	                </c:when>
	                <c:otherwise>
	                     <fmt:parseNumber var="status5xxCountRatio" integerOnly="true" value="${0}" />
	                </c:otherwise>
                </c:choose>
                
```
                
**jstl c:if**
* 表达式计算
* 数值格式化

```
    <c:if test="${appItem.sumTranTime / appItem.totalCount  >= 500}">class='td-value red-color'  </c:if>>
     <fmt:formatNumber type="number" value="${appItem.sumTranTime / appItem.totalCount}" pattern="##.##" maxFractionDigits="2"/>
```
