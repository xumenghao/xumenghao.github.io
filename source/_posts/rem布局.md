---
title: 手机端页面自适应解决方案—rem布局进阶版
abbrlink: 4a17b202
tags: [rem布局,HTML5,前端]
categories: Web前端
---

好玩的rem布局

<!--  more -->


>  
>一年前笔者写了一篇 [《手机端页面自适应解决方案—rem布局》]("https://www.jianshu.com/p/b00cd3506782")，意外受到很多朋友的关注和喜欢。但随着时间的推移，该方案已然过时，故为大家介绍一个目前我极力推荐使用的，更加完美的方案——rem布局（进阶版）
>
**另外：**
>
>+ 此方案仅适用于移动端web
>+ 文章底部**常见问题说明第四条** ，笔者已给出一个相当便捷的解决方案，欢迎留言交流。（2018/3/23）

该方案使用相当简单，把下面这段已压缩过的 **原生JS**（仅1kb，源码已在文章底部更新） 放到 HTML 的 head 标签中即可（注:不要手动设置viewport，该方案自动帮你设置）


	<script>
	!function(e){function t(a){if(i[a])return i[a].exports;var n=i[a]={exports:{},id:a,loaded:!1};return e[a].call(n.exports,n,n.exports,t),n.loaded=!0,n.exports}var i={};return t.m=e,t.c=i,t.p="",t(0)}([function(e,t){"use strict";Object.defineProperty(t,"__esModule",{value:!0});var i=window;t["default"]=i.flex=function(normal,e,t){var a=e||100,n=t||1,r=i.document,o=navigator.userAgent,d=o.match(/Android[\S\s]+AppleWebkit\/(\d{3})/i),l=o.match(/U3\/((\d+|\.){5,})/i),c=l&&parseInt(l[1].split(".").join(""),10)>=80,p=navigator.appVersion.match(/(iphone|ipad|ipod)/gi),s=i.devicePixelRatio||1;p||d&&d[1]>534||c||(s=1);var u=normal?1:1/s,m=r.querySelector('meta[name="viewport"]');m||(m=r.createElement("meta"),m.setAttribute("name","viewport"),r.head.appendChild(m)),m.setAttribute("content","width=device-width,user-scalable=no,initial-scale="+u+",maximum-scale="+u+",minimum-scale="+u),r.documentElement.style.fontSize=normal?"50px": a/2*s*n+"px"},e.exports=t["default"]}]);  flex(false,100, 1);
	</script>

作者：_minooo_
链接：https://www.jianshu.com/p/985d26b40199
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


### 代码原理

这是阿里团队的高清方案布局代码，所谓高清方案就是利用rem的特性（我们知道默认情况下html的1rem = 16px），根据设备屏幕的DPR（设备像素比，又称DPPX，比如dpr=2时，表示1个CSS像素由4个物理像素点组成）**根据设备DPR调整页面的压缩比率（即：1/dpr），同时动态设置 html 的font-size为（50 * dpr)，进而达到高清效果**。

### 有何优势

+ 引用简单，布局简便
+ 根据设备屏幕的DPR,自动设置最合适的高清缩放。
+ 保证了不同设备下视觉体验的一致性。（老方案是，屏幕越大元素越大；此方案是，屏幕越大，看的越多）
+ 有效解决移动端真实1px问题（这里的1px 是设备屏幕上的物理像素）


### 如何使用

重要的事情说三遍！
**绝不是每个地方都要用rem，rem只适用于固定尺寸**！
**绝不是每个地方都要用rem，rem只适用于固定尺寸**！
**绝不是每个地方都要用rem，rem只适用于固定尺寸**！
在相当数量的布局情境中（比如底部导航元素平分屏幕宽，大尺寸元素），你必须使用百分比或者flex才能完美布局！

看过 ['《手机端页面自适应解决方案—rem布局》']("https://www.jianshu.com/p/b00cd3506782")的朋友，应该对rem有所了解，这里不再赘述，
**此方案也是默认 1rem = 100px，所以你布局的时候，完全可以按照设计师给你的效果图写各种尺寸啦**。
比如你在效果图上量取的某个按钮元素长 55px, 宽37px ，那你直接可以这样写样式：



	.myBtn {  
	   width: 0.55rem;  
	   height: 0.37rem;  
	}  



### 为了让朋友们更清晰感受此方案的巨大优势，下面是源码和Demo

[实践应用1（请在手机端或者手机模式下浏览效果更佳！）]("https://link.jianshu.com/?t=https%3A%2F%2Fminooo.github.io%2FDemo%2Freact-study-step-03-demo%2Findex.html")

[实践应用2（请在手机端或者手机模式下浏览效果更佳！）]("https://link.jianshu.com/?t=https%3A%2F%2Fminooo.github.io%2FDemo%2Freact-study-step-04-demo%2Findex.html")

