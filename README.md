<html lang="en-US">
<head>
  <meta charset="UTF-8">
	<title></title>
</head>
<body>
	
<div class="chead">简介</div>
<p>
	　　之所以写这个库，缘起于一次baidu无线阿拉丁项目，本来作为前端开发者，使用惯了jquery，而且jquery也给力的发布了jquery的mobile库。但是。。。。悲剧的是他居然是依赖于原来的jquery库。哎，各种压缩过之后依然不小啊。国外有个zepto.js， &nbsp;仿jquery针对html5封的一个库，高度模仿啊，以至于能无缝的对接各个jquery第三方库。膜拜一下。但是awen开发中发现了一些bug，这里就不详细说了。总之，本人不爽了。为了以后自己不再蛋疼，才想自己封一个库，精简点，支持链式，不要那么多功能，可扩展。所以想了想就叫 simple javascript 吧，简称sjs。</p>
<p>
	　　首先，它跟jquery的模式也差不多，一些个人喜欢的jquery的方法也封了进去，当然也加了一些自己的api。主要是为了减轻从新熟悉api的过程。值得注意的是它只针对于支持html5的智能手机浏览器，所以jquery的第三方selector就被干掉了，取而代之的当然就是querySelectorAll了，所以选择器的功能，省代码啊~~嘎嘎。前面说了精简，那么一些俺不经常用的api肯定被就简化了（O(∩_∩)O）比如jquery的index在这里只能获取当前元素的索引。position,width，height统一为了getBox等等。。。众口难调嘛~不过各位有需要的话可以自己扩展或者给我邮件讨论。
</p>
<p>
	　　虽然说了针对于html5，但是习惯性的，有许多接口基本上还是考虑了兼容,因为有些移动客户端浏览器也相当的不给力，比如iphone3的原生safari就不支持JSON等。于是代码量比预期的臃肿了。。。哎。最起码智能手机开发要兼容啊。。当然本库没有与jquery相比的意义，我还没自大到可以与一个庞大后勤部队支持的jquery比肩，这毕竟是第一个版本，以后会优化。
</p>
<div class="chead"> API介绍</div>
<p>
	　　如果不太特殊说明，表明该接口与jquery用法相同，具体示例与说明请查阅jquery文档。
	<div class="pin40">
		<span class="red">*</span> 该api与jquery是有所不同的，是扩展或者精简了的接口。但不影响使用
		<br><span class="red">new</span> 新增接口
	</div>

</p>	
<h3>一 选择器 </h3>
<div class="indent">
	<h4 >1。元素选择器 <span class="red">*</span></h4>
	<div>　基础用法跟jquery差不多。全局的变量为$或者sjs。效率方面据我测试，jquery也就是是标签选取的时候比较快（下例第一个），稍微复杂点，比如id,class等就完球了。既然用的querySelector选择器那么写法当然是标准的，就不一一写出来了，下面简单举几个例子。</div>
	<ol class="code">
		<li>var divs=$("div"),</li>
		<li>test=$("#test"),</li>
		<li>span=$("#test>span"),</li>
		<li>cssd=$("ul[name=cssd]");</li>
		<li>var d=document.getElementById("d");dd=$(d);(这样貌似也可以用到非html5浏览器了)</li>
	</ol>
</div>
<h3>二 sjs核心</h3>
<div class="indent">
	<h4 >1。sjs对象核心函数</h4>
	<ul class="detail" >
		<li class="title">sjs(function($){}) </li>
		<li class="tip">dom加载完成后的执行函数</li>
		<li class="title">each(callback)</li>
		<li class="tip">以每一个匹配的元素作为上下文来执行一个函数。返回 'false' 将停止循环 (就像在普通的循环中使用 'break')。返回 'true' 跳至下一个循环(就像在普通的循环中使用'continue')。
</li>
		<li class="title">length</li>
		<li class="tip">当前sjs对象中元素的个数。</li>
		<li class="title">selector</li>
		<li class="tip">记录sjs对象的原始选择器</li>
		<li class="title">get(index)</li>
		<li class="tip">取得其中一个匹配的dom元素。num表示取得第几个匹配的元素。</li>
		<li class="title">index() <span class="red">*</span></li>
		<li class="tip">返回对象本身相对于父对象的索引,从0开始计数。,<span class="red">*</span>cut掉了jquery中该接口的其他功能</li>
	</ul>
	<h4 >2。数据缓存</h4>
	<ul class="detail" >
		<li class="title">data([key],[value])</li>
		<li class="tip">在一个sjs对象上存放数据,而不是像jquery一样在每个匹配的dom上存放数据。但是参数用法一样。返回sjs对象或者数据。
