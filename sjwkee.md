## 主页样式修改整理
#### nav内的ul列表中ul和a标签都没有高度，只有li有高度，怀疑样式不足：

*源码：*
```
{
    没有给a标签写display：block；float:left;/display:inline-block;
    源码只给了li标签宽高，代码如下：
        .nav_bg ul li {
            width: 69px;
            height: 52px;
            font-size: 15px;
            margin: 15px 13px 0 13px;
            line-height: 48px;
            text-align: center;
            float: left;
            color: white;
        }
------
}

```
**已修复**

<br/>

>给section下public的建议：

>>为什么总是给前面的的标签外边距来增加后面元素的距离？这个习惯不太好，容易导致样式爆炸，同时不易管理代码；

<br/>

#### 注意父元素的宽高：
>固定样式的话不会有什么影响；但是如果是兼容的话样式会炸；比如aside>ul就没有高度，一旦屏幕过于窄小的话样式就会炸，有可能里面的li竖向排列，也有可能吧article中的内容挤走，或者强制使屏幕溢出，使横向滚动条出现！
```
已修改完成，目前没有废弃代码；吧li的高度赋值给UL，LI不设置高度；因为内部有margin值，可以撑起；
源码：
    .electricity aside ul li {
        width: 143px;
        height:156px;
        margin-left: 48px;
        float: left;
    }
改后源码
    aside>ul{
        width: auto;
        height: 156px;
    }
    .electricity aside ul li {
        width: 143px;
        margin-left: 48px;
        float: left;
    }
```
<br/>

*刚刚才说的先写前面标签的样式在写后面的样式会炸，果然，#featureCarousel中的样式已经炸了，解析：*
```
源码：
    .advantage p {
        letter-spacing: 2px;
        margin: 30px auto 163px auto;
        text-align: center;
    }
    #featureCarousel {
        height: 300px;
        width:1100px;
        position:relative;
        margin: 163px auto -20px  auto;
        top: -66px;
    }
    修改后的源码：
    .advantage p {
	letter-spacing: 2px;
	margin: 30px auto 0px auto;
	text-align: center;
    }

    #featureCarousel {
        height: 300px;
        width:1100px;
        position:relative;
        margin: 143px auto 0px  auto;
        top: -66px;
    }
```
>在这里一定要注意写到哪里就写哪里的样式，不要着急；或者最起码要等到写到该样式的时候再去写/相互影响的样式。最好等到写到的时候再去写该标签的样式！
<br />

#### 并且 其中#featureCarousel中的a标签没有高度/严重不符合该图片的高度！在检测代码中#featureCarousel中的a标签只有21的高度！are you kidding me ?

**上源码！**
```
源码就是：a标签根本没写样式！
修改后的源码：

    #featureCarousel>div>a,.feature>a{
        display: block;
        width: auto;
        height:auto;
    }

```
#### 一个标签能搞定的事情不要用两个；
**源码展示**
```
HTML部分源码：	

        <div class="process_bg">
            <article>
                <span>
                    STEP1<br /><div>免费咨询</div>
                </span>
                <p>
                    您了解更多相关事宜，可拨打我们的免费咨询<br />电话，随时为您解答
                </p>
            </article>
            <aside>
            </aside>
        </div>


HTML部分修改后的源码:

        <div class="process_bg">
            <article>
                <span>
                    STEP1<br /><div>免费咨询</div>
                </span>
                <p>
                    您了解更多相关事宜，可拨打我们的免费咨询<br />电话，随时为您解答
                </p>
            </article>
        </div>


css部分源码:

    .process_bg aside {
        background: url(../img/dadiannao.png);
        width: 715px;
        height: 418px;
        float: right;
    }
    .process_bg article {
        width: 410px;
        height: 418px;
        float: left;
    }
    .process_bg article span {
	width: 380px;
	height: 70px;
	padding-left: 20px;
	margin: 100px auto 0 auto;
	display: block;
	font-size: 22px;
	color: white;
	padding-top: 10px;
	border-left: 2px solid white;
    }
    .process_bg article span>div {
        font-size: 28px;
    }
    .process_bg article>p {
        font-size: 18px;
        text-align: left;
        margin-top: 49px;
    }
    

CSS部分修改后的源码:

    .process_bg {
        width: 1138px;
        height: 420px;
        /*border: 1px solid red;*/
        margin: 48px auto 0 auto;
        background: url(../img/dadiannao.png) no-repeat right center;
    }
    .process_bg article {
        width: 410px;
        height: 418px;
        float: left;
    }
    .process_bg article span {
        width: 380px;
        height: 70px;
        padding-left: 20px;
        margin: 100px auto 0 auto;
        display: block;
        float:left;
        font-size: 22px;
        color: white;
        padding-top: 10px;
        border-left: 2px solid white;
    }
    .process_bg article span>div {
        font-size: 28px;
    }
    .process_bg article>p {
        font-size: 18px;
        text-align: left;
        margin-top: 49px;
    }


```

*以上方法节省很多时间和代码*

#### 永远不要忘记给标签宽高，footer中的ul就没有高度，看样子好像是打算用img来吧父级标签撑起来，但是支撑起来了ul的子元素，li标签的宽高，通过这里我们可以发现：

*子元素只能撑他的上一级父元素的宽高，不能撑起他的上上级父元素。所以，一旦有类似情况一定要给它的上上级父元素设置宽高！*

>代码展示：
```

修改前样式：

    .call ul li {
        float: left;
        color: white;
    }
    .call ul li ul {
        margin-left: 30px;
    }
    .call ul li ul li {
        font-size: 12px;
        line-height: 30px;
        clear: both;
        color: #717884;
    }

    修改后样式:

    .call>ul{
        width: 100%;
        height: 161px;
    }
    .call ul li {
        float: left;
        color: white;
    }
    .call ul li ul {
        margin-left: 30px;
    }
    .call ul li ul li {
        font-size: 12px;
        line-height: 30px;
        clear: both;
        color: #717884;
    }

```