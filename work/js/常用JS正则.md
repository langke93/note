匹配中文字符的正则表达式： [u4e00-u9fa5]

评注：匹配中文还真是个头疼的事，有了这个表达式就好办了

匹配双字节字符(包括汉字在内)：[^x00-xff]

评注：可以用来计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）

匹配空白行的正则表达式：ns*r

评注：可以用来删除空白行

匹配HTML标记的正则表达式：< (S*?)[^>]*>.*?|< .*? />

评注：网上流传的版本太糟糕，上面这个也仅仅能匹配部分，对于复杂的嵌套标记依旧无能为力

匹配首尾空白字符的正则表达式：^s*|s*$

评注：可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式

匹配Email地址的正则表达式：w+([-+.]w+)*@w+([-.]w+)*.w+([-.]w+)*

评注：表单验证时很实用

匹配网址URL的正则表达式：[a-zA-z]+://[^s]*

评注：网上流传的版本功能很有限，上面这个基本可以满足需求

匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$

评注：表单验证时很实用

匹配国内电话号码：d{3}-d{8}|d{4}-d{7}

评注：匹配形式如 0511-4405222 或 021-87888822

匹配腾讯QQ号：[1-9][0-9]{4,}

评注：腾讯QQ号从10000开始

匹配中国邮政编码：[1-9]d{5}(?!d)

评注：中国邮政编码为6位数字

匹配身份证：d{15}|d{18}

评注：中国的身份证为15位或18位

匹配ip地址：d+.d+.d+.d+

评注：提取ip地址时有用

匹配特定数字：

^[1-9]d*$　 　 //匹配正整数

^-[1-9]d*$ 　 //匹配负整数

^-?[1-9]d*$　　 //匹配整数

^[1-9]d*|0$　 //匹配非负整数（正整数 + 0）

^-[1-9]d*|0$　　 //匹配非正整数（负整数 + 0）

^[1-9]d*.d*|0.d*[1-9]d*$　　 //匹配正浮点数

^-([1-9]d*.d*|0.d*[1-9]d*)$　 //匹配负浮点数

^-?([1-9]d*.d*|0.d*[1-9]d*|0?.0+|0)$　 //匹配浮点数

^[1-9]d*.d*|0.d*[1-9]d*|0?.0+|0$　　 //匹配非负浮点数（正浮点数 + 0）

^(-([1-9]d*.d*|0.d*[1-9]d*))|0?.0+|0$　　//匹配非正浮点数（负浮点数 + 0）

评注：处理大量数据时有用，具体应用时注意修正

匹配特定字符串：

^[A-Za-z]+$　　//匹配由26个英文字母组成的字符串

^[A-Z]+$　　//匹配由26个英文字母的大写组成的字符串

^[a-z]+$　　//匹配由26个英文字母的小写组成的字符串

^[A-Za-z0-9]+$　　//匹配由数字和26个英文字母组成的字符串

^w+$　　//匹配由数字、26个英文字母或者下划线组成的字符串

在使用RegularExpressionValidator验证控件时的验证功能及其验证表达式介绍如下:

只能输入数字：“^[0-9]*$”

只能输入n位的数字：“^d $”

只能输入至少n位数字：“^d{n,}$”

只能输入m-n位的数字：“^d{m,n}$”

只能输入零和非零开头的数字：“^(0|[1-9][0-9]*)$”

只能输入有两位小数的正实数：“^[0-9]+(.[0-9]{2})?$”

只能输入有1-3位小数的正实数：“^[0-9]+(.[0-9]{1,3})?$”

只能输入非零的正整数：“^+?[1-9][0-9]*$”

只能输入非零的负整数：“^-[1-9][0-9]*$”

只能输入长度为3的字符：“^.{3}$”

只能输入由26个英文字母组成的字符串：“^[A-Za-z]+$”

只能输入由26个大写英文字母组成的字符串：“^[A-Z]+$”

只能输入由26个小写英文字母组成的字符串：“^[a-z]+$”

