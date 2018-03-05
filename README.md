

—————————————————————————SVG (可伸缩矢量图形)————————————————————————————

<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="xxx" height="xxx">
/*补充 
	xmlns属性会定义一个或者多个可供选择的命名空间，属性可以放置在文档内任何元素的开始标签内，类似于URL，适用于当前元素内的所有内容
	例如，如果需要使用符合 XML 规范的 XHTML 文档，则应该在文档中的<html> 标签中至少使用一个 xmlns 属性，以指定整个文档所使用的主要命名空间：
	<html xmlns="http://www.w3.org/1999/xhtml">
	如果不希望在每次div 元素中定义 xmlns 属性，那么更好的办法是在文档的开头处定义具有前缀的命名空间：
	<html xmlns="http://www.w3.org/1999/xhtml">
	xmlns:math="http://www.w3.org/1999/Math/MathMl">
	然后，就可以在 div 中使用该前缀了，就像这样：
	<math:div>x3/X<div>
*/
<?xml version="1.0" standalone="no"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" 
"http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">

第一行包含了 XML 声明。请注意 standalone 属性！该属性规定此 SVG 文件是否是"独立的"，或含有对外部文件的引用。
standalone="no" 意味着 SVG 文档会引用一个外部文件 - 在这里，是 DTD 文件。
第二和第三行引用了这个外部的 SVG DTD。该 DTD 位于 "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"。
该 DTD 位于 W3C，含有所有允许的 SVG 元素。

============================================优势=============================================

	SVG 可被非常多的工具读取和修改（比如记事本）
	SVG 与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
	SVG 是可伸缩的
	SVG 图像可在任何的分辨率下被高质量地打印
	SVG 可在图像质量不下降的情况下被放大
	SVG 图像中的文本是可选的，同时也是可搜索的（很适合制作地图）
	SVG 可以与 Java 技术一起运行
	SVG 是开放的标准
	SVG 文件是纯粹的 XML

=========================================读取svg的方式==========================================

svg→文件←可以通过 embed object iframe标签嵌入到代码里

	embed
	优势：所有主要浏览器都支持，并允许使用脚本
	缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）
	<embed src="circle1.svg" type="image/svg+xml" />

	object
	优势：所有主要浏览器都支持，并支持HTML4，XHTML和HTML5标准
	缺点：不允许使用脚本。
	<object data="circle1.svg" type="image/svg+xml"></object>
	
	iframe
	优势：所有主要浏览器都支持，并允许使用脚本
	缺点：不推荐在HTML4和XHTML中使用（但在HTML5允许）
	<iframe src="circle1.svg"></iframe>
	
	也可以直接在html里嵌入 svg代码
	
	如果用jq或者js生成svg代码 需要在代码后再重新给svg赋值一次
		例如：$("svg").html($("svg").html())		//给svg重新赋值一次
		
	g标签
	g标签为svg常用的标签，g用于把相关元素进行组合的容器元素。
	在svg中提供了如g元素这样的将多个元素组织在一起的元素。由g元素编组在一起的可以设置相同的颜色，可以进行坐标变换

============================================图形=============================================

SVG有一些预定义的形状元素，可被开发者使用和操作：

		矩形<rect>
属性有 x/y/width/height/rx/ry/style
距离svg左方距离/距离svg上方距离/矩形宽度/矩形高度/上下两条线的圆角大小/左右两条线的圆角大小/一些样式值
圆角大小的最大值为宽度或者高度的一半 最大的话正方形为圆 矩形为椭圆 100%弯曲 如果设置百分比 则直接为最大值

style属性 fill stroke stroke-width fill-opacity stroke-opacity opacity
填充颜色/边框颜色/边框粗细/填充色的透明度/边框透明度/整体透明度

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="1000" height="1000">
		<rect x="100" y="300" width="300" height="100" rx="20" ry="5" style="fill:red;stroke:blue;stroke-width:10;fill-opacity:.3;stroke-opacity:.7"></rect>
	</svg>

===========================================================================================

		圆形<circle>
属性有cx/cy/r/stroke/fill/stroke-width/stroke-opacity/fill-opacity
中心x坐标/中心y坐标/半径/边框颜色/填充颜色/边框宽度/边框透明度/填充透明度
如果不写cx cy默认圆心在0 0 也就是在左上角

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="1000" height="1000">
		<circle cx="500" cy="500" r="200" fill="gray" stroke="red" stroke-width="10" stroke-opacity=".1" fill-opacity=".6"></circle>
	</svg>
		
