---
title: 用Inspect功能修正hexo排版错误

categories:
- 编程

tags:
- hexo
- markdown
- debug
---

前两周参考[笑来老师文章](http://lixiaolai.com/2016/06/22/makecs-build-a-blog-with-hexo-on-github/)用hexo建了一个静态博客站点，准备正式开始练习写作（顺便说一下笑来老师的这个博客有很多学习编程的心得、实用知识和技巧，非常值得看看）。

写作过程中发现hexo中对markdown语法的支持有些问题。例如使用引用语法的时候，在atom里模拟显示正常：

![Markdown Debug 1](https://i.imgur.com/3gYkIOE.jpg)

但在浏览器里却显示有问题：

![Markdown Debug 2](https://i.imgur.com/u63KkyK.jpg)

反复试了多次都是同样的问题，正在一筹莫展时，同样是受笑来老师博客里的[一篇文章](http://lixiaolai.com/2016/06/25/makecs-html-css/)的启发最终解决了这个问题。

谷歌chrome浏览器的Inspect功能对于发现和修正html/css问题非常有效。以上面的问题为例：

1. 在网页的有问题位置按鼠标右键，在弹出菜单里选择Inspect；

![Markdown Debug 3](https://i.imgur.com/MTNKHmB.jpg)

2. 这时会弹出Inspect窗口。窗口左侧是网页的html文件内容，可以看到引用的部分是属于一个`blockquote`的class；

![Markdown Debug 4](https://i.imgur.com/FWUqnhE.jpg)

3. 用鼠标点击这个class或者在右边窗口中输入blockquote，可以看到对应的css文件；

![Markdown Debug 5](https://i.imgur.com/I41s74W.jpg)

4. 仔细看看这个文件就会发现这种格式显示的肯定不是引用的效果：
``` css
.article-entry blockquote {
    font-family: Georgia, "Times New Roman", serif;
    font-size: 1.4em;
    margin: 1.6em 20px;
    text-align: center;
}
```
5. 找一个能够正常显示引用的网页，同样用Inspect功能打开css文件，看看引用部分的css是怎么写的：

![Markdown Debug 6](https://i.imgur.com/KQAgPm6.jpg)

6. 把css文件内容拷贝下来，粘贴到自己有问题网页的对应css文件中，发现网页可以正确显示引用了（可以随便试试各种效果，试不坏的）：

![Markdown Debug 7](https://i.imgur.com/RaAxHlM.jpg)

7. 最后一步，在hexo所在文件夹里搜索blockquote（在atom里用'shift+command+F'快捷键搜索），css设置一般都在‘style.css’文件里，将对应的部分换成以下内容就行了：
``` css
.article-entry blockquote {
    padding: 0 15px;
    color: #666;
    border-left: 4px solid #ddd;
}
```

### 总结
* Inspect功能对于学习、发现和修正html/css问题非常方便、有效；
* 对于html/css/javascript还是缺乏系统了解，需要尽快补上。

### 问题
* 修改完后用手机浏览博客能够立刻正常显示，但在电脑上需要等一会儿才能显示正常，用‘localhost:4000’调试模式则一直不正常；
* 修改hexo文件后要反复存几次才能生效，否则即使存盘后也会变回原来的设置。

估计可能是hexo的问题，也可能是自己操作的原因，希望能尽快找到答案。
