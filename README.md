question
========

通常我们遇到一些奇怪的图形或者为了省事，就会直接把整张图切下来然后放到页面中。可是这样不但减慢了页面的加载速度，同时也对服务器造成了很大的压力，图片可比文字的请求大的多了。

如果页面全部用图片代替，还需要我们前端工程师干嘛？

这个项目里就是用代码实现了简单的效果（如下图）：  
![image](https://github.com/wenzi0github/question/raw/master/img/s.png)  

从图片里我们能够将一个问答分成两部分：问题部分和回答部分。问题部分在这里我设定成了一张背景图片，当然我们可以分成三部分，左半部分，中部分和右半部分，不过由于我们所有的问题都在有限的范围内，因此这里我就设定了一张图片；不过回答部分的背景图片，我还真的分成了三部分，上半部分，中间的内容部分和底部部分，中间的部分是不定高的，根据内容来进行背景图片的重复：background-repeat:repeat-y。  

在这里我们还能学到一个小技巧，一般我们使用浮动后需要再额外使用一个元素，来清除浮动：
```html
<div style="clear:both;"></div>
```
可是这样我们会额外的使用一些对页面无用的元素，那我们能不能在不添加额外元素的情况下清除浮动呢。这里我们用到了伪元素after，不过伪元素after只有IE8及以上的浏览器才能支持，低版本的浏览器是不支持的。

我们看下面的代码：
```css
.main{border:1px solid #00f;}
.main div{width:100px; height:200px; border:1px solid #ccc;}
.fl{float:left;}
.fr{float:right;}
```
```html
<div class="main">
  <div class="fl"></div>
  <div class="fr"></div>
</div>
```

.fl和.fr都是浮动元素，由于元素的浮动导致.main容器没有被撑开，高度为0。这里我们使用伪元素after来清除浮动：
```css
.main:after{content: "\00A0";display: block;visibility: hidden;width: 0;height: 0;clear: both;font-size: 0;line-height: 0;overflow: hidden;}
```

添加了上面的代码后我们就能看到.main容器被撑开了，也是清除了浮动。

当然，我们为了after清除浮动的通用性，我们可以单独使用一个类，为这个类使用伪元素，当哪些元素需要清除浮动时，只需要添加这个类名就可以了。
```css
.clearfix:after{content: "\00A0";display: block;visibility: hidden;width: 0;height: 0;clear: both;font-size: 0;line-height: 0;overflow: hidden;}
```
```html
<div class="main clearfix">
  <div class="fl"></div>
  <div class="fr"></div>
</div>
```
