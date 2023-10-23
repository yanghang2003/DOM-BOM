# DOM和BOM简介

## DOM和BOM简介

一个完整的 JavaScript 实现应该由下列三个不同的部分组成 ：

- ECMAScript 核心：为不同的宿主环境提供核心的脚本能力；
- DOM（文档对象模型）：规定了访问HTML 和XML 的应用程序接口；
- BOM（浏览器对象模型）：提供了独立于内容而在浏览器窗口之间进行交互的对象和方法。

通过前面的学习，相信大家已经掌握了javaScript的基础知识。但是，要想实现网页交互效果，仅仅掌握基础知识还是不够的。例如，通过JaveScript改变元素的内容，样式和属性，为元素注册事件，页面跳转，要实现这些功能，都需要用到DOM和BOM的相关知识。本次学习将针对其基本知识进行详细讲解



### DOM简介

DOM,全称(Document Object Model)文档对象模型 js中通过DOM来对HTML文档进行操作。只要理解了DOM就可以随心所欲操作我们的网页

DOM将整个文档视为树形结构，这个结构被称为文档树。下面具体解释DOM中的一些基本的名词

- 文档 : 一个页面就是一个文档，DOM中使用document表示
- 元素 : 页面中的所有标签都是元素，DOM中使用element表示
- 节点 ：网页中的所有内容都是节点（标签,  属性，文本，注释等），DOM中使用node表示

需要说明的是，元素是节点的一种类型，所有的元素都是节点：但节点不一定都是元素，因为节点还包括文本，注释等其他类型的节点。



### **获取元素**

在学习css中，要为HTML元素设置样式，首先需要通过css选择器选择目标元素，才能为目标元素设置样式。同理，利用DOM操作元素，首先也需要先获取目标元素，才能对目标元素进行操作。

#### **根据id获取元素**

设想一下，在页面中有一个无序列表，若要从列表中获取其中一项，即在众多li元素中获取一个，如何实现呢？此时可以为目标元素设置id属性作为唯一标识，然后结合document对象提供的getElementById()方法获取元素。

根据id属性获取元素的示例代码如下

```JS
document.getElementById('id属性值');
```

下面通过案例演示对该方法的使用

```HTML
 <body>
    <ul>
        <li id="flag">黑椒鸡排</li>
        <li>手撕鸡肉</li>
        <li>孜然牛肉</li>
        <li>鱼香肉丝</li>
    </ul>
    <script>
    //根据id属性获取元素
    var Chicken = document.getElementById('flag');
    console.log(Chicken);
    </script>
  </body>
```

打开开发者工具，进入控制台，查看运行结果，若控制台输出了一个id为flag的li元素，说明成功获取



#### **根据标签名获取元素**

如果要获取全部菜品，就要为每个元素设置id属性并通过getElementById()方法逐一获取，这是一件非常繁琐的事，所以document对象还提供了一中通过标签名获取元素的方法，即getElementByTagName()方法。

根据标签名属性获取元素的示例代码如下



```JS
document.getElementsByTagName('标签名');
```

获取标签内容为菜品的所有元素

```HTML
  <body>
    <ul>
        <li>黑椒鸡排</li>
        <li>手撕鸡肉</li>
        <li>孜然牛肉</li>
        <li>鱼香肉丝</li>
    </ul>
    <script>
    //根据标签名属性获取元素
    var lis = document.getElementsByTagName('li');
    console.log(lis);
    </script>
  </body>
```

#### **根据类名获取元素**

页面中，若要根据类名获取元素，则可以先为元素设置类名，然后使用document对象提供的getElementsByClassName()方法获取元素。

根据类名属性获取元素的示例代码如下

```JS
document.getElementsByClassName('类名');
```

上案例

```HTML
  <body>
    <ul>
        <li class='woman'>小红</li>
        <li class='woman'>女生</li>
        <li class='man'>男生</li>
        <li class='man'>小明</li>           
    </ul>
    <script>
    //根据类名woman获取元素
    var woman = document.getElementsByClassName('woman');
    //根据类名man获取元素
    var man = document.getElementsByClassName('man');
    console.log(woman[0]);
    console.log(man[0]);
    </script>
  </body>
```

#### 根据css选择器获取元素

根据css选择器获取元素的示例代码如下