只能输入由数字和26个英文字母组成的字符串：“^[A-Za-z0-9]+$”

只能输入由数字、26个英文字母或者下划线组成的字符串：“^w+$”

验证用户密码:“^[a-zA-Z]w{5,17}$”正确格式为：以字母开头，长度在6-18之间，

只能包含字符、数字和下划线。

验证是否含有^%&’,;=?$”等字符：“[^%&',;=?$x22]+”

只能输入汉字：“^[u4e00-u9fa5],{0,}$”

验证Email地址：“^w+[-+.]w+)*@w+([-.]w+)*.w+([-.]w+)*$”

验证InternetURL：“^http://([w-]+.)+[w-]+(/[w-./?%&=]*)?$”

验证电话号码：“^((d{3,4})|d{3,4}-)?d{7,8}$”

正确格式为：“XXXX-XXXXXXX”，“XXXX-XXXXXXXX”，“XXX-XXXXXXX”，

“XXX-XXXXXXXX”，“XXXXXXX”，“XXXXXXXX”。

验证身份证号（15位或18位数字）：“^d{15}|d{}18$”

验证一年的12个月：“^(0?[1-9]|1[0-2])$”正确格式为：“01”-“09”和“1”“12”

验证一个月的31天：“^((0?[1-9])|((1|2)[0-9])|30|31)$”

正确格式为：“01”“09”和“1”“31”。

匹配中文字符的正则表达式： [u4e00-u9fa5]

匹配双字节字符(包括汉字在内)：[^x00-xff]

匹配空行的正则表达式：n[s| ]*r

匹配HTML标记的正则表达式：/< (.*)>.*|< (.*) />/

匹配首尾空格的正则表达式：(^s*)|(s*$)

匹配Email地址的正则表达式：w+([-+.]w+)*@w+([-.]w+)*.w+([-.]w+)*

匹配网址URL的正则表达式：http://([w-]+.)+[w-]+(/[w- ./?%&=]*)?

(1)应用：计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）

String.prototype.len=function(){return this.replace([^x00-xff]/g,”aa”).length;}

(2)应用：javascript中没有像vbscript那样的trim函数，我们就可以利用这个表达式来实现

String.prototype.trim = function()

{

return this.replace(/(^s*)|(s*$)/g, “”);

}

(3)应用：利用正则表达式分解和转换IP地址

function IP2V(ip) //IP地址转换成对应数值

{

re=/(d+).(d+).(d+).(d+)/g //匹配IP地址的正则表达式

if(re.test(ip))

{

return RegExp.$1*Math.pow(255,3))+RegExp.$2*Math.pow(255,2))+RegExp.$3*255+RegExp.$4*1

}

else

{

throw new Error(”Not a valid IP address!”)

}

}

(4)应用：从URL地址中提取文件名的javascript程序

s=”http://www.9499.net/page1.htm”;

s=s.replace(/(.*/){0,}([^.]+).*/ig,”$2″) ; //Page1.htm

(5)应用：利用正则表达式限制网页表单里的文本框输入内容

