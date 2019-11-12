---
title: 点击图片放大
date: 2019-09-09 11:17:56
tags:
highlight_copy: true
cover: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=1551958397,2774203265&fm=26&gp=0.jpg
---
点击图片让图片放大 图片是动态渲染出来的

## jQuery点击图片让图片放大

### html部分

``` html部分(只有body内)
<div class="hide dn">
    <div>x</div>
    <img src="" alt="">
</div>
```

### css部分

``` css部分
* {
    margin: 0;
    padding: 0;
}
.hide {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 100;
}
.hide img {
    position: absolute;
    width: 100px;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
}
.hide div {
    position: absolute;
    right: 15px;
    top: 0;
    font-size: 30px;
    color: #ccc;
    cursor: pointer;
}
img {
    width: 100px;
    float: left;
}
.dn {
    display: none;
}
.oh {
    overflow-y: hidden;
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
                var data = response.data
                for (var i in data) {
                    var str = '';
                    var cdn_img = data[i].cdn_img
                    str += '<img src="' + cdn_img + '" alt="" data-src="' + cdn_img + '">'
                    $('body').append(str)
                }
            }
        }
    });
})
$(document).on('click','img', function () {
    $('body').addClass('oh')
    $('.hide').show()
    var url = $(this).attr('data-src')
    $('.hide img').attr('src', url)
    $('.hide').bind('mousewheel', function (e) {
        var delta = (e.originalEvent.wheelDelta && (e.originalEvent.wheelDelta > 0 ? 1 :-1)) ||
            // chrome & ie
            (e.originalEvent.detail && (e.originalEvent.detail > 0 ? -1 : 1)); // firefox
        var wid = $('.hide img').width();
        if (delta > 0) {
            $('.hide img').stop().animate({
                'width': wid + 100
            },300)
        } else if (delta < 0) {
            $('.hide img').stop().animate({
                'width': wid - 100
            },300)
        }
    })
})
$('.hide div').on('click',function () {
    $('body').removeClass('oh')
    $('.hide').hide()
})
```

## 效果图(鼠标滚动放大缩小)
![](/img/imgmax.gif)
# 此代码需要jq2.2.0以上版本才可以运行
  