```JS
document.querySelector('css选择器')
document.querySelectorAll('css选择器')
```

------

```HTML
  <body>
    <div class='play'>过山车</div>
    <div class='play'>摩天轮</div>
    <div class='play'>旋转木马</div>
    <div class='play'>电影院</div>
    <script>
    //获取类名为play的第一个div
    var firstdiv = document.querySelector('.play');
    console.log(firstdiv);
    //获取类名为play的所有div
    var alldiv = document.querySelectorAll('.play');
    console.log(alldiv);
    </script>
  </body>
```

#### 获取基本结构元素

|           属性           |                说明                |
| :----------------------: | :--------------------------------: |
| document.documentElement |         获取文档的html元素         |
|      document.body       |         获取文档的body元素         |
|      document.title      |         获取当前文档的标题         |
|      document.forms      | 获取文档中包含的所有form元素的集合 |
|     document.images      |    获取文档中包含所有images元素    |

### **事件基础**

#### **事件概述**

事件是一种"触发-响应"机制，产生行为后 对应的事件就被触发了，事件相应的事件驱动程序就会被调用，从而使网页响应交互效果。

事件有三个要素，分别是事件源，事件类型，事件驱动程序。

- 事件源:承受事件的元素对象
- 事件类型：使网页产生交互效果的行为对应的事件种类
- 事件驱动程序：事件触发后为了实现相应的网页交互效果而执行的代码。

#### **注册事件**

注册事件又称为绑定事件。在javaScirpt中，通过事件属性可以为操作的元素对象注册事件。

在标签中注册事件

<div onclick="">点我</div>

上述代码中，在onclick属性的值中可以编写事件驱动程序。

在JavaScript中注册事件

元素对象.事件属性 = 事件处理函数

```JS
element.onclick = function(){}
```

```html

  <body>
    <button id='btn'>单击</button>
    <script>
    //获取事件源
    var button = document.getElementById('btn')
    //为获取的元素注册鼠标单击事件
    button.onclick = function (){
        alert('hello');
    };
    </script>
  </body>
```

#### **元素内容操作**

对元素内容进行操作主要用到innerHtml和innerText两个属性

DOM中的innerHTML属性用于设置或获取元素开始标签和结束标签之间的HTML内容，返回结果包含HTML标签，并保留空格和换行，而innerText属性获取的元素内容不包含HTML标签

下面是一个示例

```HTML
 <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <body>
        <h1>innerHTML vs innerText</h1>
        <p id="exampleElement1"><span>原始内容 (innerHTML)</span></p>
        <p id="exampleElement2"><span>原始内容 (innerText)</span></p>
        <button onclick="changeContent()">点击修改内容</button>
          <script>
          function changeContent() {
            // 使用innerHTML设置元素的内容
            var element1 = document.getElementById("exampleElement1");
            console.log(element1.innerHTML);
            element1.innerHTML = "<strong>This is new content (innerHTML)</strong>";
            // 使用innerText设置元素的内容
            var element2 = document.getElementById("exampleElement2");
            console.log(element2.innerText);
            element2.innerText = "this is new content (innerText)";
          }
        </script>
      </body>
  </body>
  </html>
```

#### **元素样式操作**

在开发中，我们可能需要实现页面中关于元素样式的交互效果。对于这种交互效果，我们可以操作元素对象的style属性实现。操作style属性的示例代码如下

```JS
element.style.样式属性名 = '样式属性值';
```

当需要为元素设置多种样式时，如果通过style属性实现，需要编写多行，这种方式非常繁琐，因此，我们需要设置另一种设置样式的方法，即操作元素对象的className属性，

`element.className` = '类名'

```HTML
 <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <style>
    .myClass {
      color: red;
      font-size: 20px;
      background-color: yellow;
    }
  </style>
  <body>
    <div id="myElement">这是一个示例元素</div>
    <script>
        window.onload = function() {
          var element = document.getElementById("myElement");
          element.className = "myClass";
          element.style.color = "blue";
          element.style.fontSize = "24px";
          element.style.backgroundColor = "green";
        };
      </script>
  </body>
  </html>
```

我们还可以使用元素对象的classList属性。

```
element.classList
```