===========================================================================================

		椭圆<ellipse>
属性有cx/cy/rx/ry/style
椭圆中心x坐标/椭圆中心y坐标/椭圆横向半径/椭圆纵向半径/样式
请注意rx/ry为半径 相互设置时候需要把 cx/cy考虑进去 
cx/cy需大于rx/ry才可以显示完整椭圆

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="1000" height="1000">
		<ellipse cx="500" cy="500" rx="500" ry="500" style="fill:yellow;fill-opacity:.8;stroke:springgreen;stroke-width:50;stroke-opacity:.9"></ellipse>
	</svg>
注:	如果图形和svg大小一样的话，stroke边框为一半在圆内一半在圆外，边框变大后，会往圆内凹回去，类似给里面设置了padding
		所以 圆的可视大小为半径加上边框的1/2

===========================================================================================

		直线	<line>
属性有x1/y1/x2/y2/style="stroke:red;stroke-width:2"
起始点的x坐标/起始点的y坐标/结束点的x坐标/结束点的y坐标/样式

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="1000" height="1000">
		<line x1="200" x2="800" y1="200" y2="800" style="stroke:red;stroke-width:10"></line>
	</svg>
		
===========================================================================================

		折线	<polyline>(首位不会相连)
属性有points/style
各个点的坐标/样式
style里有 fill/填充色 stroke/边框颜色 stroke-width/边框粗细 stroke-opacity/边框透明度 fill-opacity/填充色透明度

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600">
		<polyline points="100,100 200,200 100,300 200,400 100,100" style="fill:orange;stroke:black;stroke-width:5;"/>
	</svg>
注:填充色为首位相连填充，颜色   倾向于有点的那一面
	
===========================================================================================

		多边形<polygon>(不少于三个边的图形)(首位会相连)
属性有 points/style
各个点坐标/样式
style值有 fill/fill-opacity/stroke/stroke-width/stroke-opacity/fill-rule
填充色(颜色)/填充透明度(小数)/边框色(颜色)/边框粗细(数字)/边框透明度(小数)/填充规则(evenodd/nonzero)

代码：
	<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600">
		<polygon points="100,0 0,100 200,100 0,200 300,200 0,300 400,300 0,400 500,400 0,500 600,500 0,300" style="fill:red;stroke:black;stroke-width:5;fill-rule:evenodd" />
	</svg>
注：
	fill-rule 意思为指定使用哪一种算法去判断画布上的某区域是否属于该图形“内部” （内部区域将被填充）。填充规则。
	1.填充的是认为在内部的图形
	2.nozero 判断区域是否在图形内 
			从想要判断的区域内任意方向做一条线 检测射线与图形路径的交叉情况 从0开始计数 路径从左往右穿过 则加一 从右往左穿过 则减一
			如果为0则认为在图形外部 ， 根据1则不填充 ， 如果不为0则认为在图形内部
	3.evenodd 判断区域是否在图形内
			从想要判断的区域内任意方向做一条线 检测射线与图形路径的交叉点数量 
			如果为奇数 ， 则认为 在图形内部 。 如果为偶数 ， 则认为在图形外部 。

===========================================================================================

		路径<path> 
