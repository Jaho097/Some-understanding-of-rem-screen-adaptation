
```js
 (function (doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function () {//重新换算rem方法
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;         
            docEl.style.fontSize = clientWidth / 19.2 + 'px';
            window.FONTSIZE = clientWidth / 19.2;
            setTimeout(function () {
                document.body.className = "mec-default mec-show";
            }, 100);
        };
    if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);//监听屏幕宽度
        doc.addEventListener('DOMContentLoaded', recalc, false);//当 HTML 文档被完全解析并且所有延迟脚本都已下载并执行时触发该事件
    })(document, window);
```
以上是适配的一个方案代码，其实重点就在于rem的转换，也就是

`docEl.style.fontSize = clientWidth / 19.2 + 'px';`



rem适配原理：监听屏幕变化进行fontsize换算，这里的19.2是我们自由设置的，我设置19.2的原因是比较好换算，因为设计稿给的是1920宽度，那么设置了19.2之后fontsize会等于100px，那么1rem就等于100px，以后1920设计稿需要我设置一个500px大小的元素，我只需要在代码中写5rem，7px的元素则写0.07rem即可满足。

`如果是移动端给的750px设计稿，那么建议把19.2改成7.5`，同理换算出1rem等于100px。


使用上面这段代码，设计师给出1920px的设计稿时，我们只需要按照
`(设计稿100px)=（代码1rem）`来给我们的样式进行设置，这样就能完成不同屏幕宽度适配的效果。


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4b0a010ac8b74cf7bba40b4801ff22ff~tplv-k3u1fbpfcp-watermark.image?)

下面以设计师给的1920设计稿为例子：

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/00833ce3546f493f83b64b91258c7c93~tplv-k3u1fbpfcp-watermark.image?)

由于设计稿给的是1920屏幕下的480px，我的屏幕是1440，在index中已经设置了以19.2为基准，我们只要设置宽度是4.8rem，所以1440屏幕下显示的宽度是360px，同理放大到1920就是480px。

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f2f2a8f9b3e349149c0e552e271be3d0~tplv-k3u1fbpfcp-watermark.image?)


![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe04b26a17f94863a342380792f3bfb0~tplv-k3u1fbpfcp-watermark.image?)


以上是个人整理的一些在日常开发中遇到的一些问题以及解决方案，如有错误请大家指正。
