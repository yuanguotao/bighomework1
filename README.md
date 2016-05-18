# bighomework1
<head>
<meta http-equiv="Content-Type" content="text/html; charset=gb2312" />
<title>全排列动态演示</title>
<style>
	body {
		background:#DDDDDD;
	}
	#content{
	background-color:#FFFFFF; 
	border: 2px solid black;
	height:80%;
	width:80%;
	}
	#content1{
	background-color:#CCCCFF;
	margin-top:5%;
	margin-left:2%;
	height:80%;
	width:60%;
	float:left;
	border: 2px solid blue;
	}
	#menu{
	margin-top:5%;
	margin-left:2%;
	border:0;
	float:left
	}
	.element{
	border:2px solid black;
	background-color:#CCCCCC;
	height:1%;
	width:1%;
	float:left
	}
	#div0{
	border:0;
	height:20%;
	}
	#div1{
	border:0;
	height:20%;
	}
	#div2{
	border:0;
	height:20%;
	}
	#div3{
	border:0;
	height:20%;
	}
	#div4{
	border:0;
	height:20%;
	}
	#1{
	float:left;}
	#2{
	float:left;}		
</style>
<script src="jquery-2.2.3.min.js"></script>

<script>

var tarray=new Array();  //创立二维数组，存储所有全排列结果；
var array=new Array();
var p=0;//记录总共有多少组结果;

for(var k=0;k<120;k++)//先初始化5个元素的二维数组用用；
{ //一维长度为i,i为变量，可以根据实际情况改变
	tarray[k]=new Array(); //声明二维数组，每一个一维数组里面的一个元素都是一个数组；
	for(var j=0;j<4;j++)
	{ 
		tarray[k][j]=""; //变量初始化；
 	}
}

function bala()//不弄就得不到input值得函数,操操操 ；
{
	var end=document.getElementById("num").value;
	end--;//为了与数组下标对应；
	var i=end;
	var x=0;
	for(var j=0;j<=i;j++)
	{
		array[j]=document.getElementById("int"+x).value;
		x++;
	}
	qpl(array,0,end);
}

function qpl(array,begin,end)  //全排列；
{
	var i;
	var q;
	if(begin==end)  //边界条件，排到最后一个数，直接输出当前数列； 
	{
		for(i=0;i<=end;i++) 
		{
			tarray[p][i]=array[i];
		}
		p++;
	}
	else
	{
		for(i=begin;i<=end;i++)  //将arry[begin]~arry[end]中每一个数与arry[begin]交换； 
		{
			q=array[i];
			array[i]=array[begin];
			array[begin]=q;
			qpl(array,begin+1,end);  //固定首元素后，将首元素之后的数全排列； 
			q=array[i];
			array[i]=array[begin];
			array[begin]=q;
	    }
	}
}


function append(i,num)
{
	if(num==3) {$("#div"+i).append("<table class='element'><td></td><td></td><td></td> </table>");}
	if(num==4) {$("#div"+i).append("<table class='element'><td></td><td></td><td></td><td></td> </table>");}
	if(num==5) {$("#div"+i).append("<table class='element'><td></td><td></td><td></td><td></td><td></td> </table>");}
}

	
var tru=1,fal=1;//用来让该死的获取值成功运行;
var cen=0;//当前层数，从0开始;
var al=0;//当前层有几个表格;
var sal=0;//当前属于上一层第几个表格;
var al1=1;//当前层应有表格总数;
var a=0,b=0;//交换位置;
var time=0;
var num=0;
var y;
var z=1;