classList属性返回一个对象，称为classList对象。classList对象还可以通过一系列属性和方法对元素的类名进行设置和移除。

|            属性             |                             解释                             |
| :-------------------------: | :----------------------------------------------------------: |
|           length            |                      返回元素的类名数量                      |
|          **方法**           |                                                              |
|  add(class1, class2, ...)   | 添加一个或多个类名到元素中。如果类名已存在，则不会重复添加。 |
| remove(class1, class2, ...) | 从元素中移除一个或多个类名。如果类名不存在，则不会发生变化。 |
|    toggle(class, force)     | 切换一个类名的状态。如果类名存在于元素中，则移除它；如果类名不存在于元素                                              中，则添加它。如果指定了第二个参数force为true，则强制添加或移除该类名。 |
|       contains(class)       |            检查元素是否包含指定的类名，返回布尔值            |
|         item(index)         |                  返回元素指定索引位置的类名                  |
| replace(oldClass, newClass) |               替换元素中的一个类名为另一个类名               |

```HTML
<!DOCTYPE html>
  <html>
  <head>
  <style>
    .red {
      color: red;
    }
    .bold {
      font-weight: bold;
    }
  </style>
  </head>
  <body>
    <h1 id="myHeading">Hello World</h1>
    <script>
        // 获取元素
        var heading = document.getElementById("myHeading");
       // 添加类名
    heading.classList.add("red", "bold");
    </script>
  </body>
 </html>
```

#### **元素属性操作**

通过元素对象的setAttribute()方法可以设置属性，其语法格式如下。

```js
element.setAttribute('属性','值');
```

通过元素对象的getAttribute()方法可以获取属性值，其语法格式如下

```js
element.getAttribute('属性');
```

通过元素对象的removeAttribute()方法可以移除属性，其语法格式如下

```js
element.removeAttribute('属性')
```

```html

  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>

  <body>
    <div id="myDiv">这是一个示例</div>
    <script>
      // 获取<div>元素
      const myDiv = document.getElementById("myDiv");
      // 设置属性
      myDiv.setAttribute("class", "blue");
      myDiv.setAttribute("data-custom", "12345");
      // 获取属性值
      console.log(myDiv.getAttribute("class")); // 输出：blue
      console.log(myDiv.getAttribute("data-custom")); // 输出：12345
      // 删除class属性
      myDiv.removeAttribute("class");
      // 删除data-info属性
      myDiv.removeAttribute("data-custom");
      console.log(myDiv);
      
    </script>
  </body>
  </html>
```

#### **元素其他操作**

##### **获取元素位置和大小**

offsetTop 和 offsetLeft：获取元素相对于其定位父元素的上偏移和左偏移量。

var element = document.getElementById('myElement');

var topOffset = element.offsetTop;

var leftOffset = element.offsetLeft;



offsetWidth 和 offsetHeight：获取元素的宽度和高度，包括内边距和边框（但不包括外边距）。

var element = document.getElementById('myElement');

var width = element.offsetWidth;

var height = element.offsetHeight;



clientTop 和 clientLeft：获取元素的上边框和左边框的宽度。

var element = document.getElementById('myElement');

var topBorderWidth = element.clientTop;

var leftBorderWidth = element.clientLeft;



clientWidth 和 clientHeight：获取元素的可见区域的宽度和高度，不包括滚动条、内边距和边框。

var element = document.getElementById('myElement');

var clientWidth = element.clientWidth;

var clientHeight = element.clientHeight;



getBoundingClientRect()：获取元素相对于视口的位置和大小，返回一个包含top、left、bottom、right、width和height属性的DOMRect对象。

var element = document.getElementById('myElement');

var rect = element.getBoundingClientRect();

var top = rect.top;

var left = rect.left;

var width = rect.width;

var height = rect.height;

这些属性和方法可以帮助我们获取到元素在页面中的位置和大小信息，从而进行相应的布局和样式操作

##### **元素滚动操作**

https://cloud.tencent.com/developer/article/1942767

