# css-js-xuexibiji(慕课网https://www.imooc.com/code/8342）
学习css/js/jq的笔记：
jquery：
jQuery对象转化成DOM对象

		var $div = $('div'); //jQuery对象
		var div=$div.get(0);  //这里div是dom对象
    
DOM对象转化成jQuery对象  

    var div = document.getElementsByTagName('div'); //dom对象
    $div =  $(div);         //这里div是jQuery对象
    
Query选择器之层级选择器    

    > （大于号）紧跟父子关系 如$("div > p")表示选择div下的直接层是p的节点。

    + （加号）  紧跟兄弟关系 如$("div + p")表示选择div同层的后面的相邻的p节点。

    ~ （波浪线）任意距离兄弟关系 如$("div + p")表示选择div同层的后面的p节点。

    (空格)    任意层父子关系 如$("div p")表示选择div下的p节点（不管中间隔多少层）。

    ,(逗号)   表示选择器组合，如$("div p, span p")表示div下p节点和span下p节点。
    
jQuery选择器之基本筛选选择器

    - 匹配第一个元素：`$(":first")`，如`$("div:first").css('color', 'red');`

    - 匹配最后一个元素：`$(":last")`

    - 匹配索引为index的元素：`$(":eq(index)")`

    - 匹配索引大于index的元素：`$(":gt(index)")`   //greater than

    - 匹配索引小于index的元素：`$(":lt(index)")`      //littler than

    - 匹配索引为偶数的元素：`$(":even")`

    - 匹配索引为奇数的元素：`$(":odd")`
    
    $('div:has(:not(p))')         #含有不是p标签的任何其他标签的div，也可以含有p标签，p两边可以加引号可以不加
    
    $('div:has(:not(.pa))')         #含有不是p标签的任何其他标签的div，也可以含有.pa(class=pa)，.pa两边可以加引号可以不加
    
    $('div:not(:contains("asd"))')     #内部任何文本不含有asd的div，asd两边可以加引号可以不加
    
   
jQuery选择器之内容筛选选择器

	$(':contains(text)')  			查找指定标签内字符串，文本含有text（后代元素含有也行）

	$(':parent')				查找有内容的标签,也可以是文本（包括空格），似乎等于:not(:empty)

	$(':empty')				查找内容为空的标签，不能含有任何标签和文本，似乎等于:not(:parent)

	$('has:(selector)')			查找指定标签，内部含有selector（后代元素含有也行）
	
	
jQuery选择器之属性筛选选择器
	
	$("div[name]") 匹配含有name属性的div元素

	$("div[name='test']") 匹配name值为test的div元素
	
	$("div[name|='test']") 匹配name值等于test或以test-开头的的div元素,只能含有一个值（如name=aatest1 aatest2不匹配）

	$("div[name!='test']") 匹配name值不为test的div元素,name=test a的元素也能匹配,没有name属性也能匹配

	$("div[name*='test']") 匹配name值的文本含有test的div元素，如name='abc 8test1'
	
	$("div[name~='test']") 匹配有name值是test的div元素，如name='abc test'

	$("div[name^='test']") 匹配name值开头为test的div元素,如name='test123 asd'

	$("div[name$='test']") 匹配name值结尾为test的div元素,如name='t3 asdtest'

	$("div[id][name^='test']") 匹配有id属性且name值开头为test的div元素
	
	$("*[name]")和$("[name]") 匹配有name属性的所有标签
	
jQuery选择器之子元素筛选选择器

	$(".first-div a:first-child")查找class="first-div"下所有的a元素，且该a元素是它父元素下第一个子元素（父元素不需要满足.first-div）

	$(".first-div a:last-child")与first-child类似

	$(".first-div a:only-child")查找class="first-div"下所有的a元素，且该a元素是它父元素下唯一的子元素（父元素不需要满足.first-div，且不算文本元素）

	$(".last-div a:nth-child(2)")查找class="last-div"下的第二个a元素，条件同上

	$(".last-div a:nth-last-child(2)")查找class="last-div"下的倒数第二个a元素，条件同上
	
