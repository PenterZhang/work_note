### 工作日常笔记：

`0.1 框架兼容与百分比：通过使用不同的框架来使PC和移动端兼容发现不管使用哪款框架，都无法完美兼容PC和移动端。比如：`
<br>
>PC端呈现出的是三个div并排的，但是到移动端以后就会发现，要么是向下排列了，要么就是变形了，总之是无法完美兼容的。
>
<br>

`0.2   垂直水平居中的九种方法：`
```
	（1）通过margin 0 auto； text-algin：center；实现css水平居中

	（2）通过display：flex；实现水平居中：父元素为display：flex；flex-direction：column；子元素为align-self：center；

	（3）通过display：table-cell 和 margin-left实现：父元素为display:table-cell；子元素为margin-left(父元素的一半);

	（4） 通过position：absolute 实现css居中：父元素为position：absolute;子元素为：margin-left；

	（5） 通过width：fit-content实现：给该元素属性width：fit-content； margin： 0 auto； text-algin：center；

	（6）通过display：inline-block 和text-algin:center实现： 父元素为display：inline-block；子元素给text-algin:center； margin： 0 auto；

	（7） 通过position：relative、float：left和margin-left实现： 给父元素position：relative，子元素为float：left和margin-left属性；
```
##### 剩下两条详情见[百度百科CSS的九种居中方法](http://jingyan.baidu.com/article/86112f1381081127379787bb.html?allowHTTP=1)

**垂直水平居中最好用margin0 auto 和绝对定位来解决！方碧昂快捷~哈哈哈哈**