```HTML
 <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <style>
    .scrollable {
      width: 200px;
      height: 200px;
      overflow: auto;
    }
    .content {
      height: 1000px;
      background-color: #f2f2f2;
    }
    .highlight {
      background-color: yellow;
    }
  </style>
  <body>
    <div class="scrollable">
      <div class="content"></div>
    </div>
    <script>
      var scrollableElement = document.querySelector('.scrollable');
      var contentElement = document.querySelector('.content');
      function handleScroll() {
        if (scrollableElement.scrollTop > 100) {
          contentElement.classList.add('highlight');
        } else {
          contentElement.classList.remove('highlight');
        }
      }
      scrollableElement.addEventListener('scroll', handleScroll);
    </script>
  </body>
  </html>
```

上述代码定义了一个容器元素（.scrollable），内部包含了一个内容元素（.content）。当用户在容器元素中滚动时，通过监听scroll事件，判断滚动位置是否超过100像素，如果是则为内容元素添加.highlight类，使其背景色变为黄色。

##### **获取元素指针位置**

常见的鼠标位置属性包括以下几种：

clientX和clientY：鼠标相对于浏览器窗口客户区域左上角的水平和垂直坐标。这个坐标是相对于浏览器窗口的，不受滚动条的影响

pageX和pageY：鼠标相对于整个文档页面左上角的水平和垂直坐标。这个坐标是相对于文档页面的，会受滚动条的影响。

screenX和screenY：鼠标相对于用户屏幕左上角的水平和垂直坐标。这个坐标是相对于用户屏幕的，与浏览器窗口或文档页面无关。

offsetX和offsetY：鼠标相对于触发事件元素的水平和垂直坐标。这个坐标是相对于触发事件的元素的，不受父级元素的影响。

这些属性可以通过事件对象的相关属性来获取，比如mousemove事件的event对象。例如，使用clientX和clientY属性获取鼠标在浏览器窗口中的位置：

```JavaScript
document.addEventListener('mousemove', function(event) {
  var clientX = event.clientX;
  var clientY = event.clientY;
  console.log('鼠标在浏览器窗口中的位置：', clientX, clientY);
});
```

以上代码会监听所有鼠标移动事件，当鼠标移动时，会输出鼠标在浏览器窗口中的位置。你可以根据实际需求选择使用哪种坐标属性。

### **节点基础**

网页中的所有内容在文档树中都是节点，即元素，属性，文本等都属于节点，在学习节点操作前，我们需要学习节点的属性和层级。本节针对节点的属性和层级分别进行讲解。

#### **节点的属性**

节点有3个常用属性，分别是nodeName(节点名称)，nodeValue(节点值)，nodeType(节点类型)

- nodeName:用于获取节点名称，全大写形式，如<div>标签的节点名称为DIV。
- nodeValue:用于获取节点值，
- nodeType:用于获取数字表示的节点类型

节点类型   数字表示

元素节点      1

文本节点      3

属性节点      2

注释节点      8

文档节点      9

文档类型节点  10

#### **节点的层级**

1. 根节点（Root Node）：根节点是整个节点树的起点，
2. 父节点（Parent Node）：父节点是指在节点树中位于某个节点之上的节点。
3. 子节点（Child Node）：子节点是指位于某个节点下面的节点。
4. 兄弟节点（Sibling Node）：兄弟节点是指具有相同父节点的节点。

### **节点操作**

#### **获取节点**

1. 获取父节点

```
node.parentNode
```

上述语法中，node表示DOM节点对象，通过该对象的parentNode属性获取父节点。

```html
<body>  
    <div> 
        <h1> <span class="child">span元素</span> </h1> 
    </div>  
    <script>      
        var child = document.querySelector('.child');  
        console.log(child.parentNode);  
    </script> 
</body> 
```

2. 获取子节点

   |       属性        |                       说明                       |
   | :---------------: | :----------------------------------------------: |
   |    childNodes     |     获取父节点的所有子节点，返回一个节点列表     |
   |     children      | 获取父节点的所有子元素节点，返回一个元素节点列表 |
   |    firstChild     |             获取父节点的第一个子节点             |
   |     lastChild     |            获取父节点的最后一个子节点            |
   | firstElementChild |           获取父节点的第一个元素子节点           |
   | lastElementChild  |          获取父节点的最后一个元素子节点          |

   

3. 获取兄弟节点

   在DOM中，可以使用previousSibling属性和nextSibling属性获取当前节点的上一个兄弟节点和下一个兄弟节点

   如果想要获取兄弟元素节点，则可以使用nextElementSibling属性返回当前元素的下一个兄弟元素节点，使用previousElementSibling属性返回当前元素的上一个兄弟元素节点，