jQuery选择器之表单对象属性筛选选择器

	$(':enabled')选取可用的表单元素

	$(':disabled')选取不可用的表单元素

	$(':checked').attr('checked',false) 选取被选中的<input>元素,checked用于单选框和多选框

	$(':selected').attr('selected',false) 选取被选中的<option>元素，selected用于下拉列表

javascript>this 

    <script type="text/javascript">
        var p1 = document.getElementById('test1');
	p1.addEventListener('mouseover',function(){this.style.color='red';this.style.fontSize='22px';},false);
	p1.addEventListener('mouseout',function(){this.removeAttribute('style')},false);
    </script>

jquery>this

    <script type="text/javascript">
	$('#test1').mouseover(function(){$(this).css('color','red').css('font-size','22px')});
	$('#test1').mouseout(function(){$(this).removeAttr('style')});
    </script>

jQuery的属性与样式之.attr()与.removeAttr()

	$(':input').attr('value',function(){return $(this).attr('type')});			
	$(':input').attr('value','bakabaka');		#$(':input')似乎返回一个列表，attr赋值时会被遍历
	$(':input:eq(3)').removeAttr('value');
	$(':input').eq(3).removeAttr('value');		#和上面一样的结果

jQuery的属性与样式之.val()

	.val()方法，当没设置value属性时，获取的是<option>中的文本，如“ <option>慕课网</option>”获取到的是“慕课网”；
	设置了value属性的话，获取到就是value的值，如“<option value=‘imooc’>慕课网</option>”获取到的是“imooc”而不是“慕课网”了。

	<select id="animation">
		<option value="1">stop()</option>
		<option value="2" selected>stop(true)</option>
		<option value="3">stop(true,true)</option>
    	</select>
	$(document).ready(function(){
		$('#animation').change(function(){
			$('p').text($('#animation').val());
						})
					})
	1,.val()无参数，获取匹配的元素集合中第一个元素的当前值
	2,.val( value )，设置匹配的元素集合中每个元素的值
	3,.val( function ) ，一个用来返回设置值的函数
	
	
jQuery的属性与样式之增加样式.addClass()

	$('.left div').addClass('newClass');	#直接添加className
	$("div").addClass(function() {		 #用函数添加
		if(-1 !== $(this).attr('class').indexOf('imo')){
                	$(this).addClass('imoocClass')        
            }
	})				#直接删除，不return
		
jQuery的属性与样式之删除样式.removeClass()
	
	$('div').removeClass('newClass');
	$('.right > div:first').removeClass(function(){
           	$(this).next().addClass($(this).attr('class'));
        	return 'imoocClass' 		
        	})			#return什么删除什么

jQuery的属性与样式之切换样式.toggleClass()

	$("#table tr").toggleClass("c");		#classname里没有c就添加c，有就删除c，进行切换
	
jQuery的属性与样式之样式操作.css()

	$('.first').css('background')    	#返回background的值
	$('.fourth').css({'color':'red','font-size':'33px'}) 	 #用字典传参数
	$('.fifth').css('background','green')			 #传参数
	$('.sixth').click(function(){				 #函数传参
		$('.sixth').css('font-size',function(){
            		b=$(this).css('font-size').split('px');
        		return Number(b[0])+1+'px'
			})
		})
	.addClass()方法是通过增加class名的方式，那么这个样式是在外部文件或者内部样式中先定义好的，等到需要的时候在附加到元素上
	.css()方法处理的是内联样式，直接通过元素的style属性附加到元素上的；
	通过.css方法设置的样式属性优先级要高于.addClass方法
	.addClass()本质只是针对class的类的增加删除，不能获取到指定样式的属性的值，.css()可以获取到指定的样式值。