[线上项目（请在手机端或者手机模式下浏览效果更佳！）]("http://m.jr.duduapp.net/")

[示例源码]("https://codepen.io/minooo/pen/WoQjKW?editors=1100")

### 常见问题说明，新手很有必要看一下（2018/3/23）

>`许多同学对该方案存在不少误解导致使用出现各种问题，这里统一回复下。`

**1.问：为啥手机网页效果图宽度是要640或者750的，我非得弄个666的不行咩？**

答：老实说当然可以，不过为了规范，640或者750是相对合适的。
拿Iphone 5s 举例，它的css像素宽度是320px，由于它的dpr=2，所以它的物理像素宽度为320 × 2 = 640px，这也就是为什么，你在5s上截了一张图，在电脑上打开，它的原始宽度是640px的原因。
那 iphone 6 的截图宽度呢？ 375 × 2 = 750
那 iphone 6 sp 的截图宽度呢？ 414 × 3 = 1242
以此类推，你现在能明白效果图为什么一般是 640 ，750 甚至是 1242 的原因了么？（真没有歧视安卓机的意思。。。）


**2.问：宽度用rem写的情况下， 在 iphone6 上没问题， 在 iphone5上会有横向滚动条，何解？**

答：假设你的效果图宽度是750，在这个效果图上可能有一个宽度为7rem（高清方案默认 1rem = 100px）的元素。我们知道，高清方案的特点就是几乎完美还原效果图，也就是说，你写了一个宽度为 7rem 的元素，那么在目前主流移动设备上都是7rem。然而，iphone 5 的宽度为640，也就是6.4rem。于是横向滚动条不可避免的出现了。
怎么办呢？ 这是我目前推荐的比较安全的方式：**如果元素的宽度超过效果图宽度的一半（效果图宽为640或750），果断使用百分比宽度，或者flex布局**。就像把等屏宽的图片宽度设为100%一样。


**3.问：不是 1rem = 100px吗，为什么我的代码写了一个宽度为3rem的元素，在电脑端的谷歌浏览器上宽度只有150px?**

