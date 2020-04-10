# 一、水平居中
(1)文本/行内元素/行内块级元素
```
#parent{
    text-aligh:center;
}
```
(2)单个块级元素
```
#son{
    width: 100px; /*必须指定宽度*/
    margin: 0 auto;
}
```
(3)多个块级元素
```
#parent{
    text-align: center;
}
.son{
    display: inline-block; //儿子变成行内/行内块元素
}
```
(4)绝对定位
```
#parent{
    heigh: 200px;
    width: 200px;
    position: relative; //父相
    background-color: #f00
}
#son{
    position: absolute; //子绝
    left: 50%;
    transform: translateX(-50%);
    width: 100px;
    height: 100px;
    background-color: #00ff00;
}
```
(5)任意个元素(flex)
```
#parent{
    display: flex;
    justify-content: center;
}
```
**本章小结**：
- 对于水平居中，我们应该先考虑，哪些元素有自带的居中效果，最先想到的应该就是 text-align:center 了，但是这个只对行内内容有效，所以我们要使用 text-align:center 就必须将子元素设置为 display: inline; 或者 display: inline-block; ；
- 其次就是考虑能不能用margin: 0 auto; ，因为这都是一两句代码能搞定的事，实在不行就是用绝对定位去实现了。
- 移动端能用flex就用flex，简单方便，灵活并且功能强大，无愧为网页布局的一大利器！

# 二、垂直居中
(1)单行文本/行内元素/行内块级元素
```
#parent{
    height: 150px;
    line-height: 150px;
}
```
(2)多行文本/行内元素/行内块级元素
```
#parent{
    height: 150px;
    line-height: 30px;
}
```
(3)图片
```
#parent{
    height: 150px;
    line-height: 150px;
    font-size: 0;
}
img#son{
    vertical-align: middle;
}
```
(4)单个块级元素

(4-1)table-cell
```
#parent{
    display: table-cell;
    vertical-align: middle;
}
```
(4-2)绝对定位
```
/*原理：子绝父相，top、right、bottom、left的值是相对于父元素尺寸的，然后margin或者transform是相对于自身尺寸的，组合使用达到水平居中的目的*/
#parent{
    height: 150px;
    position: relative;  /*父相*/
}
#son{
    position: absolute;  /*子绝*/
    top: 50%;  /*父元素高度一半,这里等同于top:75px;*/
    transform: translateY(-50%);  /*自身高度一半,这里等同于margin-top:-25px;*/
    height: 50px;
}

/*优缺点
- 优点：使用margin-top兼容性好；不管是块级还是行内元素都可以实现
- 缺点：代码较多；脱离文档流；使用margin-top需要知道高度值；使用transform兼容性不好（ie9+）*/

或

/*原理：当top、bottom为0时,margin-top&bottom会无限延伸占满空间并且平分*/
#parent{position: relative;}
#son{
    position: absolute;
    margin: auto 0;
    top: 0;
    bottom: 0;
    height: 50px;
}
```
(5)任意个元素
```
#parent{
    display: flex;
    align-items: center;
}

或

#parent{
    display: flex;
}
.son{
    align-self: center;
}

或 

#parent{
    display: flex;
    flex-direction: column;
    justify-content: center;
}
```
**本章小结**：
- 对于垂直居中，最先想到的应该就是 line-height 了，但是这个只能用于行内内容；
- 其次就是考虑能不能用vertical-align: middle; ，不过这个一定要熟知原理才能用得顺手，建议看下vertical-align和line-height的基友关系 ；
- 然后便是绝对定位，虽然代码多了点，但是胜在适用于不同情况；
- 移动端兼容性允许的情况下能用flex就用flex

