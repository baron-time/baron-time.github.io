---
title: 下拉加载更多支持pc和移动
date: 2019-09-06 16:02:46
tags:
highlight_copy: true
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=3965973857,1348575134&fm=26&gp=0.jpg
---
# 这个例子中使用了公共的接口 各位可以用这个接口 但是不可以恶意刷数据哦 恶意刷数据时间长了此接口会禁用的 好了话不多说 上菜~

## jQuery下拉加载更多 支持pc和移动

### html部分

``` html部分(只有body内)
因为有接口就结构都是动态渲染出来的 所以body以内没有结构标签 各位用的时候按自己的实际情况活用哦
```

### css部分

``` css部分
div {
    width: 300px;
    height: 200px;
    margin: 0 auto;
}
.dn {
    display: none;
}
div img {
    width: 100%;
    height: 100%;
}
#loading,
#over {
    width: 100%;
    height: 30px;
    background-color: pink;
    text-align: center;
}
```

### js部分

``` js部分
 $(document).ready(function () {
        $.ajax({
            type: "get",
            url: "https://www.apiopen.top/satinApi?type=1&page=1",
            dataType: 'json',
            success: function (response) {
                if (response.code == 200) {
                    console.log('%c第\t1\t次\t数\t据\t请\t求\t成\t功', 'color:red;font-size: 20px;');
                    var data = response.data
                    for (var i in data) {
                        var str = '';
                        var cdn_img = data[i].cdn_img
                        str += '<div><img src="' + cdn_img + '" alt=""></div>'
                        $('body').append(str)
                    }
                }
            }
        });
    })
    // 这是从第二页开始下拉更多
    var pager = 1;
    var stop = true;
    $(window).scroll(function () {
        if ($(this).scrollTop() + $(window).height() + 100 >= $(document).height() && $(this).scrollTop() +
            100) {
            if (stop == true) {
                stop = false;
                pager = pager + 1;
                $.ajax({
                    type: "get",
                    url: "https://www.apiopen.top/satinApi?type=1&page=" + pager,
                    dataType: 'json',
                    success: function (response) {
                        if (response.code == 200) {
                            console.log('%c第\t' + pager + '\t次\t数\t据\t请\t求\t成\t功','color:red;font-size: 20px;');
                            var data = response.data
                            for (var i in data) {
                                var str = '';
                                var cdn_img = data[i].cdn_img
                                str += '<div><img src="' + cdn_img + '" alt=""></div>'
                                $('body').append(str)
                                $('#loading').remove()
                            }
                            $('body').append('<div id="loading">加载中......</div>')
                            stop = true;
                        } else {
                            console.log('%c数\t据\t请\t求\t失\t败', 'color:red;font-size: 20px;');
                            $('body').append('<div id="over">淦！~没有数据</div>')
                        }
                    }
                });
            }
        }
    });
```

## 效果图
![](/img/bottom.gif)
如果有数据就会拉一下 出现一下加载中 然后出现下一组内容 如果没有数就显示没有数据 也可以f12控制台看
# 此代码需要jq2.2.0以上版本才可以运行