在 WWDC 上看到 iOS 7 系统的发布后，我们重新审视了自己的应用 [Grocery List](http://appstore.com/grocerylistpx)，并且意识到：iOS 7 对于开发者来说是一个全新的开始，就像七年前 iPhone 首次发布一样。现在仅仅简单地改变设计是不够的，我们不得不重新思考并重构整个 app，从而让它适合 iOS 7 全新的环境。我们也的确是这么做的。
 
根据用户的反馈和我们自己的使用情况，我们意识到，虽然不能改变 app 基本的操作，但是应该对软件的操作流程进行一些优化。比如在旧版本中，添加产品的数量和单位是一个多步骤的操作过程，需要在多个 controller 之间进行导航。在 *Grocery List 2* 中，用户不用离开当前屏幕就能在恰当的位置设置数值。
 
在实现这个目标的过程中，遇到了一些我们觉得值得分享的问题。我们将会从动画和手势开始讲起，然后是界面、色彩以及字体等问题。接下来，为了吸引用户打开 app，我们将不得不思考如何针对 iOS 7 重新设计 app 的图标。最后，我们将分享在我们看来，苹果这次更新的意义何在。


## 动画

现在随着更新换代，移动设备的性能正变得越来越强大。与此同时，由于可以实时计算物品的物理属性，动画效果也变得愈加真实。在 iOS 7 中，我们不需要在界面中使用阴影和渐变这些效果了，而是应该更关注用户的感觉、手势以及交互的影响。凭借 iOS 7，你可以创建一个新世界而不是模仿旧有的世界。

新 SDK 可以让你简单地创建并使用自定义的动画效果。在 iOS 7 之前，开发者需要做大量额外的工作才能改变 view controller 之间的转场效果。iOS 7 可以让你简单地添加自己的动画，以帮助用户在不同屏幕之间切换的同时还不会丢失关注焦点。
 
在 *Grocery List* 中，我们在显示一个 modal view controller 时使用了轻度定制的转场动画。但是大部分的动画和转场效果都是使用系统默认的。我们本可以使用新的 API 来给 *Grocery List 2* 添加更多自定义的动画，但其实苹果提供的默认转场动画对于大多数情况来说已经是个不错的解决方案了，这也是为什么我们 app 中的不同 view controller 之间的转场效果和苹果官方的 app 是一样的。正如前边提到的那样，我们 app 的部分操作流程已经明显地发生了改变。所以，我们将会使用自定义动画从而更好地保持用户的关注焦点。

<img alt="Comparison of the Grocery List and the default view controller push" src="https://objccn.io/images/issue-5/redesign-animations.gif">

大多数用户对于 iOS 7 上默认的动画的感觉，是既新鲜又自然，你不需要做很多工作就可以使用这些动画来取悦用户。但是在合适的地方添加一些自定义动画将会提高整个 app 的用户体验。只是请小心不要使用过度。

## 手势

在拥有了数年的触屏设备的经验后，苹果发现大量使用手势对于用户来说正变得愈加自然。所以在 iOS 7 中，对手势的广泛使用比以前有了更多的可能性。比如在 table view cell 上滑动来显示隐藏的菜单，或者从左向右滑动来返回先前的 view controller，这些手势操作我们已经非常熟悉了，以至于如果一款应用不支持这些手势的话，我们马上就会非常想念它们。在合适的地方，这些直接的手势操作可以帮助用户更高效地完成任务而不会失去关注焦点。

在 *Grocery List* 中，我们并没有使用任何自定义手势，但是为了在下个版本中改进用户的操作流程，我们支持在 cell 上进行左右两个方向的滑动来分别展示产品的不同选项。你可以简单地从屏幕的右边缘向左滑动来快速访问菜单以进行列表或者模版的相关设置，而不用在导航栏一层层地返回。

<img alt="Grocery List 2 gestures" src="https://objccn.io/images/issue-5/redesign-gestures.png">

按钮和链接对于用户来说是可见的，也是可识别的，但手势不是。如果你打算用手势来实现某个功能，很好！但是如果 app 中那些依赖手势的功能没有一个等效的可见的控件，那要为用户提供一个好的方法来发现这些手势。一个好的用户界面通常应当是不言自明的。如果你需要一个类似使用说明一样的界面或者视频来描述 app 中的基本功能，那这里面很可能就有问题了。

## 界面

在正式发布前，大家对于 iOS 7 最大的争论莫过于扁平化和拟物化（[skeuomorphic](http://zh.wikipedia.org/wiki/仿制品)）这两种设计风格间的区别。iOS 7 完全摒弃了设计上对真实世界的依赖，但最大程度地保留了为大众所熟知的交互模式。新的纤细的工具栏图标可以帮助内容脱颖而出，但是别忘了，这样做的后果是这些图标本身变地不容易识别而且语义不明。尤其是当图标的下方没有说明其行为的文字标签时，情况更是如此。

我们发现争论的重点并不完全在于是设计上是应该再造还是移除所有实物的外观，而是说哪种设计可以更好地突显内容。如果在导航栏中增加细微的阴影可以突出内容的话，那也没必要一定不使用阴影。最重要的事情还是在需要的时候增加对比度，并且以一种方便用户使用的方式来展示你的内容。
 
*Grocery List* 在设计上非常依赖于真实世界的物品。比如以黑板为背景，类似纸张上的单元格，所有框架都是有光泽的木质效果。这种设计看起来很好看，但是在这个狭小的空间内如何放置用户交互的控件也会是个不小的挑战，增加新功能时也同样要考虑这个问题。在 iOS 7 这种更轻量的设计中，我们不必像之前那样关注如何更逼真地拟物化，而是可以把关注点放在如何提升交互，以便用户达成自己的目标。*Grocery List 2* 一定会使用这个新的设计语言，同时也会保持自己的风格。

<img alt="Comparison of the Grocery List and Grocery List 2 interface" src="https://objccn.io/images/issue-5/redesign-interface.png">

在 iOS 7 的设备上使用几周后，明显感觉到现在的交互变得比之前版本更方便。新的动画、手势以及减少对拟物化元素的使用让用户更好地关注内容。

## 颜色

iOS 6 和 iOS 7 的主要区别之一是色彩整体给人的感觉。外观的颜色从暗色转变为更鲜亮的色彩。iOS 7 使用了更为生机勃勃和高饱和度的颜色，以支持频繁使用的半透明设计和背景模糊设计。

考虑到 *Grocery List* 对拟物化设计的依赖，所以不可能过分调整用色。颜色是由我们想要模仿的材质所决定的。尽管我们喜欢 iOS 7 中更加友好的外观，像大多数内置的 app 一样大体上是白色，但是 *Grocery List 2* 这个 app 的外观将主要由符合「采购（Grocery）」这一主题的配色方案来决定。我们不希望我们的 app 看起来就仅仅是另外一个 iOS 7 风格的 app，而是希望创造独一无二的外观。

<img alt="Comparison of colors in a build-in iOS 7 app and Grocery List 2" src="https://objccn.io/images/issue-5/redesign-colors.png">

色彩可以影响用户对 app 的感觉。不要让你的 app 像内置的应用一样满是白色。相反要创造你自己独一无二的个性颜色。得益于 iOS 7 全新的设计风格刚和对拟物化使用的节制，你可以用各种出挑的色彩来表达你的 app 希望传递给用户的讯息。

## 字体

从 iOS 7 中对文本系统框架的重构这一点上就可以看出来，苹果认识到了字体的重要性。Lable 和 text field 现在直接使用 core text 提供的所有排版相关的功能，这里面就包括字体。连字（[Ligature](http://zh.wikipedia.org/wiki/合字)），文字装饰符（[swoosh](http://baike.baidu.com/view/1155820.htm)）等功能在新的框架下都可以简单地来实现。通过获取 text style 中的字体对象，你的 app 可以根据用户选择的字体大小来展示内容。想了解更详细的内容，可以看看这篇非常棒的关于 iOS 7 中的字体的[文章](http://typographica.org/on-typography/beyond-helvetica-the-real-story-behind-fonts-in-ios-7/)。

由于「实际」按钮的缺失以及文本周围描边的减少，文字本身获得了更多关注。由于在之前 iOS 7 的 beta 版本中大量使用 *Helvetica Neue* 的纤细体而受到排版专家的批评，苹果最终又换回了可读性更强的标准体。

在 *Grocery List* 中，我们使用 slab-serif 字体以配合拟物化风格。当 app 运行在 iOS 7 的设备上时，我们发现这个字体不是一个最佳选择。所以我们决定使用定制的 sans-serif 字体，这款字体可以更好地契合 app 整体的外观。

<img alt="Comparison of the Grocery List and Grocery List 2 fonts" src="https://objccn.io/images/issue-5/redesign-fonts.png">

内容是 app 的基础，提升文字的可读性非常重要，而可读性的关键在于字体。虽然苹果默认的 *Helvetica Neue* 字体适合大部分情景，但自定义字体也是值得考虑的——尤其是当你的 app 需要呈现大量文本的时候。

## App icon

苹果并不仅仅改变了 icon 的大小和轮廓，还改变了视觉氛围。App icon 不再使用光泽效果，并且大多数内置程序的 icon 是和网格对齐的。另外，icon 变得更简单了，移除了仿现实主义的效果，并且大多数只是在多彩的背景上展示简单的概念图标。这是从照相写实主义（[photorealistic](http://en.wikipedia.org/wiki/Photorealism)）风格的插图到阐述 icon 的本义——图示（[Iconographic](http://en.wikipedia.org/wiki/Iconographic)）的一次转变。

从一个有着黑板背景和木质纹理的拟物化的 app icon，转变为一个更加简洁的多彩的有着清晰符号的 icon，*Grocery List* 并不是真的完全适合新的主屏幕。下个版本中，我们把 icon 简化为一个购物篮符号，并选择一个背景色，这个背景色同样可以用作 app 的主色。这样的多种方法组合使用可以让 icon 更时尚和流行。

<img alt="Comparison of the Grocery List and Grocery List 2 app icons" src="https://objccn.io/images/issue-5/redesign-app-icon.png">

在 iOS 7 中，icon 会自动会缩放到新的尺寸，导致图像变模糊。由于 iOS 7 中使用了弧度超级大的圆角来遮盖你的 icon，阴影和高光效果看起来会非常奇怪。如果你不打算让你的 app 适配 iOS 7 的风格，那么至少更新一下你的 icon 的尺寸。

## 结论

虽然 iOS 7 给人整体的感觉是既新鲜又精致，但是很多概念都是保留下来的，比如从第一个版本就一直存在的导航功能，在列表和表格中查看数据，接收推送通知等等，用户对这类操作已经非常熟悉了，所以颜色和字体的更改以及移除拟物化设计元素等一系列的改变并没有打断用户所熟知的这一套操作流程。

在这个层面上，苹果并没有强迫你改变 app，但是我们建议你应该总是不断地尝试与时俱进，并始终把一点牢记于心：用户至上。

---

[话题 #5 下的更多文章](http://objccn.io/issue-5)

原文 [Re-Designing an App for iOS 7](http://www.objc.io/issue-5/redesigning-for-ios-7.html)

译文 部分内容参考自 [CocoaChina](http://www.cocoachina.com)
