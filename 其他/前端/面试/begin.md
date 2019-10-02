#### 记录一些有价值的面试题
* DOMContentLoaded 与onload
	* 当 onload 事件触发时，页面上所有的DOM，样式表，脚本，图片，flash都已经加载完成了
	* 当 DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash 

* 浏览器渲染
	* css加载不会阻塞DOM树的解析
	* css加载会阻塞DOM树的渲染
	* css加载会阻塞后面js语句的执行 
	* 当浏览器遇到一个 script 标记时，DOM 构建将暂停，直至脚本完成执行
	* JavaScript 可以查询和修改 DOM 与 CSSOM
	* CSSOM 构建时，JavaScript 执行将暂停，直至 CSSOM 就绪
	* 渲染树（Render-Tree）的关键渲染路径中，要求同时具有 DOM 和 CSSOM，之后才会构建渲染树


![enter description here](https://img.wsmpage.cn/learning/2019-10-2/1569982440366.png) 
* script defer async
	* defer 和 async 在网络读取（下载）这块儿是一样的，都是异步的（相较于 HTML 解析）
	* defer 是最接近我们对于应用脚本加载和执行的要求的


* 减少reflow
	* 实现元素的动画，它的position属性，最好是设为absoulte或fixed，这样不会影响其他元素的布局，还可以让动画处于更高的图层（即：z-index的值更大）这也是从图层的角度进行优化的。
	* 动画实现的速度的选择。比如实现一个动画，以1个像素为单位移动这样最平滑，但是reflow就会过于频繁，大量消耗CPU资源，如果以3个像素为单位移动则会好很多。
	* 不要使用table布局，因为table中某个元素旦触发了reflow，那么整个table的元素都会触发reflow。那么在不得已使用table的场合，可以设置table-layout:auto;或者是table-layout:fixed这样可以让table一行一行的渲染，这种做法也是为了限制reflow的影响范围


