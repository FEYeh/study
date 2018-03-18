# 前端面试题


## HTML
### level 1
1 doctype是做什么的?
> `<!DOCTYPE html>`告诉浏览器使用什么样的文档类型定义来解析文档

2 如何实现具有多种语言的页面？
> i18n框架

3 data- 属性有什么好处
> 自定义的数据属性来是用做简单存储的一种好方法

4 HTML5带来了哪些新的特性
* 语义化的文本标记
* 新的表单元素
  * datalist：元素规定输入域的选项列表
  * keygen：验证用户的可靠方法
  * output：用于不同类型的输出
* 视频和音频
* 新的JavaScript API
  * 多媒体：Video、Audio
  * 动画和游戏：Canvas、Webgl
  * 存储：Local Storage、Sesson Storage、WebSQL、IndexedDB
  * 网络：Websocket
  * 定位：Geolocation
* SVG
每一项都可以再继续深入学习

5 描述一下Cookie、Local Storage以及Sesson Storage的区别
> 前端保存数据的方式有这么几种
* HTML5 web storage
  * Local Storage
  * Session storage
  * WebSQL：使用sql查询的关系型数据库
  * IndexedDB：一种nosql数据库
* Cookie
> sessionStorage和localStorage是web storage的两种储存方式,其中sessionStorage是会话级别储存,在浏览器或页面关闭时数据就会销毁,而localStorage是持久化的本地储存,不刻意去删除数据,数据是不会销毁的。以上这两种方式只是客户端的储存,不会涉及到服务器储存。与之相比,每次发送HTTP请求时会将cookie添加到Cookie头字段,发送给服务器。

> 在储存量方面也有差异,单个cookie保存的数据不能超过4K,而localStorage和sessionStorage一般有5-10M。

> 除此之外,每个域名下cookie的个数会有限制,依据浏览器不同会有不同,而localStorage数量是无限制的。

> WebSQL 和 IndexedDB 也是持久化的本地存储，更倾向于存储数据量稍大的数据。IndexedDB更像是一个NoSQL数据库，而WebSQL更像是关系型数据库，使用SQL查询数据。W3C已经不再支持这种技术



6 描述一下`<script>`，`<script async>` 和 `<script defer>` 的区别
> `<script>`加载js文件会阻塞页面的渲染和交互,而`<script async>`和`<script defer>`都是异步加载js文件,期间不会才生阻塞,区别在于`<script async>`是加载完之后自动执行,`<script defer>`需要等到页面加载之后再执行。

7 为什么把CSS`<link>`标签放在`<head></head>`之间，而把JS放在`</body>`之前？有什么特例吗？
> 浏览器在处理HTML页面渲染和JavaScript脚本执行的时候是单一进程的,所以在当浏览器在渲染HTML遇到了`<script>`标签会先去执行标签内的代码(如果是使用src属性加载的外链文件,则先下载再执行),在这个过程中,页面渲染和交互都会被阻塞。所以将`<script>`放在`</body>`之前,当页面渲染完成再去执行`<script>`。

> 一般希望DOM还没加载必须需要先加载的js会放置在`<head>`中,有些加
了defer、async的`<script>`也会放在`<head>`中。

8 渐进增强 (progressive enhancement) 和优雅降级 (graceful degradation) 的区别
* 渐进增强: 先保证低版本浏览器的基本功能,再去兼容高版本浏览器效果和交互。
* 优雅降级: 先保证高版本浏览器的效果和交互等,再去兼容低版本的浏览器。

9 为什么在img标签上添加srcset属性，浏览器是怎么计算该属性的
> 使用srcset可以实现响应式图片

> srcset属性值的格式：`path-to-another-image 设备最小尺寸 素密度显示的能力, path-to-another-image 设备最小尺寸 素密度显示的能力, ...`

* `path-to-another-image`当符合下述条件时就使用该图片  
* 依据`media queries`要求，设备最小尺寸为`600w`和`200h`
* 浏览器有以2x像素密度显示的能力  

