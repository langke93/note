**jsonp跨域访问通过yahoo api代理**
```javascript
<script>
var url1 = "http://www.weather.com.cn/adat/cityinfo/101230601.html"
$(function(){   
    $.getJSON("http://query.yahooapis.com/v1/public/yql", {   
    q: "select * from json where url='"+url1+"'",   
    format: "json"   
}, function(data) {   
    var $content = $("#content")   
    if (data.query.results) {  
        var result = JSON.stringify(data.query.results);
        $content.text(result);  
        var obj = eval('('+result+')');
        //alert(obj.weatherinfo.city);
        var html = '';
html +='<a href="http://www.weather.com.cn/weather1d/101230601.shtml" target=_balnk>';
html+='<p class="t1"><img src="weatherPic/'+obj.weatherinfo.img1+'">/<img src="weatherPic/'+obj.weatherinfo.img2+'"></p>';
html+='<p class="t2">'+obj.weatherinfo.temp1+'/'+obj.weatherinfo.temp2+'</p>';
html+='<p class="t3">'+obj.weatherinfo.weather+'</p>';
html+='<div class="txt_2">'+obj.weatherinfo.city+'</div>';
html+='</a>';
        $("#weather").html(html)
    } else {   
        $content.text('no such code: ' + code);   
    }   
});   
         
});
</script>
```
