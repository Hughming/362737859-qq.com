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
----
**本章小结**：
<font face="黑体" color="DarkCyan">
- 对于水平居中，我们应该先考虑，哪些元素有自带的居中效果，最先想到的应该就是 text-align:center 了，但是这个只对行内内容有效，所以我们要使用 text-align:center 就必须将子元素设置为 display: inline; 或者 display: inline-block; ；
- 其次就是考虑能不能用margin: 0 auto; ，因为这都是一两句代码能搞定的事，实在不行就是用绝对定位去实现了。
- 移动端能用flex就用flex，简单方便，灵活并且功能强大，无愧为网页布局的一大利器！
</font>
----