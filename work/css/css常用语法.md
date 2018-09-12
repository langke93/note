**css常用语法**
.绝对定位居中
我们经常用margin:0 auto来实现水平居中，而一直认为margin:auto不能实现垂直居中……实际上，实现垂直居中仅需要声明元素高度和下面的CSS:
```css
.Absolute-Center {  
  margin: auto;  
  position: absolute;  
  top: 0; left: 0; bottom: 0; right: 0;  
} 
```


2.等待效果
```css
<style type="text/css">
    #pageloading{position:absolute; margin: auto;top: 0; left: 0; bottom: 0; right: 0; background:transparent url('../html/images/loading.gif') no-repeat center;z-index:99999;}
</style>
```
```javascript
<script>
  $.ajax({
            url: "report/groupByType",
            data: $("form").serialize(),
            type: "POST",
            cache: false,
            dataType: "json",
            beforeSend:function(){
                $("#pageloading").show();
            },
            complete:function(){
                $("#pageloading").hide();
            },success: function(result) {
            ......
            }
    });
</script>
```
```html
<div id="pageloading"></div> 
```


3.自动换行
word-break:break-all;

4.文字自动截取：
width:100px; overflow:hidden; white-space:nowrap; text-overflow:ellipsis

5.DIV边框颜色:border: 1px solid #D5D5D5;

6.层居中：
<div align="center" style=" width:940px"></div>

7.图片大小控制：
```css
.day1 img{
 margin:15px;
 float: left;
 width: expression(this.width >650 ? '650px': true);
 max-width: 650px;
}
```


8.div对齐问题:
```css
 style="margin-left: 10px;margin-top: 10px;float: left;display: inline"
```

9.自动调整表格换行
```css
<style> 
<!-- 
.topic-column {
	BACKGROUND: #5E8C5E; 
	COLOR: #FFFFFF; 
	word-break:keep-all; 
	word-wrap:normal
} 
.read-num {
	COLOR: #1A441A; 
	BACKGROUND: #F0F7F0; 
	word-break:keep-all; 
	word-wrap:normal 
} 
--> 
</style> 

```

层居中
```css
LEFT: expression((document.body.clientWidth-118)/2);
```