</li>
		<li class="title">removeData([name|list])</li>
		<li class="tip">在元素上移除存放的数据</li>
	</ul>
	<h4 >3。DOM操作</h4>
	<ul class="detail" >
		<li class="title">html([val|fn])</li>
		<li class="tip">获取或者设置匹配元素的html内容，获取时只获取第一个匹配元素的html内容，设置时可以使回调函数，传入的参数为（index,oldHTML）</li>
		<li class="title">css(name|pro|[,val|fn])</li>
		<li class="tip">于jquery唯一的不同就是不支持驼峰写法</li>
		<li class="title">addClass(class|Array|fn) <span class="red">*</span></li>
		<li class="tip">为每个匹配的元素添加指定的类名。<span class="red">*</span>也可以接受数组</li>
		<li class="title">removeClass([class|Array|fn]) <span class="red">*</span></li>
		<li class="tip">从所有匹配的元素中删除全部或者指定的类。没参数删除所有<span class="red">*</span>也可以接受数组</li>
		<li class="title">toggleClass(class|Array|fn) <span class="red">*</span></li>
		<li class="tip">如果存在（不存在）就删除（添加）一个类。<span class="red">*</span>去掉了没怎么用过的参数switch</li>
		<li class="title">remove() <span class="red">*</span></li>
		<li class="tip">删除符合要求的节点。<span class="red">*</span>参数中的选择器去掉了</li>
		<li class="title">getBox() <span class="red">new</span></li>
		<li class="tip">返回dom列表中第一个元素的相对于浏览器左上角的Box模型信息</li>
		<li class="code">
			$("div").getBox();<br>
			返回值: {left:8,right:1356,top:8,bottom:26,width:1348,height:18}
		</li>
		<li class="title">inBox(x,y) <span class="red">new</span></li>
		<li class="tip">检测所给点是否在box模型内，x，y均相对于浏览器窗口左上角，event可用clientX,clientY</li>
	</ul>
	<h4 >4。事件</h4>
	<ul class="detail" >
		<li class="title">on(type,[data],fn)<span class="red">*</span></li>
		<li class="tip">新的利用事件委托机制实现的事件绑定行为，不再像jquery一样提供selector参数。，回调函数的event.data来获取传入的data值，event.firecnt来获取执行的次数，另外如果函数返回false，那么函数将自动解除绑定，可定制性更高</li>
		<li class="title">off(type,[data],fn)<span class="red">*</span></li>
		<li class="tip">解除用.on()或者.one()绑定的事件，不再像jquery一样提供selector参数。只有一个type参数将取消本dom对象该type的所有函数绑定,参数个数为0将清除该对象的所用绑定事件</li>
		<li class="title">trigger(type)<span class="red">*</span></li>
		<li class="tip">执行dom对象的绑定事件</li>
		<li class="title">one(type,[data],fn)<span class="red">*</span></li>
		<li class="tip">为每一个匹配元素的特定事件绑定一个一次性的事件处理函数。</li>
		<li class="title"><del>bind(type,[data],fn)</del></li>
		<li class="tip">on的别名。只是为了兼容预留</li>
		<li class="title"><del>unbind(type,[data|fn]])</del></li>
		<li class="tip">off的别名，只是为了兼容预留</li>
	</ul>
