title: UIScrollView基本用法
date: 2014-11-21 17:11:07
tags:
---

1.UIScrollView基本概念

	UIScrollView支持显示实际内容比UIWindow大的视图。
	它通过扫动手势，能够使用户滚动内容，并且通过捏合手势缩放部分内容。
	UIScrollView的核心理念是：它是一个可以在内容视图之上调整自己原点位置的视图。可以根据自身框架的大小，剪切视图中的内容，通常框架是和应用程序窗口一样大。一个滚动的视图可以根据手指的移动，调整原点的位置，展示内容的视图，根据滚动视图的原点位置开始绘制视图的内容，这个原点位置就是滚动视图的偏移量。，除了显示水平和竖直的指示器，ScrollView本身不绘制作何内容。
	滚动视图必须知道内容视图的大小，以便于知道什么时候停止；一般而言，当滚动出内容的边界时，它就返回了。

2.UIScrollView常用属性


	tracking
	当 touch 后还没有拖动的时候值是YES，否则NO
	zoomBouncing
	当内容放大到最大或者最小的时候值是 YES，否则 NO
	zooming
	当正在缩放的时候值是 YES，否则 NO
	decelerating
	当滚动后，手指放开但是还在继续滚动中。这个时候是 YES，其它时候是 NO
	decelerationRate
	设置手指放开后的减速率
	maximumZoomScale
	一个浮点数，表示能放最大的倍数
	minimumZoomScale 
	一个浮点数，表示能缩最小的倍数

	pagingEnabled
	当值是 YES 会自动滚动到 subview 的边界。默认是NO
	scrollEnabled
	决定是否可以滚动
	delaysContentTouches
	是个布尔值，当值是 YES 的时候，用户触碰开始，scroll view要延迟一会，看看是否用户有意图滚动。假如滚动了，那么捕捉 touch-down 事件，否则就不捕捉。假如值是NO，当用户触碰， scroll view 会立即触发 touchesShouldBegin:withEvent:inContentView:，默认是 YES
	canCancelContentTouches
	当值是 YES 的时候，用户触碰后，然后在一定时间内没有移动，scrollView 发送 tracking events，然后用户移动手指足够长度触发滚动事件，这个时候，scrollView 发送了 touchesCancelled:withEvent: 到 subview，然后 scroView 开始滚动。假如值是 NO，scrollView 发送 tracking events 后，就算用户移动手指，scrollView 也不会滚动。
	contentSize
	里面内容的大小，也就是可以滚动的大小，默认是0，没有滚动效果。

	showsHorizontalScrollIndicator
	滚动时是否显示水平滚动条
	showsVerticalScrollIndicator
	滚动时是否显示垂直滚动条
	bounces
	默认是 yes，就是滚动超过边界会反弹有反弹回来的效果。假如是 NO，那么滚动到达边界会立刻停止。
	bouncesZoom
	和 bounces 类似,区别在于：这个效果反映在缩放上面，假如缩放超过最大缩放，那么会反弹效果；假如是 NO，则到达最大或者最小的时候立即停止。
	directionalLockEnabled
	默认是 NO，可以在垂直和水平方向同时运动。当值是 YES 时，假如一开始是垂直或者是水平运动，那么接下来会锁定另外一个方向的滚动。 假如一开始是对角方向滚动，则不会禁止某个方向
	indicatorStyle
	滚动条的样式，基本只是设置颜色。总共3个颜色：默认、黑、白
	scrollIndicatorInsets
	设置滚动条的位置



3.UIScrollViewDelegate方法



	- (void)scrollViewDidScroll:(UIScrollView *)scrollView;                                               // any offset changes
	- (void)scrollViewDidZoom:(UIScrollView *)scrollView NS_AVAILABLE_IOS(3_2); // any zoom scale changes

	// called on start of dragging (may require some time and or distance to move)
	- (void)scrollViewWillBeginDragging:(UIScrollView *)scrollView;
	// called on finger up if the user dragged. velocity is in points/millisecond. targetContentOffset may be changed to adjust where the scroll view comes to rest
	- (void)scrollViewWillEndDragging:(UIScrollView *)scrollView withVelocity:(CGPoint)velocity targetContentOffset:(inout CGPoint *)targetContentOffset NS_AVAILABLE_IOS(5_0);
	// called on finger up if the user dragged. decelerate is true if it will continue moving afterwards
	- (void)scrollViewDidEndDragging:(UIScrollView *)scrollView willDecelerate:(BOOL)decelerate;

	- (void)scrollViewWillBeginDecelerating:(UIScrollView *)scrollView;   // called on finger up as we are moving
	- (void)scrollViewDidEndDecelerating:(UIScrollView *)scrollView;      // called when scroll view grinds to a halt

	- (void)scrollViewDidEndScrollingAnimation:(UIScrollView *)scrollView; // called when setContentOffset/scrollRectVisible:animated: finishes. not called if not animating

	- (UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView;     // return a view that will be scaled. if delegate returns nil, nothing happens
	- (void)scrollViewWillBeginZooming:(UIScrollView *)scrollView withView:(UIView *)view NS_AVAILABLE_IOS(3_2); // called before the scroll view begins zooming its content
	- (void)scrollViewDidEndZooming:(UIScrollView *)scrollView withView:(UIView *)view atScale:(CGFloat)scale; // scale between minimum and maximum. called after any 'bounce' animations

	- (BOOL)scrollViewShouldScrollToTop:(UIScrollView *)scrollView;   // return a yes if you want to scroll to the top. if not defined, assumes YES
	- (void)scrollViewDidScrollToTop:(UIScrollView *)scrollView;      // called when scrolling animation finished. may be called immediately if already at top
