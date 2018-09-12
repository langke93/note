**jQuery 效果**  

| 函数  | 描述  |  
| ---  | ---  |  
| $(selector).hide()  | 隐藏被选元素  |  
| $(selector).show()  | 显示被选元素  |  
| $(selector).toggle() | 切换（在隐藏与显示之间）被选元素  |  
| $(selector).slideDown() | 向下滑动（显示）被选元素  |  
| $(selector).slideUp() | 向上滑动（隐藏）被选元素  |  
| $(selector).slideToggle() | 对被选元素切换向上滑动和向下滑动  |  
| $(selector).fadeIn()  | 淡入被选元素  |  
| $(selector).fadeOut() | 淡出被选元素  |  
| $(selector).fadeTo()  | 把被选元素淡出为给定的不透明度  |  
| $(selector).animate() | 对被选元素执行自定义动画  |  
| var temp= $("#test").is(":hidden"); | //是否隐藏 |  
| $("#isscore").attr("checked");  | //check框是否选中  |  
| $("#issort").attr("checked",true);  | 设置选中  |  
| $("input[name='sp'][type='radio']:checked").val();  |  //取选中radio  |  

**替换**
```javascript
var reg = new RegExp(",","g");
sortFileds = sortFileds.replace(reg,"\":"+orderby+"\",");
```
**取多选下拉值（jquery select multiple）**
```
$("#sortFields option:selected").each(function(){
jsoncode += "{\""+$(this).val()+"\":\""+orderby+"\"},\n"; 
});
```

[http://apps.hi.baidu.com/share/detail/6152780](http://apps.hi.baidu.com/share/detail/6152780)
[jQuery中attr和prop方法的区别](http://gxxsite.com/content/view/id/135.html)
**checkbox操作**
```javascript
//判断checkbox是否被选中
if($(this).is(":checked")){
    alert('选中');
}
else{
    alert('未选中');
}
//用jquery全选所有class为listbox的checkbox
$(".listbox").prop("checked", true);
//用jquery取消所有class为listbox的checkbox的选中
$(".listbox").prop("checked", false);
```

**修改form的action**
```
$('#Form1').attr('action', '/Admin/NewsCategory/Edit/' + id);
```
**jquery修改文本域：**
```javascript
$("#jsoncode").text("jsoncode");
alert($("#jsoncode").val());
提交数据L:
$.ajax( {
url : url,
type : query_method,
dataType : 'json',
data : 'method='+query_method+'&content='+jsoncode,
success : function(data,textStatus){
dataToHtml(data);
    },
    error : function(XMLHttpRequest, textStatus ){
alert(textStatus+","+XMLHttpRequest.responseText);
    }
});
```

**list排序**

valueList为 包含一个对象的List
```javascript
 valueList.sort(  
                function(a, b) {  
                    if(a.排序字段< b.排序字段) return -1;  
                    if(a.排序字段 > b.排序字段) return 1;  
                    return 0;  
                }  
            );
```

执行完毕后 自动排序完成

**jquery 对象的 $().each() 方法**
此方法可用于例遍任何对象   
回调函数拥有两个参数：
第一个为对象的成员或数组的索引  
例遍数组，同时使用元素索引和内容   

```javascript
$.each( [0,1,2], function(index, content){
  alert( "item #" + index + " its value is: " + content );
}); 

```