```html
<body>    
    <div>第一个</div>    
    <div class="second">第二个</div>    
    <div>第三个</div>     
    <script>     
    	var second = document.querySelector('.second');       
        console.log(second.previousSibling);           //获取当前节点的上一个兄弟节点            
        console.log(second.nextSibling);              //获取当前节点的下一个兄弟节点     
        console.log(second.previousElementSibling);  //获取当前节点的上一个兄弟元素节点          
        console.log(second.nextElementSibling);     //获取当前节点的下一个兄弟元素节点     
    </script>   
</body> 
```

#### **创建并添加节点**

1. 创建节点

使用document对象中的createElement()方法可以创建元素节点，因为该方法创建的节点是页面中原本不存在的，而这种方式也称为动态创建节点

document.createElement('标签名')

接下来通过代码演示节点的创建

```js
var div = document.createElement('div')
console.log(div); //结果为<div></div>
```



2. 添加节点

节点创建后，我们需要根据实际开发需求将节点添加到文档中的指定位置。DOM中提供了appendChild()方法和insertBefore()方法用于添加节点

```html
  <body>     
      <ul>         
          <li>第一个li元素</li>        
          <li>第二个li元素</li>     
      </ul>     
      <button>appendChild()</button>    
      <button>insertbefore()</button>   
      <script>        
          var ul = document.querySelector('ul');       
          var btn = document.querySelectorAll('button');      
          btn[0].onclick = function(){            
              var div = document.createElement('div');          
              div.innerHTML = '通过appendChild()方法新添加的节点';          
              ul.appendChild(div);      
          }       
          btn[1].onclick = function(){            
              var div = document.createElement('div');            
              div.innerHTML = '通过insertBefore()方法新添加的节点';                                                           ul.insertBefore(div,ul.children[1]);        
          }     
      </script>   
</body> 
```

3. 移除节点

开发过程中，根据实际需求，有时需要对节点进行移除操作。在DOM中，可以通过removeChild()方法将一个父节点的指定子节点移除，

node.removeChild(child)

具体代码如下

```html
   <body>  
       <ul>    
           <li>第一个元素</li>     
           <li>第二个元素</li>     
       </ul>    
       <button>移除ul元素中的第2个li元素节点</button>   
       <script>    
           var ul = document.querySelector('ul');   
           var btn = document.querySelector('button');    
           btn.onclick =  function(){       
               ul.removeChild(ul.children[1]);  
           };     
       </script>  
</body> 
```

4. 复制节点

开发过程中，有时会用到多个相同的节点，在这种情况下，连续创建相同的节点是一件繁琐的事情，此时可以使用DOM提供的cloneNode()方法复制节点

通过一个节点对象调用cloneNode()方法后，该方法会返回节点对象的副本，该方法的第一个参数为可选参数，默认为false，表示只复制节点本身，不复制节点内部的子节点，如果设为true，则表示复制节点本身及里面所有的子节点。

```HTML
<body>
    <ul>
        <li>第一个元素</li>
        <li>第二个元素</li>
    </ul>
    <button>移除ul元素中的第2个li元素节点</button>
    <script>
    var ul = document.querySelector('ul');
    var btn = document.querySelector('button');
    btn.onclick =  function(){
        ul.removeChild(ul.children[1]);
    };
    </script>
  </body>
```

### **事件进阶**

前面讲解了事件的概念以及事件的3个要素，接下来继续讲解事件的进阶内容，包括事件监听，事件移除和DOM事件流

#### **事件监听**

通过事件属性的方式注册事件，一个事件类型只能注册一个事件处理函数。而在javascript中还有一中为元素注册事件的方式，就是事件监听，通过事件监听可以给一个事件类型注册多个事件处理函数

在新版浏览器中，事件监听的语法格式如下

对象.addEventListener(type,callback,[capture])

上述语法中，addEventListener()方法可以为对象添加事件监听，该方法可以接受3个参数，第一个参数type表示事件类型，不带on前缀；第二个参数callback表示事件处理函数；第三个参数capture可选