</div>
<h3>三 扩展</h3>
<div class="indent">
	<h4 >1。工具类</h4>
	<ul class="detail" >
		<li class="title">$.uniqueId() </li>
		<li class="tip">返回一个唯一数</li>
		<li class="title">$.isArray(o) </li>
		<li class="tip"> 检测对象是否数组,本来html5的Array对象本身自带isArray(o)方法判断。但是为了某些智能机的低端浏览器。。</li>
		<li class="title">$.isBoolean(o)</li>
		<li class="title">$.isString(o)</li>
		<li class="title">$.isFunction(o) </li>
		<li class="title">$.isNumeric(o) </li>
		<li class="title">$.isXML(o) </li>
		<li class="title">$.isObject(o) </li>
		<li class="title">$.isPlainObject(o) </li>
		<li class="tip">检查对象是否简单对象类型，主要用于检测json</li>
		<li class="title">$.isEmptyObject(o) </li>
		<li class="tip">检查对象是否空对象类型，主要用于检测json和array</li>
		<li class="title">$.eval(o) </li>
		<li class="tip">用Function构造器重写了eval</li>
		<li class="title">$.isEmptyString(o) </li>
		<li class="tip">检查字符串是否空串</li>
		<li class="title">$.trim(o) </li>
		<li class="tip">去除字符串的首尾空格</li>
		<li class="title">$.extend([deep], target, object1, [objectN]) </li>
		<li class="tip">用一个或多个其他对象来扩展一个对象，返回被扩展的对象。如果不指定target，则给sjs命名空间本身进行扩展。该方法是扩展sjs的主要方法，如果第一个参数设置为true，则sjs返回一个深层次的副本，递归地复制找到的任何对象。否则的话，副本会与原对象共享结构。 未定义的属性将不会被复制，然而从对象的原型继承的属性将会被复制。如要合并数组用$.merge()</li>
	</ul>
	<h4 >2。数组|对象操作</h4>
	<ul class="detail" >
		<li class='title'>$.inArray(value,array,[fromIndex])</li>
		<li class="tip">确定第一个参数在数组中的位置，从0开始计数(如果没有找到则返回 -1 )。</li>
		<li class="title">$.each(obj,callback) </li>
		<li class="tip">通用例遍方法，可用于例遍对象和数组。
不同于例遍对象的 $().each() 方法，此方法可用于例遍任何对象。回调函数拥有两个参数：第一个为对象的成员或数组的索引，第二个为对应变量或内容。如果需要退出 each 循环可使回调函数返回 false，其它返回值将被忽略。与jquery的不同之处在于，过滤函数中的this是待过滤对象本身而不是jquery的window。</li>	
		<li class="title">$.grep(o,callback,[invert])</li>
		<li class="tip">使用过滤函数过滤数组元素。
此函数至少传递两个参数：待过滤数组和过滤函数。过滤函数必须返回 true 以保留元素或 false 以删除元素。返回过滤后的数组，该函数不修改原数组。。"invert" 为 false 或未设置，则函数返回数组中由过滤函数返回 true 的元素.与jquery的不同之处在于，过滤函数中的this是待过滤对象本身而不是jquery的window。</li>
		<li class="title">$.merge(first,second) </li>
		<li class="tip">合并两个数组返回的结果会修改第一个数组的内容——第一个数组的元素后面跟着第二个数组的元素。要去除重复项，请使用$.unique().(吐槽：真不知道有concat用merge干嘛不就是，返回值变了，哎兼容留着吧)</li>
		<li class="title">$.unique(array) <span class="red">*</span> </li>
		<li class="tip">数组去除重复元素，返回去重后的数组，不修改原数组。值得注意的是数组中的元素只能是基本数据类型，如数字，字符串,不同于jquery中的只能过滤dom数组</li>
		<li class="title">$.map(arr|obj,callback)</li>
		<li class="tip">将一个数组中的元素转换到另一个数组中。作为参数的转换函数会为每个数组元素调用，而且会给这个转换函数传递一个表示被转换的元素作为参数。转换函数可以返回转换后的值、null（删除数组中的项目）或一个包含值的数组，并扩展至原始数组中。</li>
		<li class="title">$.remove(arr|obj,k|v,isval)<span class="red">new</span></li>
		<li class="tip">从对象或者数组中删除给定的键或者值，第三个参数确定第二个参数的类型，true为值，默认为键.<span class="red">注意，别在数组正向循环中使用它，否则索引会混乱</span></li>
	</ul>
	<h4 >3。JSONS对象<span class="red">new</span></h4>
	<div class="tip">将所有的json操作给整合在了一起，本来用html5的parse stringify就够了，谁知道天杀的safari3.2居然不支持，我晕。还要单独实现</div>
	<ul class="detail" >
		<li class="title">parse(string)</li>
		<li class="tip">格式化字符串为json或者数组</li>
		<li class="title">stringify(json|array)</li>
		<li class="tip">将字符串格式化为数组或者json</li>
		<li class="title">parseQuery(string)</li>
		<li class="tip">将&连接的query串格式化为json（经常用于格式化url后的search）</li>
		<li class="title">toQuery(json)</li>
		<li class="tip">将json格式化为&连接的query串</li>
		<li class="title">count(json)<span class="red">new</span></li>
		<li class="tip">返回json中元素的个数</li>
	</ul>
	<h4 >4。AJAX对象</h4>
	<div class="tip">常规ajax操作（~稍后更新）</div>
	<ul class="detail" >
		<li class="title">$.ajax(url,[settings])</li>
		<li class="tip"></li>
	</ul>
</div>

</body>
</html>