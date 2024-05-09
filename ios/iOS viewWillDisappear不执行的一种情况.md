
# iOS viewWillDisappear不执行的一种情况

最近在开发过程中，A（VC）跳转另一个B（VC）时。A不调用viewWillDisappear不执行就出现了。


特意去查了一下调用viewWillAppear的条件，同时查看了Present的类型说明


```object-c 

/// Called when the view is about to made visible, before it is added to the hierarchy.
/// Because the view is not yet in the hierarchy at the time this method is called, it
/// is too early in the appearance transition for many usages. Prefer -viewIsAppearing:
/// instead of this method when possible. Only use this method when its exact timing
/// before the appearance transition starts running is desired, such as to set up an
/// alongside animation with a transition coordinator, or as a counterpart for paired
/// code in a viewWillDisappear/viewDidDisappear callback that does not rely on the
/// view or view controller's trait collection or the view hierarchy.
- (void)viewWillAppear:(BOOL)animated;


/// Called when the view is about to be dismissed, covered, or otherwise hidden.
- (void)viewWillDisappear:(BOOL)animated;




/*
 Defines the presentation style that will be used for this view controller when it is presented modally. Set this property on the view controller to be presented, not the presenter.
 If this property has been set to UIModalPresentationAutomatic, reading it will always return a concrete presentation style. By default UIViewController resolves UIModalPresentationAutomatic to UIModalPresentationPageSheet, but system-provided subclasses may resolve UIModalPresentationAutomatic to other concrete presentation styles. Participation in the resolution of UIModalPresentationAutomatic is reserved for system-provided view controllers.
 Defaults to UIModalPresentationAutomatic on iOS starting in iOS 13.0, and UIModalPresentationFullScreen on previous versions. Defaults to UIModalPresentationFullScreen on all other platforms.
 */
@property(nonatomic,assign) UIModalPresentationStyle modalPresentationStyle API_AVAILABLE(ios(3.2));

```

从ViewController的基类上的解释，可以定位到问题如下

### 问题所在

如果B（VC）使用overFullScreen模式推出后，A（VC）的viewWillDisappear不执行，**需要改为fullScreen模式。**  （含over的都需要修改）


在UIModalPresentationStyle模式中：

凡是带有over的都是在原视图上覆盖（类似View Add 一个新的View，Controller的层级并没改变），层级关系上原始图还在， 所以viewWillDisappear不会走，因为它本身就在那。


不带over的原视图VC会被压到视图VC栈下层， VC执行viewWillDisappear方法。 





