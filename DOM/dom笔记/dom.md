#第六章 DOM
####6.1 dom概述
6.1.1 DOM的概念
DOM文档对象模型,DOM对象不仅仅是一个普通的内置对象,他还是一个巨大的API的核心对象,他将文档的内容呈现在js面前,并赋予了js操作文档的能力.

6.1.2 DOM和JavaScript的关系
一个web页面是一个文档,这文档可以在浏览器窗口或者作为html源代码显示出来.但上述两种情况都是同一个文档,DOM提供了对同一份文档的另一种表现,存储和操作的方式.DOM能够使用JavaScript脚本语言进行修改.

6.1.3 DOM节点
加载HTML页面是,web浏览器生成一个树形结构,用来表示页面的内部结构.DOM将这种结构理解为节点组成.根据w3c的html DOM标准,html文档找那个所有的内容都是节点.

> 整个文档是一个文档节点
> 每个HTML元素是元素节点
> HTML元素内的文本是文本节点 
> 每个HTML属性都是属性节点
> 注释也是节点,叫注释节点

				
6.1.4 DOM树
DOM树体现着html页面的层级结构,而DOM树有DOM文档树和DOM元素树两种,DOM元素树包含的只有元素节点,而DOM文档树则包括DOM文档中的所有内容.

####6.2 获取元素
6.2.1 用Id获取元素
getElementById()的方法,接受一个参数:获取元素的id,如果找到相应元素,则返回该元素,否则返回null.

       //用变量    文档  找   元素  用Id   'd'
        var d = document.getElementById('d');

6.2.2 用标签名获取元素
getElementsByTagName()可以获取该元素下所有的元素,返回一个伪数组,或者是节点列表.

        var lis = document.getElementsByTagName('li');
        //伪数组
        console.log(lis);

在某一个元素中,并不是在全局文档中利用标签获取元素,这样更加精准.

       var ul = document.getElementById('ul');
       var list = ul.docoment.getElementsByTagName('li');
       console.log(list);

当元素只有一个的时候,返回的也依然是一个列表,而不是一个元素,可以通过数组的下表找到该元素.

      var div = document.getElementsByTagName('div');
      console.log(div[0]); 

6.2.3 用类名获取元素
        var a = document.getElementsByClassName('a');
        console.log(a);
 
6.2.4 用选择器获取元素
querySelector()和querySelectorAll()可以依靠选择器找到元素,但是前者只能找到元素列表的第一个元素,而后者可以全部找到.注意,该方法性能没有直接利用标签寻找高.

        var ul = document.getElementById('ul')
        var x = document.querySelector('#div>div a');
        var lis = ul.querySelectorAll('li');
        console.log(lis);

6.2.5 用name属性值获取元素
getElementsByName()方法可以获取相同名称的name元素,返回一个伪数组对象.

        <input type="radio" name="sex" value="0">男 
        <input type="radio" name="sex" value="1">女
    
        var sex = document.getElementsByName('sex');
        console.log(sex);

####6.3 获取和设置元素中的其他信息

6.3.1 获取元素名
当我们使用id获取元素的时候,元素的名称会和整个元素一起显示出来.如果想要拿到该元素的元素名,也就是标签名则需要用tagName属性.

tagName属性,该属性只能获取,不能设置.

    var div = document.getElementById('mydiv');
    console.log(div.tagName);//DIV

6.3.2 获取元素节点里的内容
当获取了元素之后,如果我们需要拿到元素中的内容(所有东西),则需要用另一种方法得到,元素里的内容可能包括:文本或元素.需要用innerHTML属性.	

        var div = document.getElementById('mydiv');
        console.log(div.innerHTML);//获取元素内容

innerHTML属性除了可以获取标签内的内容外,还可以设置标签内的内容.

6.3.3 获取元素节点中的文本
利用innerText属性获取的只能是文本节点,不能是其他,当然innerText属性除了获取,也可以设置元素中的文本.

      var div = document.getElementById('mydiv');
      console.log(div.innerText);

      div.innerText = 'hello';

6.3.4  获取元素的类名
利用className属性获取元素的类名,以字符串的形式返回.同时可以设置新的class类名,需要注意的是,返回值是一个字符串,如果更换其中一个类,则需要考虑该字符串中其他类是否应该一起设置

        var md = document.getElementById('mydiv');
        console.log(div.className);
    
6.3.5 获取元素样式
style属性可以获取元素内联样式的所有属性,当然如果继续在style中找到属性名如:backgroundColor,就可以得到该属性的值,以字符串的形式返回.同时也可以设置该属性,从而达到增加或更改样式.需要注意的是,以js形式增加的样式的优先级大于css优先级.

    <div style="background-color:blue;"></div>
    <script>
      var div = document.getElementsByTagName('div');
    //js拿到和获取的是内联
      console.log(div[0].style.backgroundColor);

##练习
1.随便用一个标签,给他一个id属性.
2.获取这个元素的标签名
3.如果这个元素是加粗的,就把它变成不加粗显示


     <h1 id="mytag">写点字</h1>
      <script>
      var mytag = document.getElementById('mytag');
      console.log(maytag.tagName);

      //那些标签是加粗的,h1~h6 ,b , strong
      if(maytag.tagName == 'H1' || mytag.tagName == 'H2' || mytag.tagname =='H3'|| mytag.tagName == 'H4' || mytag.tagName == 'H5' || mytag.tagName == 'H6' || mytag.tagName == 'B' || mytag.tagName == 'STRONG' ){
      mytag.style.fontWeight = 400;
    }

    //方法二:
    //不管是不是粗体,统一变为细体
    mytag.style.fontWeight = 400;

    //方法三:
    var arr = ['H1','H2','H3','H4','H5','H6','B','STRONG'];
    // console.log(arr.indexOf('DIV'))
    // 检测数组里是否有粗体的标签名,返回-1以外都是粗体
    var is = arr.indedxOf(mytag.tagName);
    console.log(is);
    //判断如是粗体标签名  就改变样式
    if(is != -1){
        mytag.style.fontWeight = 200;
        mytag.style.color= 'red';
    }


需求2:  
1.在一个列表标签中,插入三个无序内容块
2.内容分别为:苹果、西瓜、草莓

需求3:
1.一个200*200的红色方框,一个按钮
2.点击按钮,让红色方框变成蓝色
3.必须用className的赋值方法

####6.3.6 获取元素的属性
getAttribute('')可以获取元素的某个属性,要将属性名称放在括号中记得要用引号括起来.返回值就是字符串形式的属性值.


       var div = document.getElementById('mydiv');
       var  a = document.getElementsByTagName('a');

       console.log(div.getAttribute('data-lj'))
       console.log(a[0].getAttribute('href'))


有get 有set

#####6.3.7 设置元素属性
setAttribute()可以设置元素的某个属性,第一个参数是属性名,第二个参数是属性值,都需要引号括起来以逗号分隔.
         
         var div = document.getElementsByTagName('div');
         var a = document.getElementsByTagName('a');
         div[0].setAttribute('id','mydiv');
         a[0].setAttribute('href','http://www.baidu.com');

#####6.3.8 删除元素属性
使用removeAttribute(),可以删除某个元素的某个属性,括号中放入需要删除的属性名,用引号包括.

         var div = document.getElementById('mydiv');
         div.removeAttribute('id');