# 三、水平垂直居中
(1)行内/行内块级元素/图片
```
#parent{
    height: 150px;
    line-height: 150px;  /*行高的值与height相等*/
    text-align: center;
    font-size: 0;   /*消除幽灵空白节点的bug*/
}
#son{
    /*display: inline-block;*/  /*如果是块级元素需改为行内或行内块级才生效*/
    vertical-align: middle;
}
```
(2)table-cell
```
#parent{
    height: 150px;
    width: 200px;
    display: table-cell;
    vertical-align: middle;
    /*text-align: center;*/   /*如果是行内元素就添加这个*/
}
#son{
    /*margin: 0 auto;*/    /*如果是块级元素就添加这个*/
    width: 100px;
    height: 50px;
}
```
(3)button作为父元素
```
button#parent{  /*改掉button默认样式就好了,不需要居中处理*/
    height: 150px;
    width: 200px;
    outline: none;  
    border: none;
}
#son{
    display: inline-block; /*button自带text-align: center,改为行内水平居中生效*/
}
```
(4)绝对定位
```
#parent{
    position: relative;
}
#son{
    position: absolute;
    top: 50%;
    left: 50%;
    /*定宽高时等同于margin-left:负自身宽度一半;margin-top:负自身高度一半;*/
    transform: translate(-50%,-50%); 
}
```
(5)绝对居中
```
#parent{
    position: relative;
}
#son{
    position: absolute;
    margin: auto;
    width: 100px;
    height: 50px;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
}
```
(6)flex
(7)视窗居中
```
#son{
	/*0如果去掉，则会多出滚动条并且上下都是50vh的margin。如果去掉就给body加上overflow:hidden;*/
    margin: 50vh auto 0;  
    transform: translateY(-50%);
}
```
**本章小结：**

- 一般情况下，水平垂直居中，我们最常用的就是绝对定位加负边距了，缺点就是需要知道宽高，使用transform倒是可以不需要，但是兼容性不好（ie9+）；
- 其次就是绝对居中，绝对定位设置top、left、right、bottom为0，然后margin:auto; 让浏览器自动平分边距以达到水平垂直居中的目的；
- 如果是行内/行内块级/图片这些内容，可以优先考虑line-height和vertical-align 结合使用，不要忘了还有text-align ，这个方法代码其实不多，就是理解原理有点困难，想要熟练应对各种情况还需好好研究；
- 移动端兼容性允许的情况下能用flex就用flex。

# 四、两列布局

**4.1 左列定宽，右列自适应**

(1) float + margin

html:
```
<body>
<div id="left">左列定宽</div>
<div id="right">右列自适应</div>
</body>
```
css:
```
#left {
    background-color: #f00;
    float: left;
    width: 100px;
    height: 500px;
}
#right {
    background-color: #0f0;
    height: 500px;
    margin-left: 100px; /*大于等于#left的宽度*/
}
```
(2) float + margin(fix)

html:
```
<body>
<div id="left">左列定宽</div>
<div id="right-fix">
    <div id="right">右列自适应</div>
</div>
</body>
```
css:
```
#left {
    background-color: #f00;
    float: left;
    width: 100px;
    height: 500px;
}
#right-fix {
    float: right;
    width: 100%;
    margin-left: -100px; /*正值大于或等于#left的宽度,才能显示在同一行*/
}
#right{
    margin-left: 100px; /*大于或等于#left的宽度*/
    background-color: #0f0;
    height: 500px;
}
```
(3) float + overflow

html:
```
<body>
<div id="left">左列定宽</div>
<div id="right">右列自适应</div>
</body>
```
css:
```
#left {
    background-color: #f00;
    float: left;
    width: 100px;
    height: 500px;
}
#right {
    background-color: #0f0;
    height: 500px;
    overflow: hidden; /*触发bfc达到自适应*/
}
```
(4) table

html:
```
<div id="parent">
    <div id="left">左列定宽</div>
    <div id="right">右列自适应</div>
</div>
```
css:
```
#parent{
    width: 100%;
    display: table;
    height: 500px;
}
#left {
    width: 100px;
    background-color: #f00;
}
#right {
    background-color: #0f0;
}
#left,#right{
    display: table-cell;  /*利用单元格自动分配宽度*/
}
```
(5) 绝对定位

html:
```
<body>
<div id="parent">
    <div id="left">左列定宽</div>
    <div id="right">右列自适应</div>
</div>
</body>
```
css:
```
#parent{
    position: relative;  /*子绝父相*/
}
#left {
    position: absolute;
    top: 0;
    left: 0;
    background-color: #f00;
    width: 100px;
    height: 500px;
}
#right {
    position: absolute;
    top: 0;
    left: 100px;  /*值大于等于#left的宽度*/
    right: 0;
    background-color: #0f0;
    height: 500px;
}
```
(6) flex

html:
```
<body>
<div id="parent">
    <div id="left">左列定宽</div>
    <div id="right">右列自适应</div>
</div>
</body>
```
css:
```
#parent{
    width: 100%;
    height: 500px;
    display: flex;
}
#left {
    width: 100px;
    background-color: #f00;
}
#right {
    flex: 1; /*均分了父元素剩余空间*/
    background-color: #0f0;
}
```
(7) Grid