默认值为false,表示在事件冒泡阶段完成事件处理，将其设置为ture时，表示在事件捕获阶段完成事件处理，关于冒泡和捕获的相关内容，会在后面讲解。

下面举一个案例

```HTML
  <body>
  <div id='t'>test</div>
  <script>
    var obj = document.getElementById('t')
    //添加第一个事件处理函数
    obj.addEventListener('click',function(){
      console.log('one');
    });
    //添加第二个事件处理函数
    obj.addEventListener('click',function(){
      console.log('two');
    });
  </script>
  </body>
```

#### **事件移除**

在开发过程中，可以根据需求对页面的事件进行移除，例如抽奖按钮，当抽奖次数达到上限的时候，抽奖按钮不在生效，

移除事件属性方式注册的事件，语法格式如下

对象.onclick = null;

移除事件监听方式注册的事件，语法格式如下。

对象.removeEventListener(type,callback);

上述语法中，type表示要移除的事件类型，callback表示事件处理函数，

```HTML
  <body>
    <div id='t'>text</div>
    <script>
      var obj = document.getElementById('t');
      //定义事件处理函数
      function test(){
        console.log('test')
      };
      obj.addEventListener('click',test);
      obj.removeEventListener('click',test);
    </script>
  </body>
```

#### DOM事件流

事件流

当浏览器发展到第四代时（IE4和Netscape Communicator4），IE和Netscape开发团队遇到一个很有意思的问题：页面哪个部分会拥有某个特定的事件？举个例子：一张纸上有一组同心圆，当手指放在圆心上时，那么指向的不是一个圆，而是所有圆。两家公司的浏览器开发团队看待这个问题是一致的：单机按钮的同时，你也单击了按钮的容器元素，甚至也单击了整个页面。

事件流描述的是从页面中接收事件的顺序。两个团队提出了几乎完全相反的事件流的概念。IE的事件流是事件冒泡流，而Netscape Communicator的事件流是事件捕获流。

W3C对两个公司进行中和处理，将DOM事件流分为3个阶段

- 事件捕获阶段：事件从document节点自上而下向目标节点传播的阶段。
- 事件目标阶段：事件流到达目标节点后，执行相应的事件处理函数的阶段。
- 事件冒泡阶段：事件从目标节点自上而下向document节点传播的阶段。

#### **事件冒泡**

事件冒泡，即从触发事件的节点(目标元素)，自下而上的去触发事件

我们给div和span都添加了事件，按照事件监听的规则，此时是冒泡执行，so，让我们看看会发生什么吧

```HTML
 <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <style>
  </style>
  <body>
    <div id="test">div
        <span id="test2">span</span>
    </div>
  </body>
  <script>
    let test = document.getElementById('test')
    test.addEventListener('click',() => {
        console.log('123')
    })
    let test2 = document.getElementById('test2')
    test2.addEventListener('click',() => {  //点击span盒子竟然先输出了456，但是为什么会输出123捏，这就是冒泡的知识了哈哈
        console.log('456')    
    })
  </script>

  </html>
```

即如果点击页面中的span元素(目标元素)，则click的传播顺序是

span-->div-->html-->document

click事件首先在span元素上发生，然后click事件沿DOM树向上传播，在每一级节点都会发生，直到传播到document对象。

#### **事件捕获**

事件捕获从document到触发事件的那个节点，即自上而下的去触发事件。

然后，我们再将flase变为true，那么此时会出现什么效果捏

```HTML
<script>
    let test = document.getElementById('test')
    test.addEventListener('click',() => {
        console.log('123')
    })
    let test2 = document.getElementById('test2')
    test2.addEventListener('click',() => {  //再次点击span的时候先输出了123，然后才输出456，这就是事件捕获
        console.log('456')    
    })
  </script>
```

即单击span后触发事件的顺序为

document-->html-->div-->span

注意：JavaScript中事件的类型有很多，但不是所有的事件都能冒泡，如blur事件，focus事件,mouseenter事件等不能冒泡。

#### **事件对象**

当一个事件被触发后，与该事件相关的一系列信息和数据的集合会被放入一个对象，这个对象称为事件对象。当事件存在时，事件对象才会存在，它是javaScript自动创建的，例如，鼠标单击的事件对象中，包含鼠标指针的坐标等相关信息。

