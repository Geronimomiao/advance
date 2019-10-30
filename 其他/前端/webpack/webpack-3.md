---
title: webpack-3
time:  2019-10-27
author: wsm
mail: 1030057982@qq.com
---

==source map==
> JavaScript脚本正变得越来越复杂。大部分源码（尤其是各种函数库和框架）都要经过转换，才能投入生产环境
> Source map就是一个信息文件，里面储存着位置信息。也就是说，转换后的代码的每一个位置，所对应的转换前的位置
> 解决开发代码 和生产代码不一致问题

```
// 在 webpack 配置文件添加
 devtool: "source-map"
```


