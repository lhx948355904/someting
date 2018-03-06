###Welcome to use MarkDown
ES6 全称ECMA Script2015
关于ES6的10个特性(后续补充)
\1/函数参数默认值
\2/模版字符串
\3/多行字符串
\4/解构赋值
\5/对象属性简写
\6/箭头函数
\7/Promise
\8/Let Const
\9/类
\10/模块化


\1/
		函数参数默认值
		
不使用ES6
function foo(height,color){
	var height=height||100;
	var color=color||"red";
	...
}
但是当调用的参数的布尔类型为false时候，则会使用默认参数。foo(0,"");

使用ES6
function foo(height=100,color="red"){
	...
}
不会受参数的布尔类型影响


\2/
		模版字符串
		
不使用ES6
使用加号拼接字符串 如果中间需要空格还需要添加空格字符串
var first="大宝",last="二宝"
var name="Hellow! My name is "+first+" "+last;
console.log(name);

使用ES6
更加方便 使用``反向单引号 把变量放在${}内
var name1=`Hellow! My name is ${first} ${last}`
console.log(name1)


\3/
		多行字符串
		
不使用ES6
var str="a\n\t"+											隐形换行，即在代码里换行，在html变现层并不换行 \n为换行\t为制表符 为空格
"b\n\t"+"c\n\t";											
如果需要在html换行 需要用 document.write("<br/>")
var str="a\n<br/>bbbbb\nccc"							
document.write(str);												//在html中表现为 <br>处换行 \n处为空格 换行解析为空格
console.log(str);														//在代码中表现为\n出换行 <br>依然存在  \n读取
alert(str);																	//弹框会显示<br/>算代码表现

使用ES6
var str1=`aaaa<br><div>123123</div>
换行<br>
测试`;
document.write(str1);											//在html中表现为读取代码<br><div>123123</div>会读取
console.log(str1);													//在代码中变现和``内格式相同 不需要手动添加\n等
alert(str1);


\4/
		解构赋值


\5/
		对象属性简写
		
不使用ES6
var bar = 'bar';
var foo = function (){
	console.log(222)
}
var baz = {
 abc: bar,										//对象的属性名与属性值名可以不同
 cba: foo
};
console.log(baz)
baz.cba();

使用ES6
var bar1 = 'bar';
var foo1 = function (){
	console.log(333)
}
var baz = { bar1, foo1 };					//更加简介，但是需要对象的属性名和属性值名相同
console.log(baz)
baz.foo1();


\6/
		箭头函数
	1.格式为 ()=>code
		1>如果没有参数 则依旧需要加括号 格式为()=>console.log(111);
		2>如果有一个参数 则不需要加括号 格式为x=>alert(x);
		3>如果有多个参数 则需要用括号括起来 格式为(a,b,c)=>console.log(a+"|"+b+"|"+c);
	2.如果想使用标准的函数体或者函数内有更多语句要执行则要用大括号把内容括起来 并指定返回值
		格式 var sum=(a,b)=>{return a+b};
	3.如果想返回对象
		常规：
			var www=function(a,b){
				return {
					a:a,
					b:b
				}
			}
			button[0].onclick=function(){
				console.log(www("fighting","forhome"))
			}
		ES6:需要在外层用小括号包起来，并且不需要用return
			var xxx=(xx,yy)=>({xx:xx,yy:yy});
			button[0].onclick=function(){
				console.log(www("fighting","liuhongxiang"))
			}
		4.
		
\8/
		let和const

//let
var lii=document.querySelectorAll("li");
for(let x=0;x<lii.length;x++){
	lii[x].onclick=function(){
		console.log(x)
	}
}
console.log(x)			//x is not defined	[let块级性]

//var
var lii=document.querySelectorAll("li");
for(lvar x=0;x<lii.length;x++){
	lii[x].onclick=function(){
		console.log(x)
	}
}
console.log(x)			//3 [var全局性]

//闭包解决
for(var v=0;v<lii.length;v++){
	lii[v].onclick=abc(v);
}
function abc(zz){
	var xx=function(){
		console.log(zz)
	}
	console.log(zz);
	return xx;
}

	1.循环中var命名是全局性的
	2.但是ES6中let命名的是块级性的，命名不会重复，var是全局性的会每次覆盖。
	3.如果在循环内设置延迟或者点击事件，下标为最后一次下标。
	4.解决方法let命名或者闭包
	5.闭包解决原理：如果直接循环 var为全局变量最后一次的变量会覆盖以前的变量 则为最大值
								 闭包会每次给不同的元素绑定不同的事件，事件的变量就是下标，每次的点击事件函数都不同
								 for为变量会覆盖，闭包为每次会赋予不同的点击事件
	6.const为定义常量，常量为恒定不变的量。所以用const命名的变量不可以改变值，改值的话会报错，以及也不能覆盖别的变量。
