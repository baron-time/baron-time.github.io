---
title: 用js实现rem
date: 2019-09-09 09:37:15
tags:
cover: https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=1919037390,2349900337&fm=26&gp=0.jpg
highlight_copy: true
---

### js部分

``` js部分
 /*计算rem高度*/
(function (win, doc) {
    win.onresize = function () {
        change();
    };
    change();

    function change() {
        var oFs = doc.documentElement.clientWidth / (750 / 100);
        doc.documentElement.style.fontSize = oFs + 'px';
        
    }
})(window, document);
```
这个是直接调用的公共js文件 没有效果图直接调用就行
## 使用后直接把这个js文件引成公共的 1rem = 100px  例如你需要 36px 那么就 36px = 0.36rem