html:
```
<body>
<div id="parent">
    <div id="left">左列定宽</div>
    <div id="right">右列自适应</div>
</div>
</body>
```
css:
```
#parent {
    width: 100%;
    height: 500px;
    display: grid;
    grid-template-columns: 100px auto;  /*设定2列就ok了,auto换成1fr也行*/
}
#left {
    background-color: #f00;
}
#right {
    background-color: #0f0;
}
```

**4.2 左列自适应，右列定宽**

(1) float + margin

html:
```
<body>
<div id="parent">
    <div id="left">左列自适应</div>
    <div id="right">右列定宽</div>
</div>
</body>
```
css:
```
#parent{
    height: 500px;
    padding-left: 100px;  /*抵消#left的margin-left以达到#parent水平居中*/
}
#left {
    width: 100%;
    height: 500px;
    float: left;
    margin-left: -100px; /*正值等于#right的宽度*/
    background-color: #f00;
}
#right {
    height: 500px;
    width: 100px;
    float: right;
    background-color: #0f0;
}
```
(2) float + overflow - BFC

html:
```
<body>
<div id="parent">
    <div id="right">右列定宽</div>
    <div id="left">左列自适应</div>   <!--顺序要换一下-->
</div>
</body>
```
css:
```
#left {
    overflow: hidden;  /*触发bfc*/
    height: 500px;
    background-color: #f00;
}
#right {
    margin-left: 10px;  /*margin需要定义在#right中*/
    float: right;
    width: 100px;
    height: 500px;
    background-color: #0f0;
}
```
(3) table

html:
```
<body>
<div id="parent">
    <div id="left">左列自适应</div>
    <div id="right">右列定宽</div>
</div>
</body>
```
css:
```
#parent{
    width: 100%;
    height: 500px;
    display: table;
}
#left {
    background-color: #f00;
    display: table-cell;
}
#right {
    width: 100px;
    background-color: #0f0;
    display: table-cell;
}
```
(4) 绝对定位

html:
```
<body>
<div id="parent">
    <div id="left">左列自适应</div>
    <div id="right">右列定宽</div>
</div>
</body>
```
```
#parent{
    position: relative;  /*子绝父相*/
}
#left {
    position: absolute;
    top: 0;
    left: 0;
    right: 100px;  /*大于等于#rigth的宽度*/
    background-color: #f00;
    height: 500px;
}
#right {
    position: absolute;
    top: 0;
    right: 0;
    background-color: #0f0;
    width: 100px;
    height: 500px;
}
```

(5) flex

html:
```
<body>
<div id="parent">
    <div id="left">左列自适应</div>
    <div id="right">右列定宽</div>
</div>
</body>
```
```
#parent{
    height: 500px;
    display: flex;
}
#left {
    flex: 1;
    background-color: #f00;
}
#right {
    width: 100px;
    background-color: #0f0;
}
```

(6) Grid

html:
```
<body>
<div id="parent">
    <div id="left">左列自适应</div>
    <div id="right">右列定宽</div>
</div>
</body>
```
```
#parent {
    height: 500px;
    display: grid;
    grid-template-columns: auto 100px;  /*设定2列,auto换成1fr也行*/
}
#left {
    background-color: #f00;
}
#right {
    background-color: #0f0;
}
```
**4.3 一列不定，一列自适应**

