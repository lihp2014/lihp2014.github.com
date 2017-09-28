title: input file框无法选择华为手机图片
tags: '移动Web'
categories: '前端'

---
### 前情提要
1. 项目中引用了github上一位道友贡献的图片上传插件[PhotoClip.js](https://github.com/baijunjie/PhotoClip.js)，移动端支持手势缩放，拖拽。非常好用。
2. 用一个图标icon盖住了input file框，点击icon，手动触发file框的click事件，然后再进行选择操作。
<!-- more -->

### Bug描述
在华为手机上微信中打开时，点击上传图片icon，打开文档，如下图：
![Alt HW截图](./images/752286147338753965_Ink_LI.jpg)
选择上图中1处图片文件夹下的图片时，所有图片蒙上了一层白板，无法进行选择操作。

### 解决问题
1. 在网上查找相关问题的解决方案，[这里](https://github.com/weui/weui/issues/388)给出了详细描述，于是我按照最后的方式给file框添加了accept="image/*"属性。
2. 添加该属性后，发现一个问题，html文档里file框的accept="image/*"属性被浏览器渲染成了accept="image/jpeg,image/x-png,image/gif"，这可能就是导致问题的原因。
3. 按照常理来说，浏览器是不会擅自修改html文档元素的属性的，一定是js某个地方对该属性进行了重写，于是仔细查找是哪个地方悄悄修改了file框的accept属性。
4. 对引用的插件挨个进行排查，在PhotoClip.js(前情提要中的第一点里的辣个)这个插件源码中发现了如下一行代码：
![Alt SourceCode截图](./images/20161122111602.jpg)
至于这里为何要重写accept属性，我还不是很清楚。。
5. 既然插件里重写了accept属性，一定有作者的用意，那我也不能修改源码。于是在自己的代码中，触发file框的click事件后，对其accept属性又写成了"image/*",如下：
![Alt 截图](./images/20161122112226.jpg)
6. 至此问题解决。