答：先说高清方案代码，再次强调咱们的高清方案代码是根据设备的dpr动态设置html 的 font-size，
如果dpr=1(如电脑端），则html的font-size为50px，此时 1rem = 50px
如果dpr=2(如iphone 5 和 6），则html的font-size为100px，此时 1rem = 100px
如果dpr=3(如iphone 6 sp），则html的font-size为150px，此时 1rem = 150px
如果dpr为其他值，即便不是整数，如3.4 , 也是一样直接将dpr 乘以 50 。

再来说说效果图，一般来讲，我们的效果图宽度要么是640，要么是750，无论哪一个，它们对应设备的dpr=2，此时，1 rem = 50 × 2 = 100px。这也就是为什么高清方案默认1rem = 100px。而将1rem默认100px也是好处多多，可以帮你快速换算单位，比如在750宽度下的效果图，某元素宽度为53px，那么css宽度直接设为53/100=0.53rem了。

然而极少情况下，有设计师将效果图宽定为1242px，因为他手里只有一个iphone 6 sp (dpr = 3)，设计完效果图刚好可以在他的iphone 6 sp里查看调整。一切完毕之后，他将这个效果图交给你来切图。由于这个效果图对应设备的dpr=3，也就是1rem = 50 × 3 = 150px。所以如果你量取了一个宽度为90px的元素，它的css宽度应该为 90/150=0.6rem。由于咱们的高清方案默认1rem=100px，为了还原效果图，你需要这样换算。当然，一个技巧就是你可以直接修改咱们的高清方案的默认设置。在代码的最后 你会看到 flex(false, 100, 1) ，将其修改成flex(false, 66.66667, 1)就不用那么麻烦的换算了，此时那个90px的直接写成0.9rem就可以了。


**4.问：在此方案下，我如果引用了别的UI库，那些UI库的元素会显得特别小，如何解决？**

答：可以这样去理解问题的原因，如果不用高清方案，别的UI库的元素在移动设备上（假设这个设备是iphone 5好了）显示是正常的，这没有问题，然后我们在这个设备上将该页面截图放到电脑上看，发现宽度是640（问答1解释过了），根据你的像素眼大致测量，你发现这个设备上的某个字体大小应该是12px，而你在电脑上测量应该是24px。

现在我们使用高清方案去还原这个页面，那么字体大小应该写为 0.24rem 才对！

所以，如果你引用了其他的UI库，为了兼容高清方案，你需要对该UI库里凡是应用px的地方做相应处理，即： a px => a*0.02 rem
(具体处理方式因人而异，有模块化开发经验的同学可使用类似的 px2rem 的插件去转化，也可以完全手动处理）

**（2018/3/23更新）然而真实情况往往更为复杂，比如，你引入了百度地图（N个样式需要处理转换）；或者你引入了一个framework；又或者你使用了 video 标签，上面默认的尺寸样式很难处理。等等这些棘手问题**

面对这些情况，此时我们的高清方案如果不再压缩页面，那么以上问题将迎刃而解。
基于这样的思路，笔者对高清方案的源码做了如下修改，即添加一个叫做 normal 的参数，由它来控制页面是否压缩。
在文章顶部代码的最后，你会看到 `flex(false, 100, 1)`，默认情况下页面是开启压缩的。

如果你需要禁止压缩，由于我们的源码执行后，直接将flex函数挂载到全局变量window上了，**此时你直接在需要禁止压缩的页面执行 **`window.flex(true)` **就可以了，而rem的用法保持不变**。

有一点美中不足的是，如果禁止了页面压缩，高清屏的1像素就不能实现了，如果你必须要实现1像素，那么自行谷歌：css 0.5像素，有N多的解决方案，这里不再赘述。

**5.问：有时候字体会不受控制的变大，怎么办？**

答：在X5新内核Blink中，在排版页面的时候，会主动对字体进行放大，会检测页面中的主字体，当某一块字体在我们的判定规则中，认为字号较小，并且是页面中的主要字体，就会采取主动放大的操作。然而这不是我们想要的，可以采取给最大高度解决

解决方案：

	*, *:before, *:after { max-height: 100000px }


补充：有同学反映，在一些情况下`textarea` 标签内的字体大小即便加上上面的方案，字体也会变大，无法控制。此时你需要给 `textarea` 的 `display` 设为 `table` 或者 `inline-table`即可恢复正常。

**6.问：我在底部导航用的flex感觉更合适一些，请问这样子混着用可以吗？**

答：咱们的rem适合写固定尺寸。其余的根据需要换成flex或者百分比。源码示例中就有这三种的综合运用。


**7.问：用了这个方案如何使用媒体查询呢？**

一般来讲，使用了这个方案是没必要用媒体查询了，如果你必须要用，假设你要对 iphone5 （css像素宽度320px,
这里需要取其物理像素，也就是640）宽度下的类名做处理，你可以这样

	@media screen and (max-width: 640px) {  
    	.yourLayout {  
    	    width:100%;  
		}  
	}  

 

**8.问：可以提供下这个高清方案的源码吗？**




	
	'use strict'  
	/**  
	 * @param {Boolean} [normal = false] - 默认开启页面压缩以使页面高清;  
	 * @param {Number} [baseFontSize = 100] - 基础fontSize, 默认100px;  
	 * @param {Number} [fontscale = 1] - 有的业务希望能放大一定比例的字体;  
	 */  
	const win = window;  
	export default win.flex = (normal, baseFontSize, fontscale) => {  
	const _baseFontSize = baseFontSize || 100;  
	const _fontscale = fontscale || 1;  
	
	const doc = win.document;  
	const ua = navigator.userAgent;  
	const matches = ua.match(/Android[\S\s]+AppleWebkit\/(\d{3})/i);  
	const UCversion = ua.match(/U3\/((\d+|\.){5,})/i);  
	const isUCHd = UCversion && parseInt(UCversion[1].split('.').join(''), 10) >= 80;  
	const isIos = navigator.appVersion.match(/(iphone|ipad|ipod)/gi);  
	let dpr = win.devicePixelRatio || 1;  
	if (!isIos && !(matches && matches[1] > 534) && !isUCHd) {  
	  // 如果非iOS, 非Android4.3以上, 非UC内核, 就不执行高清, dpr设为1;  
	  dpr = 1;  
	}  
	const scale = normal ? 1 : 1 / dpr;  
	
	let metaEl = doc.querySelector('meta[name="viewport"]');  
	if (!metaEl) {  
	  metaEl = doc.createElement('meta');  
	  metaEl.setAttribute('name', 'viewport');  
	  doc.head.appendChild(metaEl);  
	}  
	metaEl.setAttribute('content', `width=device- 	width,user-scalable=no,initial-scale=${scale},maximum-scale=${scale},minimum-scale=${scale}`);  
	doc.documentElement.style.fontSize = normal ? '50px' : `${_baseFontSize / 2 * dpr * _fontscale}px`;  
	};   


**10.问：我在使用 rem 布局进阶方案的时候遇到了XXX的问题，如何解决？**

+ 此方案久经考验，具有普遍适用性，自身出致命问题的情况很少，至少笔者是没遇到过。
+ 绝大多数你遇到的问题，都是由于对rem布局理解不到位导致的。本文对rem布局做了大量的解释说明，配置了若干 demo，你可以把你遇到的问题放到demo里测试。遇到问题时，首先问自己，为什么这明显的错误大家没遇到就我遇到了？？
+ 如果你真的经过充分验证，比对，确实是rem布局自身出了问题，那么请私信我，把还原问题场景的 demo 或者文件发给我。谢谢！
