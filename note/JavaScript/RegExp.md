## **引言**

实际工作中，验证手机号、邮箱、身份证号，对复杂文本，处理地图地址，去重等等需求，都需要使用到火星文正则表达式，但熟练运用正则并不是那么容易。这里将不定期更新在实际工作中运用到的正则，并且会整理出有关正则的知识点

<div><!--more--></div>

## 正则表达式的匹配规则

### 修饰符

```javascript

g 		 全局匹配
	用法:
		var reg = /is/g;
		var reg = new RegExp("is", "g");

i 		忽略大小写
	用法:
		var reg = /is/gi;
		var reg = new RegExp("is", "gi");

```

### 开头和结尾

```javascript

^ 		匹配字符串的开头
	用法:
		var reg = /^[a-z]/;   //匹配以小写字母开头
		^要写在正则的最前面

$ 		匹配字符串的结尾
	用法:
		var reg = /[a-z]$/;   //匹配以小写字母结尾
		$要写在正则的最末尾

```

### 字符类

```javascript

\w 		匹配单词字符，包括字母数字下划线
\W 		非单词字符，与\w相反
\d 		匹配数字，0-9的数字
\D 		非数字
\s 		匹配空白字符，包含空格、制表符、回车符、换行符等
\S 		非空白符
\t 		制表符
\r 		回车符
\n 		换行符

```

### 匹配次数

```javascript
? 		匹配0次或1次，可以没有也可以有一次
* 		匹配0次或多次
+ 		至少一次或多次
{n} 		匹配n次
{2,5}		匹配2-5次
{2,} 		匹配2次或2次以上

```

### []、()组的使用

```javascript

[] 			在[]内可以任选一个进行匹配
[a-z]  		匹配a-z的小写字母
[A-Z] 		匹配A-Z的大写字母
[a-zA-Z] 	匹配所有的字母（小写字母或大写字母）
[0-9] 		匹配所有的数字
[a-zA-Z0-9] 	匹配所有的字母和数字
[abc] 		匹配a或b或c
[^abc]   	^在[]里面，代表非的意思，不能是abc
[^a-z] 		不能是小写字母

| 			或者
() 			作用一:用于分组，通常与|一起使用
			用法:
			var reg = /[a-z]+(.com|.cn)$/;   匹配以.com或.cn结尾的字符串

			作用二:
			()里面的字符，具有被记忆的功能，一般用于replace替换字符
			通过$1去引用记忆中的字符，
			正则中可以有多个()，引用从1开始:$1 $2 $3...

```

### 任意字符

```javascript
	. 			匹配除终止符以外的任意字符

```


### 转义

```javascript

转义字符
\ 			如果要匹配有特殊功能的字符，则需要用\进行转义
			转义之后，该字符就变成了普通字符
			比如:.+*?^$[]{}()|\等等

匹配汉字
[\u4E00-\u9FFF]
```

## 配合正则表达式的函数

要发挥正则表达式的功效，必须配合一些函数一起使用。下面将列出几种常用的函数

> js正则表达式之test函数

```功能介绍:``` 该方法用户检测字符串内容是否有存在于正则表达式相匹配的结果，如果匹配成功返回true，否则返回false

```基本语法:``` regExp.test(objStr);

```参数:``` regExp正则表达式规则,objStr需要检验的文本

<pre>

	let email = document.getElementsByClassName('email');
	let text = email[0];
	let button = email[1];
	button.onclick = function(){
		let reg = /\w{3,12}@(qq|gmail|163)\.(com|cn)/;
		let pass = reg.test(text.value);
		if(pass)
			alert('是正确的email地址')
		else
			alert('请输入正确email')
	}
</pre>

> js正则表达式之exec方法详解

```功能说明:``` 该函数对指定的字符串进行一次匹配，获取字符串中的第一个与正则表达式的内容，并且将匹配的内容和子匹配的结果存放在返回数组中

```基本用法:``` regExp.exec(string);

<pre>
	var objStr="我的手机号13522222222，他的手机号13288888888，她的手机号码13699999999"; 
	//设置正则表达式，匹配以13开头11位字符串，全局匹配 
	var reg=/13(\d)(\d{8})/g; 
	//执行exec函数，尽管是全局匹配的正则表达式，但是exec方法只对指定的字符串进行一次匹配，获取字符串中第一个与正则表达式相匹配的内容，并且将匹配内容和子匹配的结果存储到返回的数组中 
	var arr=reg.exec(objStr); 
	//循环输出结果 
	for(var i=0;i<arr.length;i++){ 
		document.write("<li>"+arr[i]+"<br>"); 
	}
</pre>



> js正则表达式之replace函数

```函数功能:``` replace函数根据正则表达式将指定的字符文本替换成指定的字符后复制

```函数格式:``` stringObj.replace(regExp,replaceText)

```参数:``` 字符串stringObj,regExp正则表达式,replaceText需要替换内容的字符串


简单案例:
<pre>
	let str = 'no one no one    no one no one one '
	let reg = /o\w?/g;
	let reg1 = /o\w?/;
	document.write('去除o获取o后面加一个字符',str.replace(reg,'xx'));
	document.write('去除第一个o获取o后面跟着数字字母下划线的字符',str.replace(reg1,'xx'));

</pre>

> js正则表达式之match函数

```功能介绍:``` 使用正则表达式对字符串进行查找，并将包含查找的结果作为数组返回 

```返回值:``` 如果能匹配则返回结果数组，否则返回null

```函数格式:``` stringObj.match(regExp) stringObj要进行查找匹配的字符串,regExp要进行匹配的格式


<pre>
let str = 'Love is like a butterfly. It goes where it pleases and it pleases where it goes.'
let regExp = /\wo(\w+)?/g;
let arr = str.match(regExp);
console.log(arr);
</pre>


> js正则表达式之search方法讲解

```功能:``` 返回正则表达式查找内容匹配的第一个字符串的位置

```语法:``` stringObj.search(regExp)

```返回值:``` search方法指明是否存在相应的匹配。如果找到一个匹配，search方法将返回一个索引位置，表明匹配的字符的位置

<pre>
	var re = /apples/gi;
	var str = "Apples are round, and apples are juicy.";
	 console.log(str.search(re));
	if ( str.search(re) == -1 ){
	  document.write("Does not contain Apples" );
	}else{
	  document.write("Contains Apples" );
	}
</pre>