function nextstep()
{

	if(z==1)
	{
	
	var i=0,j=0,q=0;
	var o=document.getElementById("num").value;
	num=parseInt(o);
	var c=document.getElementById("time").value;
	time=parseInt(c);
	if(al==al1&&cen==(num-1))   //全排列拍完;
	{
		$("#div"+cen).children().css("background-color","yellow");
		z=0;
	}
	
	else{
	
	if(tru==1&&cen==0) 
	{
		bala(),tru=0,al1=num;   //构建二维数组,赋初值al1;
		append(cen,num);       //生成第一层的空表格;
		for(i=0;i<num;i++)    //给第一层的表格赋值;
		 {
		 	q=document.getElementById("int"+i).value;
			$("#div0").children().children().children().children().eq(i).html(q);
		 }
		cen++;  //转到第二层;
	}
	
	else if(al<al1)   //从不是第一层开始，每一次做交换与勾勒其他全排列元素动画;
	{
		if(fal==1) {append(cen,num);}//1.生成一个空表格；
		if(al<(sal+1)*(num-cen+1)) //判定当前表格属于上一层那个表格的势力范围；
		{
			for(i=0;i<num;i++) //2.把属于上一层的表格的值赋给当前表格；
			{
			    q=$("#div"+(cen-1)).children().eq(sal).children().children().children().eq(i).html();
				$("#div"+cen).children().eq(al).children().children().children().eq(i).html(q);	
			}
		    
			y=al;
			
			$("#div"+cen).children().eq(al).children().children().children().eq(a).animate({fontSize:"1.8em"},time);         //3.改变需要交换的数字大小;
			
			$("#div"+cen).children().eq(al).children().children().children().eq(a).fadeOut(time,function(){
			
			if(cen==(num-1)) 	{ 	for(i=0;i<num;i++)																				  //5.把该层该表格本应有的值赋上;
										{	q=tarray[y][i];
											$("#div"+cen).children().eq(y).children().children().children().eq(i).html(q);}}
			if(cen==(num-2)) 	{ 	for(i=0;i<num;i++)
										{	q=tarray[y*2][i]
											$("#div"+cen).children().eq(y).children().children().children().eq(i).html(q);}}	
			if(cen==(num-3)) 	{ 	for(i=0;i<num;i++)
										{	q=tarray[y*2*3][i]
											$("#div"+cen).children().eq(y).children().children().children().eq(i).html(q);}}	
			if(cen==(num-4)) 	{ 	for(i=0;i<num;i++)
										{	q=tarray[y*2*3*4][i]
											$("#div"+cen).children().eq(y).children().children().children().eq(i).html(q);}}	
				});							
															
			$("#div"+cen).children().eq(al).children().children().children().eq(a).fadeIn(time);
						               
			$("#div"+cen).children().eq(al).children().children().children().eq(a).animate({fontSize:"1em"},time,function(){     
			               
			for(i=a+1;i<num;i++){   $("#div"+cen).children().eq(y).children().children().children().eq(i).css('color','red');   }
			});
			
			if(a!=b)
			{
			
			$("#div"+cen).children().eq(al).children().children().children().eq(b).animate({fontSize:"1.8em"},time)            //3.改变需要交换的数字大小;
			
			$("#div"+cen).children().eq(al).children().children().children().eq(b).fadeOut(time);
			
											
			$("#div"+cen).children().eq(al).children().children().children().eq(b).fadeIn(time);
						               
			$("#div"+cen).children().eq(al).children().children().children().eq(b).animate({fontSize:"1em"},time);     
			
			}
			al++;b++,fal=1;            //处理好当前表格，进行下一个;	
		}
		else {sal++,fal=0,b=a,nextstep();};
	}
	
	
	else if(al==al1){ cen++;al1=al1*(num-cen+1);al=0;a++;b=a;nextstep()} //当前层满，进行下一层;
	}
}
}

function start()
{	
	var h=document.getElementById("num").value;
	var u=parseInt(h);
	var both=1;
	var s=0;
	for(var i=u;i>=2;i--) {both=both*i;s=s+both;}
	s++;
	for(i=1;i<=s;i++)                                                                   //不知道怎样可以使含动画的函数依次循环n次；
	 {
	 	setInterval(nextstep(),500);
	 }
	
}
</script>
</head >
<body >
	<h1 id="2">全排列动态演示</h1> <p id="1">【老师请耐心的点下一步并且不要点太快...】</p>
	<div id="content">
	
		<div id="content1">
			<div id="div0">
			</div>
			<div id="div1">
			</div>
			<div id="div2">
			</div>
			<div id="div3">
			</div>
			<div id="div4">
			</div>
		</div>
		
		<div id="menu">
		<table border="0">
		<tr>
			<p><select id="type">
			<option value="1">递归算法</option>
			<option value="2">八皇后算法</option>
	    	</select></p>
		</tr>
		<tr>
			<p><form>
			元素个数：<input type="text" size="1px" id="num">
			</form></p>
		</tr>
		<tr>
			<p><form>
			元素：<input type="text" id="int0" size="1px" > <input type="text" id="int1" size="1px"> <input type="text" id="int2" size="1px"> <input type="text" id="int3"  size="1px">  <input type="text" id="int4"  size="1px"></form>
			</p>
		</tr>
		<tr>
			<p><form>
			动画速度：<input type="text" size="1px" id="time">（毫秒）
			</form></p>
		</tr>
		<tr>
			<p><button id="begin" onClick="start()" >开始</button> 	<button id="stop" >暂停</button>		<button id="over">结束</button> <button id="again">重置</button> </p>
		</tr>
		<tr>
			<P><button id="upstep"  >上一步</button> 		<button id="nextstep" onClick="nextstep()">下一步</button></P>
		</tr>
		</table>
		</div>
	</div>
		<p>【第一步：首位分别与其他位交换】【第二步：首位之后的元素全排列】【红色代表需要全排列的元素，黄色代表最终全排列】【目前只支持一步一步来，但支持任意n个元素】</p>
</body>
</html>
