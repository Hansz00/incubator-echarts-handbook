# 项目结构说明

（本文档正在完善中）

## 新增一个 markdown 文件

在 `contents/zh/`（中文文章）或 `contents/en/`（英文文章）目录下新增一个 markdown 文件，最多支持三级目录。将路径及标题信息更新在 `contents/zh/posts.js` 或 `contents/en/posts.js`。

markdown 文件名称小写，用 `-` 分割单词。

## 引用代码的方式

（尚未支持可运行实例的引入）

```js
option = {
    xAxis: {
        data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
    },
    yAxis: {},
    series: [{
        type: 'bar',
        data: [23, 24, 18, 25, 27, 28, 25]
    }]
};
```

## 引用图片的方式

图片实际存放地址在 `static/images/` 下。

![图片说明](${rootPath}/images/demo.png)

## CSS 定制

对于当前页面的临时样式，可以直接写 html：

<img src="${rootPath}/images/demo.png" style="width: 50px" />

对于多个页面可以共享的样式，修改相关的 `.vue` 文件。