```HTML
<!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <style>
    .div01 {
        color: white;
        background-color: black;
        width: 100px;
        height: 30px;
    }
  </style>
  <body>
    <div id="test" class="div01">事件对象</div>
  </body>
  <script>
    let test = document.getElementById('test')
    test.addEventListener('click',(e) => {
        console.log(e)   //事件对象就是它
    })
  </script>
  </html>
```

常用方法

|            方法            |                             说明                             |
| :------------------------: | :----------------------------------------------------------: |
|            type            |                         获取事件类型                         |
|      preventDefault()      |                      取消事件的默认行为                      |
|     stopPropagation()      | 阻止事件继续传播（冒泡和捕获），不包括在当前节点上其他的事件监听函数。 |
| stopImmediatePropagation() |  阻止所有事件继续传播，包括在当前节点上其他的事件监听函数。  |
|           target           |                      获取触发事件的对象                      |

阻止事件冒泡

对应一个注册了的事件的元素来说，有时我们希望只有该元素触发事件，因为事件冒泡的存在，该元素的子元素触发事件时会使该元素的事件触发，并且该元素的父元素的事件也会被触发，这种现象与预期效果不一致，所以要阻止事件冒泡

事件对象的stopPropagation()方法可以阻止事件冒泡

```
e.stopProgapation
```

document.getElementById('child').addEventListener('click', function(event) {

  event.stopPropagation(); // 阻止冒泡

  console.log('子元素点击事件');

});

document.getElementById('parent').addEventListener('click', function() {

  console.log('父元素点击事件');

});

#### **事件委托**

在生活中，快递派送时为了提高派送效率，快递员会把快递存放到相关代收机构，然后让客户自行领取，这种处理方式可称为委托。事件委托也是如此，其原理就是将子节点对应的事件注册给父节点，然后利用事件冒泡的原理影响到每个子节点，当子节点触发事件时，会执行注册在父节点上的事件，这样做的优点在于，不需要为每个子节点注册事件，而是只给父节点注册事件，当父节点动态添加子节点时，新添加的子节点也可以触发事件。

```HTML
 <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <style>
  </style>
  <body>
    <ul id="test3">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
  </body>
  <script>
    let test3 = document.getElementById('test3')
    test3.addEventListener('click',(e) => {
        e.target.innerHTML = '被点击了呜呜'   //点击之后相应的li内容就会改变
    },true)   //加不加true结果都是一样的
  </script>
  </html>
```

在实际开发中，使用javaScript开发网页交互效果时，经常需要获取浏览器的一些信息，控制浏览器的刷新和页面跳转。为了能够使JavaScript控制浏览器，浏览器提供了BOM，接下来将对其进行详细讲解

## BOM简介

在实际开发中，使用javaScript开发网页交互效果时，经常需要获取浏览器的一些信息，控制浏览器的刷新和页面跳转。为了能够使JavaScript控制浏览器，浏览器提供了BOM，接下来将对其进行详细讲解

浏览器对象模型（Browser Object Model,BOM）是浏览器提供的用于JavaScript与浏览器窗口进行交互的一系列对象。在DOM中，顶级对象是window,表示浏览器窗口，其他对象都是window对象的属性。

​                                         window

document    location    navigator    history      screen

document对象表示文档，它既属于BOM又属于DOM;location对象用于操作浏览器地址：navigator对象用于获取浏览器的基本信息;history对象用于操作历史记录；screen对象用来获取屏幕信息。

### **window对象**

window对象在JavaScript中具有双重角色，它既是浏览器窗口对象的一个全局对象，全局对象在书写时可以省略。例如，document,console,alert(),prompt()可以写成window.document  ,window.console ,window.alert(),window.prompt() 其中，document和console是window对象的属性,alert()和prompt()是window对象的方法。

|      常用属性      |                  说明                  |
| :----------------: | :------------------------------------: |
|  window.location   |        返回或设置当前窗口的URL         |
|  window.document   |  返回对当前窗口中显示的文档对象的引用  |
| window.innerWidth  | 返回窗口的视口宽度（包括滚动条和边框） |
| window.innerHeight | 返回窗口的视口高度（包括滚动条和边框） |