用正则表达式限制只能输入中文：onkeyup=”value=”/blog/value.replace(/["^u4E00-u9FA5]/g,”) ” onbeforepaste=”clipboardData.setData(’text’,clipboardData.getData(’text’).replace(/[^u4E00-u9FA5]/g,”))”

用正则表达式限制只能输入全角字符： onkeyup=”value=”/blog/value.replace(/["^uFF00-uFFFF]/g,”) ” onbeforepaste=”clipboardData.setData(’text’,clipboardData.getData(’text’).replace(/[^uFF00-uFFFF]/g,”))”

用正则表达式限制只能输入数字：onkeyup=”value=”/blog/value.replace(/["^d]/g,”) “onbeforepaste= “clipboardData.setData(’text’,clipboardData.getData(’text’).replace(/[^d]/g,”))”

用正则表达式限制只能输入数字和英文：onkeyup=”value=”/blog/value.replace(/[W]/g,””) “onbeforepaste=”clipboardData.setData(’text’,clipboardData.getData(’text’).replace(/[^d]/g,”

以下函数调用方式：

    function check()

    {

        var bb = document.getElementById("txt_id").value;//txt_id为文本框的ID

        alert(ismobile(bb));//ismobile 代表以下任何一个函数名称

    }

HTML代码：

    <input type="text" name="textfield" id="txt_id" />

    <input type="submit" name="Submit" value="提交" />

**************************/

// 判断输入是否是一个由 0-9 / A-Z / a-z 组成的字符串

function isalphanumber(str)

{

    var result=str.match(/^[a-zA-Z0-9]+$/);

    if(result==null) return false;

    return true;

} 

// 判断输入是否是一个数字--(数字包含小数)--

function isnumber(str)

{

    return !isNaN(str);

}

// 判断输入是否是一个整数

function isint(str)

{

    var result=str.match(/^(-|\+)?\d+$/);

    if(result==null) return false;

    return true;

}

// 判断输入是否是有效的长日期格式 - "YYYY-MM-DD HHSS" || "YYYY/MM/DD HHSS"

function isdatetime(str)

{

    var result=str.match(/^(\d{4})(-|\/)(\d{1,2})\2(\d{1,2}) (\d{1,2})\d{1,2})\d{1,2})$/);

    if(result==null) return false;

    var d= new Date(result[1], result[3]-1, result[4], result[5], result[6], result[7]);

    return (d.getFullYear()==result[1]&&(d.getMonth()+1)==result[3]&&d.getDate()==result[4]&&d.getHours()==result[5]&&d.getMinutes()==result[6]&&d.getSeconds()==result[7]);

}

// 检查是否为 YYYY-MM-DD || YYYY/MM/DD 的日期格式

function isdate(str){

var result=str.match(/^(\d{4})(-|\/)(\d{1,2})\2(\d{1,2})$/);

if(result==null) return false;

var d=new Date(result[1], result[3]-1, result[4]);

return (d.getFullYear()==result[1] && d.getMonth()+1==result[3] && d.getDate()==result[4]);

}

// 判断输入是否是有效的电子邮件

function isemail(str)

{

    var result=str.match(/^\w+((-\w+)|(\.\w+))*\@[A-Za-z0-9]+((\.|-)[A-Za-z0-9]+)*\.[A-Za-z0-9]+$/);

    if(result==null) return false;

    return true;

}

// 去除字符串的首尾的空格

function trim(str){

return str.replace(/(^\s*)|(\s*$)/g, "");

}

// 返回字符串的实际长度, 一个汉字算2个长度

function strlen(str){

return str.replace(/[^\x00-\xff]/g, "**").length;

}

//匹配中国邮政编码(6位)

function ispostcode(str)

{

    var result=str.match(/[1-9]\d{5}(?!\d)/);

    if(result==null) return false;

    return true;

}

//匹配国内电话号码(0511-4405222 或 021-87888822)

function istell(str)

{

    var result=str.match(/\d{3}-\d{8}|\d{4}-\d{7}/);

    if(result==null) return false;

    return true;

}

//校验是否为(0-10000)的整数

function isint1(str)

{

    var result=str.match(/^[0-9]$|^([1-9])([0-9]){0,3}$|^10000$/);

    if(result==null) return false;

    return true;

}

//匹配腾讯QQ号

function isqq(str)

{

    var result=str.match(/[1-9][0-9]{4,}/);

    if(result==null) return false;

    return true;

}

//匹配身份证(15位或18位)

function isidcard(str)

{

    var result=str.match(/\d{15}|\d{18}/);

    if(result==null) return false;

    return true;

}

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

//校验文本是否为空

function checknull(field,sval)

{

    if (field.value =="")

      {

        alert("请填写" + sval + "！");

        field.focus();

        return false;

      }

      return true;

}

//屏蔽输入字符

/***********************

调用方法：    

    在文本框中加上 

*************************/

function checkChar()

{ 

    var keycode = event.keyCode;

    if(!(keycode>=48&&keycode<=57))

    {

        return false;

    }

}

/***************************************************************************************************************************

中国电话号码验证 

匹配形式如:0511-4405222 或者021-87888822 或者 021-44055520-555 或者 (0511)4405222 

正则表达式 "((d{3,4})|d{3,4}-)?d{7,8}(-d{3})*"

中国邮政编码验证 

匹配形式如:215421 

正则表达式 "d{6}"

电子邮件验证 

匹配形式如:justali@justdn.com 

正则表达式 "w+([-+.]w+)*@w+([-.]w+)*.w+([-.]w+)*"

身份证验证 

匹配形式如:15位或者18位身份证 

正则表达式 "d{18}|d{15}"

常用数字验证 

正则表达式 

"d " n为规定长度 

"d{n,m}" n到m的长度范围

非法字符验证 

匹配非法字符如:< > & / ' | 

正则表达式 [^<>&/|'\]+

日期验证 

匹配形式如:20030718,030718 

范围:1900--2099 

正则表达式((((19){1}|(20){1})d{2})|d{2})[01]{1}d{1}[0-3]{1}d{1}

匹配中文字符的正则表达式： [\u4e00-\u9fa5]

评注：匹配中文还真是个头疼的事，有了这个表达式就好办了

匹配双字节字符(包括汉字在内)：[^\x00-\xff]

评注：可以用来计算字符串的长度（一个双字节字符长度计2，ASCII字符计1）

匹配空白行的正则表达式：\n\s*\r

评注：可以用来删除空白行

匹配HTML标记的正则表达式：< (\S*?)[^>]*>.*?|< .*? />

评注：网上流传的版本太糟糕，上面这个也仅仅能匹配部分，对于复杂的嵌套标记依旧无能为力

匹配首尾空白字符的正则表达式：^\s*|\s*$

评注：可以用来删除行首行尾的空白字符(包括空格、制表符、换页符等等)，非常有用的表达式

匹配Email地址的正则表达式：\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*

评注：表单验证时很实用

匹配网址URL的正则表达式：[a-zA-z]+://[^\s]*

评注：网上流传的版本功能很有限，上面这个基本可以满足需求

匹配帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：^[a-zA-Z][a-zA-Z0-9_]{4,15}$

评注：表单验证时很实用

匹配国内电话号码：\d{3}-\d{8}|\d{4}-\d{7}

评注：匹配形式如 0511-4405222 或 021-87888822

匹配腾讯QQ号：[1-9][0-9]{4,}

评注：腾讯QQ号从10000开始

匹配中国邮政编码：[1-9]\d{5}(?!\d)

评注：中国邮政编码为6位数字

匹配身份证：\d{15}|\d{18}

评注：中国的身份证为15位或18位

匹配ip地址：\d+\.\d+\.\d+\.\d+

评注：提取ip地址时有用

提取信息中的ip地址: 

(\d+)\.(\d+)\.(\d+)\.(\d+) 

提取信息中的中国手机号码:

(86)*0*13\d{9} 

提取信息中的中国固定电话号码:

(\(\d{3,4}\)|\d{3,4}-|\s)?\d{8} 

提取信息中的中国电话号码（包括移动和固定电话）:

(\(\d{3,4}\)|\d{3,4}-|\s)?\d{7,14} 

提取信息中的中国邮政编码:

[1-9]{1}(\d+){5} 

提取信息中的中国身份证号码:

\d{18}|\d{15} 

提取信息中的整数：

\d+ 

提取信息中的浮点数（即小数）：

(-?\d*)\.?\d+ 

提取信息中的任何数字 ：

(-?\d*)(\.\d+)?

提取信息中的中文字符串：

[\u4e00-\u9fa5]* 

提取信息中的双字节字符串 (汉字)：

[^\x00-\xff]*

提取信息中的英文字符串：

\w*

提取信息中的网络链接:

(h|H)(r|R)(e|E)(f|F) *= *('|")?(\w|\\|\/|\.)+('|"| *|>)? 

提取信息中的邮件地址:

\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*

提取信息中的图片链接:

(s|S)(r|R)(c|C) *= *('|")?(\w|\\|\/|\.)+('|"| *|>)?

匹配特定数字：

^[1-9]\d*$　 　 //匹配正整数

^-[1-9]\d*$ 　 //匹配负整数

^-?[1-9]\d*$　　 //匹配整数

^[1-9]\d*|0$　 //匹配非负整数（正整数 + 0）

^-[1-9]\d*|0$　　 //匹配非正整数（负整数 + 0）

^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$　　 //匹配正浮点数

^-([1-9]\d*\.\d*|0\.\d*[1-9]\d*)$　 //匹配负浮点数

^-?([1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0)$　 //匹配浮点数

^[1-9]\d*\.\d*|0\.\d*[1-9]\d*|0?\.0+|0$　　 //匹配非负浮点数（正浮点数 + 0）

^(-([1-9]\d*\.\d*|0\.\d*[1-9]\d*))|0?\.0+|0$　　//匹配非正浮点数（负浮点数 + 0）

评注：处理大量数据时有用，具体应用时注意修正

匹配特定字符串：

^[A-Za-z]+$　　//匹配由26个英文字母组成的字符串

^[A-Z]+$　　//匹配由26个英文字母的大写组成的字符串

^[a-z]+$　　//匹配由26个英文字母的小写组成的字符串

^[A-Za-z0-9]+$　　//匹配由数字和26个英文字母组成的字符串

^\w+$　　//匹配由数字、26个英文字母或者下划线组成的字符串

评注：最基本也是最常用的一些表达式

////////////////////前4行程序用于保护js代码不被下载

// ////////////////////基本正则表达式/////////////////// 

//非空验证 function NotNull (str) { return (str!=""); } 

//邮件地址验证 

function checkEmail (str) {

    //邮件地址正则表达式 isEmail1=/^\w+([\.\-]\w+)*\@\w+([\.\-]\w+)*\.\w+$/; 

    //邮件地址正则表达式 [email=isEmail2=/%5E.*@[%5E_]*$/]isEmail2=/^.*@[^_]*$/[/email]; 

    //验证邮件地址，返回结果 return (isEmail1.test(str)&&isEmail2.test(str)); 

    } //身份证验证 function checkIDCard (str) { 

        //身份证正则表达式(15位) 

        isIDCard1=/^[1-9]\d{7}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{3}$/; 

        //身份证正则表达式(18位) isIDCard2=/^[1-9]\d{5}[1-9]\d{3}((0\d)|(1[0-2]))(([0|1|2]\d)|3[0-1])\d{4}$/; 

        //验证身份证，返回结果 return (isIDCard1.test(str)||isIDCard2.test(str)); } 

        //IP验证 function checkIP (str) 

        { //IP正则表达式 IP='(25[0-5]|2[0-4]\\d|1\\d\\d|\\d\\d|\\d)'; 

        IPdot=IP+'\\.'; isIPaddress=new RegExp('^'+IPdot+IPdot+IPdot+IP+'$'); 

        //验证IP，返回结果 return (isIPaddress.test(str)); } 

        //主页（网址）验证 function checkHomepage (str) { 

            //主页正则表达式 //isHomepage=/^\w+([\.\-]\w)*$/; isHomepage=/^\w+(\.\w+)+\.\w+$/; 

            //验证主页，返回结果 return (isHomepage.test(str)); } 

            //是否数字 function isNum (str) { //isNumber=/^([1-9]\d*(\.\d+)?)|(\d+(\.\d+))$/; isNumber=/^\d+(\.\d+)?$/; 

            //验证并返回结果 return (isNumber.test(str)); } 

            //是否整数 function isInt (str) { isInteger=/^\d+$/; 

            //验证并返回结果 return (isInteger.test(str)); } 

            //是否字母 function isChar (str) { isCharacter=/^[A-Za-z]+$/; 

            //验证并返回结果 return (isCharacter.test(str)); } 

            /////////////////////基本弹出窗口/////////////////// 

            function checkBoolean(bv,i,w) { if(bv==false) { try{i.focus();}catch(e){} alert(w); return false; } return true } 

            ////////////////////元素和取值判断//////////////////// // 

            已选择 function checkElement_selected(item,alert_str) { if(item.type=="select-one")return checkElement_NotNull(item,alert_str); if(alert_str.length==0)alert_str=item.title+"为必选项！"; rt=false; if(item.length>0) { for(i=0;i<item.length;i++){rt=rt||item.checked;} } else { rt=item.checked } return checkBoolean(rt,item[0],alert_str); return true; } //

            不为空 function checkElement_NotNull(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_NotNull(v,a,w,g)); } function checkValue_NotNull(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=NotNull(v); return(checkBoolean(bv,i,w)); } 

            // 合法邮箱 function checkElement_IsEmail(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsEmail(v,a,w,g)); } 

            function checkValue_IsEmail(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=checkEmail(v); return(checkBoolean(bv,i,w)); } // 合法身份证 function checkElement_IsIDCard(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsIDCard(v,a,w,g)); }

function checkValue_IsIDCard(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=checkIDCard(v); return(checkBoolean(bv,i,w)); } // 合法IP function checkElement_IsIP(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsIP(v,a,w,g)); } function checkValue_IsIP(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=checkIP(v); return(checkBoolean(bv,i,w)); } 

// 验证数字 function checkElement_IsNum(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsNum(v,a,w,g)); } function checkValue_IsNum(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=isNum(v); return(checkBoolean(bv,i,w)); } 

// 验证整数 function checkElement_IsInt(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsInt(v,a,w,g)); } function checkValue_IsInt(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=isInt(v); return(checkBoolean(bv,i,w)); } // 验证字母 function checkElement_IsChar(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsChar(v,a,w,g)); } function checkValue_IsChar(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=isChar(v); return(checkBoolean(bv,i,w)); } 

// 合法主页 function checkElement_IsHomepage(a,alert_str,g) { v=a.value; w=alert_str; if(alert_str.length==0)w=a.title+"不能为空！"; return(checkValue_IsHomepage(v,a,w,g)); } function checkValue_IsHomepage(v,i,w,g) { if(g!="NOT_TRIM")v=v.replace(/(^\s*)|(\s*$)/g, ""); bv=checkHomepage(v); return(checkBoolean(bv,i,w)); }

! 去除字符串两端空格的处理

如果采用传统的方式,就要可能就要采用下面的方式了 

//清除左边空格 

function js_ltrim(deststr) 

{ 

if(deststr==null)return ""; 

var pos=0; 

var retStr=new String(deststr); 

if (retStr.lenght==0) return retStr; 

while (retStr.substring(pos,pos+1)==" ") pos++; 

retStr=retStr.substring(pos); 

return(retStr); 

} 

//清除右边空格 

function js_rtrim(deststr) 

{ 

if(deststr==null)return ""; 

var retStr=new String(deststr); 

var pos=retStr.length; 

if (pos==0) return retStr; 

while (pos && retStr.substring(pos-1,pos)==" " ) pos--; 

retStr=retStr.substring(0,pos); 

return(retStr); 

} 

//清除左边和右边空格 

function js_trim(deststr) 

{ 

if(deststr==null)return ""; 

var retStr=new String(deststr); 

var pos=retStr.length; 

if (pos==0) return retStr; 

retStr=js_ltrim(retStr); 

retStr=js_rtrim(retStr); 

return retStr; 

}

采用正则表达式,来去除两边的空格,只需以下代码 

String.prototype.trim = function() 

{ 

return this.replace(/(^\s*)|(\s*$)/g, ""); 

}

一句就搞定了, 

可见正则表达式为我们节省了相当的编写代码量