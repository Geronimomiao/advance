---
title: webpack-2
time:  2019-10-22
author: wsm
mail: 1030057982@qq.com
---

==autoprefixer 自动补全 css3 前缀==
+- webpack.config.js 
```
{
	test: /\.less$/,
	use: [
          MiniCssExtactPlugin.loader,
		'css-loader',
		'less-loader',
		{
            loader: 'postcss-loader',
			options: {
            	plugins: () => [
            		require('autoprefixer')({})
				]
			}
          }
	]
},
```

+- package.json
```
"browserslist": [
    "last 2 version",
    "> 1%",
    "IOS 7"
 ]
```
[推荐链接](https://github.com/browserslist/browserslist#readme)


==静态资源内联==
* 意义
	* 页面框架初始脚本
	* 上报相关打点
	* css 内联避免页面闪动
	* 减少 http 请求数

```
// raw-loader 内联 html
	${require("raw-loader!./demo.inline.html").default}
	
// raw-loader 内联 css
 <style>
        ${require("raw-loader!./demo.inline.css").default}
  </style>
	
// raw-loader 内联 js
<script>
      ${require("raw-loader!babel-loader!../node_modules/lib-flexible").default}
 </script>
```


==px -> rem==
+- 依赖

```yarn add px2rem-loader lib-flexible```

+- webpack.config.js 
```
{
    loader: 'px2rem-loader',
	options: {
        // rem px 转换比例
        remUnit: 75,
		// 转换后小数点 保留位数
		remPrecision: 8
	}
}
```

==多页面应用打包==
+- 多页面应用(MPA)
每一次页面跳转时 后台服务器都会返回一个新的 html 文档 这种类型网站就是多页网站 也叫多页应用

 +-
 ```
 // 先约定好 入口文件都是 ./src 文件夹下 index.js
 module.exports = {
 	entry: {
		index: './src/index/index.js',
		search: './src/search/index.js'
	}
 }
 
 // yarn add glob
 // 动态获取文件名 将其拼入 htmlWebpackPlugins 数组中
 const setMPA = () => {
	const entry = {};
	const htmlWebpackPlugins = [];

	const entryFiles = glob.sync(path.join(__dirname, './src/*/index.js'));

	Object.keys(entryFiles).map(i => {
		const entryFile = entryFiles[i];
		const match = entryFile.match(/src\/(.*)\/index\.js/);
		const pageName = match && match[1];

		entry[pageName] = entryFile;
		htmlWebpackPlugins.push(
      		new HtmlWebpackPlugin({
        		template: path.join(__dirname, `src/${pageName}/index.html`),
        		// 打包输出文件名称
        		filename: `${pageName}.html`,
        		// 指定打包 需要 chunks
        		chunks: [pageName],
        		// 打包 完成 会将 css js 自动注入
        		inject: true,
        		minify: {
          			html5: true,
          			collapseWhitespace: true,
          			preserveLineBreaks: false,
          			minifyCSS: true,
          			minifyJS: true,
          			removeComments: false
        		}
      	}),
	);
	});

	return {
		entry,
		htmlWebpackPlugins
	}
};

const {entry, htmlWebpackPlugins } = setMPA();
 
 ```

****
+- tree shaking
一个模块有多个方法 tree shaking 只把用到的方法 打入 bundle 没有用到的方法会在 uglify 阶段被擦除掉
webpack 默认支持  production 默认开启