|        常用方法        |                         说明                         |
| :--------------------: | :--------------------------------------------------: |
|     window.open()      |                  打开新的浏览器窗口                  |
|     window.close()     |                    关闭浏览器窗口                    |
|     window.alert()     |           弹出一个警告框，带有指定的消息。           |
|    window.prompt()     | 弹出一个提示框，带有指定的消息和一个可编辑的文本字段 |
|    window.confirm()    |    弹出一个确认框，带有指定的消息和确定/取消按钮     |
|  window.setTimeout()   |    设置一个定时器，在指定的毫秒数后执行指定的函数    |
|  window.setInterval()  | 设置一个间隔定时器，在指定的毫秒数循环执行指定的函数 |
| window.clearTimeout()  |         清除由 setTimeout() 方法设置的定时器         |
| window.clearInterval() |        清除由 setInterval() 方法设置的定时器         |

这些属性和方法可以帮助开发者控制浏览器窗口、处理用户交互以及管理定时任务等

### **location对象**

location对象用于获取浏览器地址，通过location对象可以获取当前窗口的URL地址相关的信息，需要说明的是，location对象既是window对象的属性又是document对象的属性，window.location等同于document.location

里面封装当前窗口打开的url

1. location.href  完整的URL路径
2. location.protocol  协议名            
3. location.hostname  主机名
4. location.port  端口号
5. location.host  主机名+端口号        
6. location.pathname  文件路径
7. location.search  从？开始的参数部分
8. location.hash  从#开始的锚点部分

### **navigator对象**

navigator对象用于获取有关浏览器的信息

1. navigator.appCodeName;浏览器的代码名。
2. navigator.appName;完整的浏览器名称。
3. navigator.appVersion;浏览器的平台和版本信息。
4. navigator.userAgent;包含浏览器的名称、内核、版本号等。
5. navigator.plugins;检测有无插件。
6. navigator.onLine;表示是否连接到了因特网。

### **screen对象**

screen对象用于获取屏幕相关的信息，如屏幕的宽带和高度

1. screen.height;屏幕的像素高度
2. screen.width;屏幕的像素宽度
3. screen.availHeight;屏幕的像素高度减去系统部件高度之后的值(只读)
4. screen.availWidth;屏幕的像素宽度减去系统部件宽度之后的值(只读)
5. screen.availLeft;未被系统部件占用的最左侧的像素值(只读)[chrome和firefox返回0，IE不支持]
6. screen.availTop;未被系统部件占用的最上方的像素值(只读)[chrome和firefox返回0，IE不支持]

### **histroy对象**

history对象可以对用户在浏览器中访问过的历史记录进行操作，出于安全方面的考虑，history对象不能直接获取用户浏览过的历史记录，但可以控制浏览器的后退和前进等功能，下面是history对象常用的属性和方法

1. length; 查看浏览器的历史访问的网页的个数；
2. back(); 加载history列表中的前一个url
3. forward();加载history列表中的下一个url
4. go(); 加载history列表中的某个具体页面
5. go(0);相当于刷新页面

### **窗口事件**

窗口事件是指window对象的事件，它与整个窗口有关。常用的窗口事件有窗口加载与卸载事件，窗口大小事件。

#### **窗口加载与卸载事件**

如果要在窗口加载完成后要执行某些代码，或在窗口关闭时执行某些代码，可以使用window对象提供的窗口卸载与加载事件

 事件名称                       事件触发时机

  load                 窗口加载事件，当页面加载完毕后触发

  unload               窗口卸载事件，当页面关闭时触发

#### **窗口大小事件**

在开发中，有时需要知道用户是否在调整浏览器窗口大小，此时可以使用窗口大小事件resize，

```js
<script>
    window.addEventLisntener('resize',function(){
    console.log(document.body.clientWidth)
  });
</script>
```

## **作业**

1.填空题

事件的三个要素分别是_______

DOM中的______用于设置或获取元素开始标签和结束标签之间的HTML内容

通过元素对象的_____方法可以设置元素的自定义属性

将一个节点添加到父节点的所有子节点末尾用_____方法

____事件是在窗口改变时触发的

2.简答题

简述使用innerHTML属性和innerText属性操作元素内容有什么不同

简述如何获取鼠标指针在元素中的位置

简述DOM和BOM的区别

3.编程题

- 简易留言板
- Tab栏切换