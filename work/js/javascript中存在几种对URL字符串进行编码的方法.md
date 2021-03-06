javascript中存在几种对URL字符串进行编码的方法：escape()，encodeURI()，以及encodeURIComponent()。这几种编码所起的作用各不相同。

escape() 方法：

采用ISO Latin字符集对指定的字符串进行编码。所有的空格符、标点符号、特殊字符以及其他非ASCII字符都将被转化成%xx格式的字符编码（xx等于该字符在字符集表里面的编码的16进制数字）。比如，空格符对应的编码是%20。

不会被此方法编码的字符： @ * / +

encodeURI() 方法：

把URI字符串采用UTF-8编码格式转化成escape格式的字符串。

不会被此方法编码的字符：! @ # $& * ( ) = : / ; ? + ’

encodeURIComponent() 方法：

把URI字符串采用UTF-8编码格式转化成escape格式的字符串。与encodeURI()相比，这个方法将对更多的字符进行编码，比如 / 等字符。所以如果字符串里面包含了URI的几个部分的话，不能用这个方法来进行编码，否则 / 字符被编码之后URL将显示错误。

不会被此方法编码的字符：! * ( ) ’

因此，对于中文字符串来说，如果不希望把字符串编码格式转化成UTF-8格式的（比如原页面和目标页面的charset是一致的时候），只需要使用escape。如果你的页面是GB2312或者其他的编码，而接受参数的页面是UTF-8编码的，就要采用encodeURI或者encodeURIComponent。

另外，encodeURI/encodeURIComponent是在javascript1.5之后引进的，escape则在javascript1.0版本就有。

 verTemplate = encodeURIComponent(verTemplate);