(盒子宽度随着内容增加或减少发生变化,另一个盒子自适应)
![(盒子宽度随着内容增加或减少发生变化,另一个盒子自适应)](https://user-gold-cdn.xitu.io/2018/3/9/1620a136d19c5afc?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

(1) float + overflow

html:
```
<body>
<div id="parent">
    <div id="left">左列不定宽</div>
    <div id="right">右列自适应</div>
</div>
</body>
```
```
#left {
    margin-right: 10px;
    float: left;  /*只设置浮动,不设宽度*/
    height: 500px;
    background-color: #f00;
}
#right {
    overflow: hidden;  /*触发bfc*/
    height: 500px;
    background-color: #0f0;
}
```

(2) flex

```
#parent{
    display: flex;
}
#left { /*不设宽度*/
    margin-right: 10px;
    height: 500px;
    background-color: #f00;
}
#right {
    height: 500px;
    background-color: #0f0;
    flex: 1;  /*均分#parent剩余的部分*/
}
```
(3) Grid

html:
```
#parent{
    display: grid;
    grid-template-columns: auto 1fr;  /*auto和1fr换一下顺序就是左列自适应,右列不定宽了*/
}
#left {
    margin-right: 10px;
    height: 500px;
    background-color: #f00;
}
#right {
    height: 500px;
    background-color: #0f0;
}
```
# 五、三列布局
**5.1 两列定宽，一列自适应**

![效果图](https://user-gold-cdn.xitu.io/2018/3/9/1620a136d1ea53c5?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

(1) float + margin

html:
```
<body>
<div id="parent">
    <div id="left">左列定宽</div>
    <div id="center">中间定宽</div>
    <div id="right">右列自适应</div>
</div>
</body>
```
css:
```
#parent{
    min-width: 310px; /*100+10+200,防止宽度不够,子元素换行*/
}
#left {
    margin-right: 10px;  /*#left和#center间隔*/
    float: left;
    width: 100px;
    height: 500px;
    background-color: #f00;
}
#center{
    float: left;
    width: 200px;
    height: 500px;
    background-color: #eeff2b;
}
#right {
    margin-left: 320px;  /*等于#left和#center的宽度之和加上间隔,多出来的就是#right和#center的间隔*/
    height: 500px;
    background-color: #0f0;
}
```
(2)float + overflow BFC

css:
```
#parent{
    min-width: 320px; /*100+10+200+20,防止宽度不够,子元素换行*/
}
#left {
    margin-right: 10px; /*间隔*/
    float: left;
    width: 100px;
    height: 500px;
    background-color: #f00;
}
#center{
    margin-right: 10px; /*在此定义和#right的间隔*/
    float: left;
    width: 200px;
    height: 500px;
    background-color: #eeff2b;
}
#right {
    overflow: hidden;  /*触发bfc*/
    height: 500px;
    background-color: #0f0;
}
```
(3) table:
```
#parent {
    width: 100%; 
    height: 520px; /*抵消上下间距10*2的高度影响*/
    margin: -10px 0;  /*抵消上下边间距10的位置影响*/
    display: table;
    /*左右两边间距大了一点,子元素改用padding设置盒子间距就没有这个问题*/
    border-spacing: 10px;  /*关键!!!设置间距*/
}
#left {
    display: table-cell;
    width: 100px;
    background-color: #f00;
}
#center {
    display: table-cell;
    width: 200px;
    background-color: #eeff2b;
}
#right {
    display: table-cell;
    background-color: #0f0;
}
```
(4) flex
```
#parent {
    height: 500px;
    display: flex;
}
#left {
    margin-right: 10px;  /*间距*/
    width: 100px;
    background-color: #f00;
}
#center {
    margin-right: 10px;  /*间距*/
    width: 200px;
    background-color: #eeff2b;
}
#right {
    flex: 1;  /*均分#parent剩余的部分达到自适应*/
    background-color: #0f0;
}
```
(5) Grid
```
#parent {
    height: 500px;
    display: grid;
    grid-template-columns: 100px 200px auto; /*设置3列,固定第一第二列的宽度,第三列auto或者1fr*/
}
#left {
    margin-right: 10px;  /*间距*/
    background-color: #f00;
}
#center {
    margin-right: 10px;  /*间距*/
    background-color: #eeff2b;
}
#right {
    background-color: #0f0;
}
```

**5.2 两侧定宽，中间自适应**

***5.2.1 双飞翼布局方法***

![双飞翼](https://user-gold-cdn.xitu.io/2018/3/9/1620a136d1cc24f8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

html:
```
<body>
<div id="header"></div>
<!--中间栏需要放在前面-->
<div id="parent">
    <div id="center">
        <div id="center_inbox">中间自适应</div>
        <hr>  <!--方便观察原理-->
    </div>
    <div id="left">左列定宽</div>
    <div id="right">右列定宽</div>
</div>
<div id="footer"></div>
</body>
```
css:
```
#header {
    height: 60px;
    background-color: #ccc;
}
#left {
    float: left;
    width: 100px;
    height: 500px;
    margin-left: -100%; /*调整#left的位置,值等于自身宽度*/
    background-color: #f00;
    opacity: 0.5;
}
#center {
    height: 500px;
    float: left;
    width: 100%;
    background-color: #eeff2b;
}
#center_inbox{
    height: 480px;
    border: 1px solid #000;
    margin: 0 220px 0 120px;  /*关键!!!左右边界等于左右盒子的宽度,多出来的为盒子间隔*/
}
#right {
    float: left;
    width: 200px;
    height: 500px;
    margin-left: -200px;  /*使right到指定的位置,值等于自身宽度*/
    background-color: #0f0;
    opacity: 0.5;
}
#footer {
    clear: both;  /*注意清除浮动!!*/
    height: 60px;
    background-color: #ccc;
}
```

双飞翼布局和圣杯布局很类似，不过是在middle的div里又插入一个div，通过调整内部div的margin值，实现中间栏自适应，内容写到内部div中。
这样可以先做好主体部分，然后再将附属部分放到合适的位置！

1. 首先把left、middle、right都放出来, middle中增加inner
2. 给它们三个设置上float: left, 脱离文档流；
3. 一定记得给container设置上overflow: hidden; 可以形成BFC撑开文档
4. left、right设置上各自的宽度
5. middle设置width: 100%;

***接下来与圣杯布局不一样的地方：***

6. left设置 margin-left: -100%, right设置 right: -rightWidth;
7. container设置padding: 0, rightWidth, 0, leftWidth;

https://www.jianshu.com/p/f9bcddb0e8b4



总结：

圣杯布局在DOM结构上显得更加直观和自然；
双飞翼布局省去了很多css，而且由于不用使用定位，可以获得比圣杯布局更小最小宽度；
说到这里需要注意一下  由于双飞翼布局会一直随着浏览器可视区域宽度减小从而不断挤压中间部分宽度。
所以需要设置给页面一个
```
min-width > LeftWidth + RightWidth；
```
还有一件事就是他们在单独部分内容扩充的时候，童鞋们可能发现了 底部会参差不齐。
在我的老师那里知道了最简单的解决办法 / 笑哭

给left、middle、right设置上 
```
padding-bottom: 9999px; margin-bottom: -9999px;
```

***5.2.2 圣杯布局方法***

html:
```
<body>
<div id="header"></div>
<div id="parent">
    <!--#center需要放在前面-->
    <div id="center">中间自适应
        <hr>
    </div>
    <div id="left">左列定宽</div>
    <div id="right">右列定宽</div>
</div>
<div id="footer"></div>
</body>
```
css:
```
#header{
    height: 60px;
    background-color: #ccc;
}
#parent {
    box-sizing: border-box;
    height: 500px;
    padding: 0 215px 0 115px;  /*为了使#center摆正,左右padding分别等于左右盒子的宽,可以结合左右盒子相对定位的left调整间距*/
}
#left {
    margin-left: -100%;  /*使#left上去一行*/
    position: relative;
    left: -115px;  /*相对定位调整#left的位置,正值大于或等于自身宽度*/
    float: left;
    width: 100px;
    height: 500px;
    background-color: #f00;
    opacity: 0.5;
}
#center {
    float: left;
    width: 100%;  /*由于#parent的padding,达到自适应的目的*/
    height: 500px;
    box-sizing: border-box;
    border: 1px solid #000;
    background-color: #eeff2b;
}
#right {
    position: relative;
    left: 215px; /*相对定位调整#right的位置,大于或等于自身宽度*/
    width: 200px;
    height: 500px;
    margin-left: -200px;  /*使#right上去一行*/
    float: left;
    background-color: #0f0;
    opacity: 0.5;
}
#footer{
    height: 60px;
    background-color: #ccc;
}
```

(3) grid

html:
```
<body>
<div id="parent">
    <div id="header"></div>
    <!--#center需要放在前面-->
    <div id="center">中间自适应
        <hr>
    </div>
    <div id="left">左列定宽</div>
    <div id="right">右列定宽</div>
    <div id="footer"></div>
</div>
</body>
```
css:
```
#parent {
    height: 500px;
    display: grid;
    grid-template-columns: 100px auto 200px; /*设定3列*/
    grid-template-rows: 60px auto 60px; /*设定3行*/
    /*设置网格区域分布*/
    grid-template-areas: 
        "header header header" 
        "leftside main rightside" 
        "footer footer footer";
}
#header {
    grid-area: header; /*指定在哪个网格区域*/
    background-color: #ccc;
}
#left {
    grid-area: leftside;
    background-color: #f00;
    opacity: 0.5;
}
#center {
    grid-area: main; /*指定在哪个网格区域*/
    margin: 0 15px; /*设置间隔*/
    border: 1px solid #000;
    background-color: #eeff2b;
}
#right {
    grid-area: rightside; /*指定在哪个网格区域*/
    background-color: #0f0;
    opacity: 0.5;
}
#footer {
    grid-area: footer; /*指定在哪个网格区域*/
    background-color: #ccc;
}
```
(4) 其他方法：table, flex, position

# 六、多列布局

**6.1 等宽布局**

6.1.1 四列/多列等宽

float table grid flex
 
**6.2 九宫格**

**6.3 栅格系统**

# 七、全局布局

![](https://user-gold-cdn.xitu.io/2018/3/9/1620a13716f2d8c3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

grid/flex/position


