---
title: jquery模拟实现删除，查询，全选，反选
date: 2019-09-06 10:00:04
tags:
cover: https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1567745585834&di=862a4bd311672c3c920e2661a53723f8&imgtype=0&src=http%3A%2F%2Fimg.365azw.com%2FAttachments%2Fshare%2F201703%2F58d48a40ef15d.jpg%2521article.w.p
highlight_copy: true
---
这是第二天 学习的代码 jquery模拟实现删除，查询，全选，反选

## jquery模拟实现删除，查询，全选，反选

### html部分
``` html部分(只有body内)
<h1>学员信息查询管理系统</h1>
条件：
<p><input id="txt_search" type="text" placeholder="搜索空为显示全部"> <input id="btn_search" type="button" value="查询姓名">
    <input type="button" id="del_btn" value="选择删除">
    </p><table id="tab" border="1">
        <tbody><tr id="sh">
            <th><input type="checkbox" id="selectAll">全选 <input type="checkbox" id="ReverseSelect">反选</th>
            <th>学号</th>
            <th>姓名</th>
            <th>性别</th>
            <th>年龄</th>
            <th>成绩</th>
            <th>班级</th>
        </tr>
        <tr>
            <td><input type="checkbox" class="xz"></td>
            <td>110</td>
            <td class="nm">小明</td>
            <td>男</td>
            <td>44</td>
            <td>100</td>
            <td>89班</td>
        </tr>
        <tr>
            <td><input type="checkbox" class="xz"></td>
            <td>110</td>
            <td class="nm">小红</td>
            <td>男</td>
            <td>44</td>
            <td>99</td>
            <td>89班</td>
        </tr>
        <tr>
            <td><input type="checkbox" class="xz"></td>
            <td>110</td>
            <td class="nm">小白</td>
            <td>男</td>
            <td>44</td>
            <td>98</td>
            <td>89班</td>
        </tr>
        <tr>
            <td><input type="checkbox" class="xz"></td>
            <td>110</td>
            <td class="nm">小王</td>
            <td>男</td>
            <td>44</td>
            <td>22</td>
            <td>89班</td>
        </tr>
    </tbody></table>
```

### css部分
``` css部分
#nul {
	margin-left:150px;
	display:none;
}
```

### js部分
``` js部分
$('#selectAll').on('click', function() {
    // $('#tab td input').attr('checked')
    var flage = $(this).is(":checked");
    if (flage) {
        $('#tab td input').prop("checked", true);
    } else {
        $('#tab td input').prop("checked", false);
    }
})
// 四个选中再全选
$('.xz').on('click', function() {
    if ($(".xz[type='checkbox']:checked").length == $('.xz').length) {
        $('#selectAll').prop("checked", true);
    } else {
        $('#selectAll').prop("checked", false);
    }
})
// 反选
$('#ReverseSelect').on('click', function() {
    $("#tab td :checkbox").each(function() {
        //遍历所有复选框，然后取值进行 !非操作
        $(this).prop("checked", !$(this).prop("checked"));
    })
    if ($(".xz[type='checkbox']:checked").length == $('.xz').length) {
        $('#selectAll').prop("checked", true);
    } else {
        $('#selectAll').prop("checked", false);
    }
})
// 搜索
$('#btn_search').on('click', function() {
    var tex = $('#txt_search').val()
    $('.nm').each(function() {
        if (tex == $(this).text()) {
            $(this).text(tex).parents('tr').show().siblings().hide();
            $('#nul').hide();
        } else {
            $(this).parents('tr').hide();
            // $('#nul').show();
        }
        if (tex == '') {
            $(this).parents('tr').show();
            $('#nul').hide();
        }
    })
    $('#sh').show()
})
// 删除
$('#del_btn').on('click', function() {
    $("#tab td :checkbox").each(function() {
        if ($(this).prop("checked") == true) {
            $(this).parents('tr').remove()
        }
    })
})
```

## 效果图(全选-反选-删除-搜索这些功能都可以使用 删除了就搜索不到了哦)
![](/img/tab.gif)
# 此代码需要jq2.2.0以上版本才可以运行