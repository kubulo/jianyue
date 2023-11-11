> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [discuss.logseq.com](https://discuss.logseq.com/t/css-template-eisenhower-matrix/526)

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)here’s my attempt at an eisenhower matrix (priority matrix)

这是我对艾森豪威尔矩阵（优先矩阵）的尝试。

[![](https://discuss.logseq.com/uploads/default/optimized/1X/9285cb935a1b69143deac3d780ddc142bba20bdd_2_690x472.png)image 图像 1056×723 53.9 KB 图片 1056 ×723 53.9 KB](https://discuss.logseq.com/uploads/default/original/1X/9285cb935a1b69143deac3d780ddc142bba20bdd.png)

it works by combining a template and css rules :

它的工作原理是结合模板和 css 规则：

*   the template will create a tree structure and tag the root block with `#.v-eisenhower-matrix`
*   模板将创建一个树结构，并使用 `#.v-eisenhower-matrix` 标记根块
*   the css will look for the block tagged with `#.v-eisenhower-matrix` and apply styling/layout modifications
*   css 将查找标记为 `#.v-eisenhower-matrix` 的块并应用样式 / 布局修改
*   at any time, you can revert to the standard outlining view by removing the tag (or changing its name) as shown is the gif
*   在任何时候，您都可以通过删除标记（或更改其名称）恢复到标准大纲视图，如 gif 所示
*   colors and styling can be customized at the beginning of the css
*   颜色和样式可以在 css 开始时自定义
*   the captions can be modified in the template
*   标题可以在模板中修改

installation 安装
---------------

### 1. create the template 1. 创建模板

copy-paste the following lines in a document (I keep all my templates in a single document for easy management)

将以下行复制粘贴到文档中（我将所有模板保存在一个文档中，以便于管理）

show the template :  显示模板：

```
## #.v-eisenhower-matrix
:PROPERTIES:
:template: v-eisenhower
:END:
### [[TODO]]
####
####
####
### [[DECIDE]]
####
####
####
### [[DELEGATE]]
####
####
####
### [[ELIMINATE]]
####
####
#### 


```

it will create a template called `v-eisenhower` that looks like this

它将创建一个名为 `v-eisenhower` 的模板，如下所示

[![](https://discuss.logseq.com/uploads/default/optimized/1X/7b07eefd15954af6fa823764290580384da9f26b_2_385x500.png)image 图像 632×820 10.4 KB 图像 632 ×820 10.4 KB](https://discuss.logseq.com/uploads/default/original/1X/7b07eefd15954af6fa823764290580384da9f26b.png)

### 2. the css 2. 的 css

copy the css rules at the bottom of your `custom.css` or use the `stylus` addon to load them

复制 CSS 规则在你的 `custom.css` 底部或使用 `stylus` 插件加载它们

CODE v20210306 : 代码 v20210306：

```
/* WIP css eisenhower matrix by cannibalox v202100306 */
/* works best with the `v-eisenhower` template        */
/* activate with:  `/template v-eisenhower		      */
/* or tag a block with `#.v-eisenhower-matrix`        */  
/* define vars */ 
[data-refs-self*="eisenhower-matrix"]{
	--eisen-caption-color: #fff;
	--eisen-caption-bg: #0000;
	--eisen-scrollbar-thumb: #f9f9f99e;
	--eisen-scrollbar-track: #0000;
	--eisen-outercaption-color: #979797b8;
	--eisen-todo-bgcolor: #4bad00a8;
	--eisen-decide-bgcolor: #0067beb8;
 	--eisen-delegate-bgcolor:#bf8300c7;
 	--eisen-eliminate-bgcolor:#9c003ecc;
	--eisen-bullet-color : #d9d9d9;
	--eisen-clover-borderstyle: none; /*eg: 3px solid white */
}

/* optionnal : add captions around the diagram */
div[data-refs-self*="eisenhower-matrix"] > .block-children:before {
	content: "↑ IMPORTANT";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	left: 44%;
	top: 0.5rem;
}  
div[data-refs-self*="eisenhower-matrix"] > .block-children:after {
	content: "URGENT ←";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	left: -1rem;
	top: 50%;
}  
div[data-refs-self*="eisenhower-matrix"]:before {
	content: "↓ NOT IMPORTANT";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	left: 43%;
	bottom: -0.5rem;
}  
div[data-refs-self*="eisenhower-matrix"]:after {
	content: "→ NOT URGENT";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	right: -2rem;
	top: 50%;
}  

/* blocks / col */
div[data-refs-self*="eisenhower-matrix"] > .block-children > div.ls-block {
	display: inline-block;
	width: 46%;
	overflow: hidden;
	margin: 5px;
	height: 14rem;
	}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block {
	border:var(--eisen-clover-borderstyle);}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block:nth-last-child(4) 
	{border-radius: 0 2rem 0 2rem; background-color: var(--eisen-todo-bgcolor);}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block:nth-last-child(3) 
	{border-radius: 2rem 0 2rem 0; background-color: var(--eisen-decide-bgcolor);}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block:nth-last-child(2) 
	{border-radius: 2rem 0 2rem 0; background-color: var(--eisen-delegate-bgcolor);}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block:nth-last-child(1) 
	{border-radius: 0 2rem 0 2rem; background-color: var(--eisen-eliminate-bgcolor);}

/* clover contents */
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block > .block-children {
	overflow: auto;
	height: 12rem;
}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block > .block-children .bullet {
	background-color:var(--eisen-bullet-color) !important;
}

/* scrollbar for each block */
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block > .block-children::-webkit-scrollbar-thumb {background-color:var(--eisen-scrollbar-thumb); border-radius: 0px;}
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block > .block-children::-webkit-scrollbar-track {background:var(--eisen-scrollbar-track); }

/* block titles */
	div[data-refs-self*="eisenhower-matrix"] > .block-children > div.ls-block > .flex-1.flex-row > div > .block-content {
		font-weight: 700;
		font-size: 0.7rem;
		text-align: center;
		margin-left: -1rem;
	} 
	div[data-refs-self*="eisenhower-matrix"] > .block-children > div.ls-block > .flex-1.flex-row > div > .block-content .page-reference {
		background:var(--eisen-caption-bg);
		border-radius: 10px;
	} 
	div[data-refs-self*="eisenhower-matrix"] > .block-children > div.ls-block > .flex-1.flex-row > div > .block-content .page-ref {
		color:var(--eisen-caption-color);
	} 
	/* remove bullet of the block title */
	div[data-refs-self*="eisenhower-matrix"] > .block-children > div.ls-block > .flex-1.flex-row > div .bullet {
		visibility: hidden
	} 

/* remove indent line ~ margin-left of table cells */
div[data-refs-self*="eisenhower-matrix"] > .block-children > .ls-block > .block-children {
	border: 0;
    margin: 0px !important;
}
div[data-refs-self*="eisenhower-matrix"] > .block-children {
	border:none;
    margin: 0px 0px 0 30px !important;
}

/* =============== END OF EISENHOWER MATRIX =====================*/


```

usage 使用
--------

once you have created the template and saved the css rules, invoke the command:

创建模板并保存 css 规则后，调用命令：

`/Template`

then choose `v-eisenhower`

然后选择 `v-eisenhower`

VIDEO DEMO 视频演示

[![](https://discuss.logseq.com/uploads/default/original/1X/b7b600c4c91c6108e9900f093dc69c7e91b4038e.gif)20210306_NUC8_uf5vSZiHNF1276×1050 540 KB](https://discuss.logseq.com/uploads/default/original/1X/b7b600c4c91c6108e9900f093dc69c7e91b4038e.gif)

20210306_NUC8_uf5vSZiHNF 1276 ×1050 540 KB

notes: 备注：

*   this should work with custom themes, but may require some tweaking for margins, etc…
*   这应该与自定义主题，但可能需要一些调整的利润率等…
*   this is a display mode, thus the inner structure of the notes still rely on indented bullets. if you want to exit the matrix, you can use TAB or SHIFT TAB to indent/unindent bullets until they are not part of the eisenhower matrix
*   这是一种显示方式，所以纸币的内部结构还是靠缩进的子弹。如果你想退出矩阵，你可以使用 TAB 或 TAB 键来删除 / 取消删除项目符号，直到它们不再是艾森豪威尔矩阵的一部分

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)I almost forgot : if you want to replace the tag `#.v-eisenhower-matrix` by the auto-expanding eye icon (as seen in the gif)

我差点忘了：如果你想用自动扩展的眼睛图标替换标签 `#.v-eisenhower-matrix` （如 GIF 中所示）

![](https://discuss.logseq.com/uploads/default/original/1X/463982077206f8a32a455cf49d97e61449ce6e70.gif)

you can add these css rules:

你可以添加这些 CSS 规则：

```
/* vismode icon component by cannibalox */ 
/* part of the ls-vizmods-suite         */ 
a.tag[data-ref*=".v-"]:before {
   content:"👁";
   font-size: 0.75rem; 
   line-height: 0.75rem;
   }
a.tag[data-ref*=".v-"]:hover:before {
   padding-right:0.3rem;
   }
a.tag[data-ref*=".v-"]:hover {
   font-size: 0.75rem; 
   line-height: 0.75rem;
   }
a.tag[data-ref*=".v-"]{
   font-size: 0px; 
   font-family: iosevka, fira code, consolas, source code pro;
   color: #88e165;
   background-color: #1a2d23;
   border: 1px solid #a1c65d; border-radius: 3px;
   padding: 0 2px;
   }


```

I will reuse the same taxonomy for my other css addons.

我将在我的其他 css 插件中重用相同的分类法。

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/tommykakashi/96/368_2.png)Could you elaborate on what the query is and the NOW page? How you organize todos?

你能详细说明一下查询是什么和现在的页面吗？如何组织 todos？

![](https://discuss.logseq.com/letter_avatar_proxy/v4/letter/w/8c91f0/96.png)[@cannibalox](/u/cannibalox)

This template is amazing. I’ve been using a slightly modified version of his for an OKR quad and very similar styling, but noticed it has broken with the latest beta. I"m assuming because of some changes in the way the beta perhaps handles styling or divs?

这个模板是惊人的。我一直在使用一个稍微修改过的版本，他的 OKR 四和非常相似的造型，但注意到它已经打破了最新的测试版。我假设是因为测试版处理样式或 div 的方式发生了一些变化？

Just wondering if you have an updated version of it since I am having trouble figuring out what has changed and broken (and you’re obviously amazing at this stuff.).

只是想知道你是否有一个更新的版本，因为我很难弄清楚什么已经改变和打破（你显然是惊人的在这方面的东西。）。

thanks! 谢谢！

![](https://discuss.logseq.com/letter_avatar_proxy/v4/letter/g/71e660/96.png)hello,it looks amazing,but I find it can not work in version 0.59 correctly.

你好，它看起来很神奇，但我发现它不能在 0.59 版本正确工作。

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/gestaltist/96/2919_2.png)As a complete noob: could this be shipped as a plug-in? It’s amazing

![](https://discuss.logseq.com/images/emoji/twitter/slight_smile.png?v=10)

作为一个完全的菜鸟：这可以作为一个插件运送？太神奇了 ![](https://discuss.logseq.com/images/emoji/twitter/slight_smile.png?v=10)

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)sorry for the late fix.can’t edit the first post toupdate.

抱歉，后期修复。不能编辑第一个帖子更新。

updated for logseq 0.6.x, now available as part of logtools plugin:

更新了 logseq 0.6.x，现在作为 logtools 插件的一部分提供：

[GitHub - cannibalox/logtools: utilities for Logseq (kanban, image gallery, priority matrix, ...) 233](https://github.com/cannibalox/logtools)

[GitHub - cannibalox/logtools：Logseq 的实用程序（看板，图像库，优先级矩阵，.）233](https://github.com/cannibalox/logtools)

[GitHub - cannibalox/logtools：Logseq 的实用程序（看板，图像库，优先级矩阵，...）233](https://github.com/cannibalox/logtools)

or on the marketplace 或者在市场上

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/yuanli.eth/96/7318_2.png) Thank you for your great job! But when I installed the plugin I encountered some problem.

感谢你的评分但是当我安装插件时，我遇到了一些问题。

I have installed it, copy the template code, then I got the error below:

我已经安装了它，复制模板代码，然后我得到了下面的错误：

[![](https://discuss.logseq.com/uploads/default/optimized/2X/d/d552043c5af847c4376f816202246ab684a4ea5e_2_690x461.png)图片 1844×1234 79.5 KB](https://discuss.logseq.com/uploads/default/original/2X/d/d552043c5af847c4376f816202246ab684a4ea5e.png)

It seems like CSS worked but the template doesn’t worked well. If I simply tag a block with `#.v-eisenhower`, it looks like:

看起来像 CSS 工作，但模板不工作得很好。如果我简单地用 `#.v-eisenhower` 标记一个块，它看起来像：

[![](https://discuss.logseq.com/uploads/default/optimized/2X/a/aa5bb6ed7a65ec1c2a0d86094e48a22a27a894b9_2_690x243.png)图片 1708×602 15.8 KB](https://discuss.logseq.com/uploads/default/original/2X/a/aa5bb6ed7a65ec1c2a0d86094e48a22a27a894b9.png)

Does the plugin worked for 0.8.x? Or something else I missed?

该插件适用于 0.8.x 吗？或者我错过了什么？

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)hey I’m sorry for the trouble, the template in the fist post is using a deprecated syntax… unfortunately I can’t edit my older post.

嘿，我很抱歉的麻烦，在第一个帖子的模板是使用一个弃用的语法. 不幸的是，我不能编辑我的旧帖子。

the correct template for LS 0.8.x should be :

LS 0.8.x 的正确模板应该是：

```
- #.v-eisenhower-matrix
  template:: eisenhower-matrix
	- [[TODO]]
		-
		-
		-
	- [[DECIDE]]
		-
		-
		-
	- [[DELEGATE]]
		-
		-
		-
	- [[ELIMINATE]]
		-
		-
		-


```

make sure your are using the latest version of `Logtools` from the marketplace or here: [https://github.com/cannibalox/logtools 47](https://github.com/cannibalox/logtools)

请确保您使用的是 Marketplace 或此处提供的最新版本的 `Logtools` ： [https://github.com/cannibalox/logtools 47](https://github.com/cannibalox/logtools)

![](https://discuss.logseq.com/letter_avatar_proxy/v4/letter/e/f05b48/96.png)I am trying to use the date picker to add a due date to a task. I noticed the menu bar is white due to the CSS. Is there a way for the menu bar to stay transparent?

我正在尝试使用日期选择器为任务添加截止日期。我注意到菜单栏是白色由于 CSS。有办法让菜单栏保持透明吗？

I am guessing you are using a different background to avoid the line going through Urgent?

我猜你是用不同的背景，以避免线通过紧急？

[![](https://discuss.logseq.com/uploads/default/optimized/2X/e/e9def36929e66dbb945f5232be39275070de0c5b_2_690x499.png)CleanShot 2022-12-02 at 21.01.22@2x](https://discuss.logseq.com/uploads/default/original/2X/e/e9def36929e66dbb945f5232be39275070de0c5b.png)

CleanShot 2022-12-02 在 21.01.22@2x2042×1478 109 KB

CleanShot 2022-12-02 在 21.01.22@2x2042×1478 109 KB

![](https://discuss.logseq.com/letter_avatar_proxy/v4/letter/e/f05b48/96.png)Eisenhower Matrix also works well with putting a TODO next to the task. However, it is navigating the menu due to it being all white. Is there another workflow you use to manage the tasks in the matrix?

艾森豪威尔矩阵也可以很好地将 TODO 放在任务旁边。然而，它是导航菜单，因为它是全白色。您是否使用其他工作流来管理矩阵中的任务？

[![](https://discuss.logseq.com/uploads/default/optimized/2X/4/45f1199eb8ee98b56b1e369b20507e58b0ea441e_2_475x499.png)CleanShot 2022-12-02 at 21.32.37@2x](https://discuss.logseq.com/uploads/default/original/2X/4/45f1199eb8ee98b56b1e369b20507e58b0ea441e.png)

CleanShot 2022-12-02 在 21.32.37@2x2208×2320 204 KB

CleanShot 2022-12-02 在 21.32.37@2x2208×2320 204 KB

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)I use a dark theme+custom css, what theme are you using?

我用的是黑暗主题 + 自定义 css，你用的是什么主题？

I’ll try to make it work for default light theme, but not have a lot of time atm, you can also tweak the value/colors in the installed script if you don’t want to wait or switch to dark mode.

我会尝试让它为默认的光主题工作，但没有太多的时间，如果你不想等待或切换到黑暗模式，你也可以调整安装脚本中的值 / 颜色。

![](https://discuss.logseq.com/letter_avatar_proxy/v4/letter/e/f05b48/96.png)I appreciate your willingness to look into making the update.

我很感激你愿意考虑更新。

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/mr.ggpx/96/9680_2.png)[![](https://discuss.logseq.com/uploads/default/optimized/2X/5/503a35f87546c2e1419f0fa768eaac5abdeb2166_2_690x330.png)image 图像 3082×1474 167 KB](https://discuss.logseq.com/uploads/default/original/2X/5/503a35f87546c2e1419f0fa768eaac5abdeb2166.png)

图片 3082 ×1474 167 KB

  

I have used the css config you provide ,it seems have a problem on my computer, can you give me some advice ?

我用了你提供的 css 配置，我的电脑好像有问题，你能给予我一些建议吗？

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)it’s probably the theme that changes the positionning of the elements, you can try to add rules in your custom.css and tweak the values

可能是主题改变了元素的位置，你可以尝试在你的 custom.css 中添加规则并调整值

```
div[data-refs-self*="eisenhower-matrix"]:before {
	content: "↓ NOT IMPORTANT";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	left: 43%;
	bottom: -0.5rem;
}  
div[data-refs-self*="eisenhower-matrix"]:after {
	content: "→ NOT URGENT";
	position: absolute;
	color: var(--eisen-outercaption-color);
	font-size: 12px;
	right: -2rem;
	top: 50%;
}  


```

[/quote]

you should tweak the values for “left, bottom, right, top” so trhat they work for your theme, maybe in the ‘not urgent’ section, try to replace`bottom: -0.5rem;` by `bottom: 3rem`

你应该调整 “左，下，右，上” 的值，这样它们才能为你的主题工作，也许在 “不紧急” 部分，试着用 `bottom: 3rem` 替换 `bottom: -0.5rem;`

and for ‘not urgent’, try to replace `top:50%` by `top: 52%`

对于 “不紧急”，请尝试将 `top:50%` 替换为 `top: 52%`

I’m not sure which values would work with this custom theme though, so you need to try different values.

我不确定哪些值可以用于此自定义主题，因此您需要尝试不同的值。

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/mr.ggpx/96/9680_2.png)I have tried it , but it doesn’t seems working after I tweak the values for “left,bottom,right,top”,my software version is 0.9.1

我试过了，但是在我调整了 “左，下，右，上” 的值后，它似乎不起作用，我的软件版本是 0.9.1

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/cannibalox/96/24_2.png)hmm…it should work in 0.9.1 (I’m using 0.9.1 nightly).

嗯...... 它应该在 0.9.1 中工作（我每晚都使用 0.9.1）。

are you able to move the elements at all ?

你能移动元素吗

if you need to find the correct values, you can use DevTools to tweak the values, then copy trhe rules to your custom.css. a breakdown:

如果你需要找到正确的值，你可以使用 DevTools 来调整这些值，然后将这些规则复制到你的 custom.css 中。细分：

in logseq, on a page with the priority matrix, hit `ctrl+shift+i` (or F12) to open the DevTools panel, it should look like the screen below more or less

在 logseq 中，在具有优先级矩阵的页面上，点击 `ctrl+shift+i` （或 F12）以打开 DevTools 面板，它应该看起来或多或少像下面的屏幕

[![](https://discuss.logseq.com/uploads/default/optimized/2X/e/e9b1c53d40eba9a01cc704f8846ed7f2fa2a81ce_2_690x388.jpeg)image 图像 1920×1080 154 KB](https://discuss.logseq.com/uploads/default/original/2X/e/e9b1c53d40eba9a01cc704f8846ed7f2fa2a81ce.jpeg)

1.  use the Select tool (icon on top left of the devtools panel)
2.  使用选择工具（devtools 面板左上角的图标）
3.  point to one of the labels from the priority matrix, this should bring you to the relevant section of the html source code
4.  指向优先级矩阵中的一个标签，这应该会将您带到 html 源代码的相关部分
5.  in the code panel, you should see the same code as in the screenshot, locate the first `::before` highlighted in the screenshot and click on it, this should correspond to the `NOT IMPORTANT` label from the priority matrix (at the bottom)
6.  在代码面板中，您应该看到与屏幕截图中相同的代码，找到屏幕截图中突出显示的第一个 `::before` 并单击它，这应该与优先级矩阵中的 `NOT IMPORTANT` 标签相对应（底部）
7.  in the css tab, you should see the css rule, tweak the values for `left` and `bottom` using your cursor up and down keys or type in numbers and validate with enter, the element should move in realtime (if you use the arrows keys) so you can tweak values until its position looks correct.
8.  在 css 选项卡中，你应该看到 css 规则，使用光标上下键调整 `left` 和 `bottom` 的值，或者输入数字并用回车键验证，元素应该实时移动（如果你使用箭头键），这样你就可以调整值，直到它的位置看起来正确。
9.  Once it’s in the right position : in the css panel, use the right mouse button and chose `copy rule` (see screenshot). Paste that rule in your custom.css and save
10.  一旦它在正确的位置：在 css 面板中，使用鼠标右键并选择 `copy rule` （见截图）。将该规则粘贴到 custom.css 中并保存
11.  [![](https://discuss.logseq.com/uploads/default/original/2X/6/6b05f627fb290352f7a21c94e974b1eb0584d3bb.png)image 图像 835×703 52.6 KB](https://discuss.logseq.com/uploads/default/original/2X/6/6b05f627fb290352f7a21c94e974b1eb0584d3bb.png)
12.  do the same steps for the other label (the `NOT URGENT` should be the last `::after` in the code from the first screenshot, highlight in green)
13.  对另一个标签执行相同的步骤（ `NOT URGENT` 应该是第一个屏幕截图中代码中的最后一个 `::after` ，以绿色突出显示）

I hope this can help.

希望这能帮上忙。

![](https://discuss.logseq.com/user_avatar/discuss.logseq.com/mr.ggpx/96/9680_2.png)thank you for your help , I have solved the problem

![](https://discuss.logseq.com/images/emoji/twitter/+1.png?v=12)

谢谢你的帮助，我已经解决了问题 ![](https://discuss.logseq.com/images/emoji/twitter/+1.png?v=12)