属性为d 通过d定义 值分别有(字母大写为绝对路径 ， 小写为相对路径)		//x为正数则在右边 👉 y为正数则在下边 👈
	
	绝对路径 这个点相对于整个svg容器的位置 如果写 H10 就是连接到上一个点所在平面(Y轴) X坐标为相对于svg的10 		//svg为参照物
		也就是(10，上一个点的Y轴坐标点[水平面])
	相对路径 这个以上一个点为参照物，如果h10，就是连接到 上一个点所在的平面(Y轴坐标) X坐标为相对于上一个点的10 	//上一个点为参照物
		也就是(上一个点距离svg左边的距离+10，上一个点的Y轴坐标[水平面])

		M/moveto L/lineto H/horizontal lineto(水平) V/vertical lineto(垂直) Z/closepath(闭合路径)
		C/curveto(曲线/三次贝塞尔曲线) S/smooth curveto(光滑曲线) 
		Q/quadratic Bézier curve(二次贝塞尔曲线)	T/smooth quadratic Bézier curveto(光滑的二次贝赛尔曲线)
		A/elliptical Arc(椭圆弧) 
		
		M/m(类似于画笔的位置 ， 起始点)			格式 M100 100/分别为x和y的坐标
		
		L/l(需要两个参数，x和y的坐标值，L命令会在当前坐标点和L指点坐标点之间画一条直线)			格式L200 200
		
		H/h(X坐标 如果为H则相对于整个svg的距离/如果为h则相对于上一个点的距离，Y轴为上一个点的Y轴坐标)
			也就是 Y轴坐标与上一个点相同 X轴坐标根据大小写进行判断 			格式H100/h100
			
		V/v(X坐标为上一个点的X坐标，Y坐标 如果为V则相对于整个svg的距离/如果为v则相对于上一个点的距离)
			也就是 X轴坐标与上一个点相同 Y轴坐标根据大小写进行判断			格式V100/v100
		
		Z/z(闭合标签 在上一个点和起始点之间连一条线 以闭合)						格式 Z (目前未发现大小写差别)
			如果在Z后再写 V 或者 H 时候，则从起始点开始连线
		代码
		<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600">
			<path d="M100 100 h100 v100 L170 130 z v500 C" stroke="black" stroke-width="3" fill="gray"></path>
		</svg>
		
		Q(二次贝塞尔曲线，共需要3个值才能绘制。M起始点，Q有两个参数，分别为控制点和结束点)
			控制点来决定起点和重点的曲线斜率
			
		T(贝塞尔曲线命令，只有一个值，即终点值)
		如果需要一个点的某一侧的控制点和另一侧的控制点对称的话，可以使用T命令
		T命令最好使用在Q命令或者T命令之后，它的第一个控制点为上一个控制点的对称点。
		T命令如果不再Q或者T命令之后，会变成一个点，控制点和终点为同一个点。所以画出来的就是一条直线。
		
		C(三次贝塞尔曲线，共需要4个值才能绘制三次贝塞尔曲线。M点起始点，C有三个参数，分别为控制点1/控制点2/结束点)
			控制点描述的是曲线起始点的斜率，曲线上各个点的斜率，是从起点斜率到终点斜率的渐变过程。
		代码：
		<svg xmlns="http://www.w3.org/2000/svg" width="600" height="600">
			<path d="M100 100 C200 200,200 200,600 10" stroke="black" stroke-width="3" fill="red"></path>
			<path d="M100 100 C200 150,200 150,600 10" stroke="black" stroke-width="3" fill="blue"></path>
			<path d="M100 100 C200 0,200 0,600 10" stroke="black" stroke-width="3" fill="pink"></path>
			<path d="M100 100 C200 50,200 50,600 10 Z" stroke="black" stroke-width="3" fill="green"></path>
			<path d="M100 100 C200 100,200 100,600 10 Z" stroke="black" stroke-width="3" fill="orange"></path>
		</svg>
		
		S(贝塞尔曲线命令，有两个值，其中一个为控制点，另一个为结束点。)
		如果想实现一个点某一侧的控制点与另一侧的控制点对称的话，可以使用S命令。
		如果S命令在C命令或者S命令后面，它的第一个控制点，则会认为是上一个控制点的对称点。
		如果它并不在C或者S命令后，那它的两个控制点[其中一个为对称的控制点]则会被认为为同一个控制点，类似变为二次贝塞尔曲线
		代码：
		<path d="M100 100 C0 100,0 500,100 200 S200 300 100 300" stroke="black" stroke-width="5" fill="transparent"></path>
		<circle cx="100" cy="100" r="2" stroke="red" stroke-width="10"></circle>
		<circle cx="0" cy="100" r="2" stroke="red" stroke-width="10"></circle>
		<circle cx="0" cy="500" r="2" stroke="red" stroke-width="10"></circle>
		<circle cx="100" cy="200" r="2" stroke="red" stroke-width="10"></circle>
		
===========================================================================================

		文本<text>
属性有x/y/font-size/fill/stroke/stroke-width/fill-opacity/stroke-opacity/opacity
意思为距离svg左边距离/距离svg上边距离/字体大小/填充颜色/对整个文字的边框颜色/边框宽度/填充透明度/边框透明度/整体透明度
属性有rotate/transform="rotate()" 
意思为文本内每一个文字的旋转角度/整体文本的旋转角度
代码：
	<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="1000" height="1000">
	  <text x="20" y="200" fill="red" fill-opacity=".5" font-size="200" st roke="black" stroke-width="10">I love SVG</text>
	</svg>

—————————————————————————SVG (可伸缩矢量图形)———————————————————————————— 

