# ApplicationHelperFramework
一行代码快速解耦Application逻辑，让Application更简洁好维护

使用场景： Application里面配置的过多的时候，可以使用这个库。

注意事项：

1.目前只适用于普通开发，组件化插件化没做兼容处理。
2.线程切换也没做考虑，因为一般的第三方库的使用基本都是在主线程，所以没做线程切换，后续有时间会慢慢完善的。
3.进程有关的也没做处理，因为目前用到的三方库没有这方面的需求，所以没考虑这一块。


代码看图http://upload-images.jianshu.io/upload_images/6098829-2f6045c5208edb0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240



2.下面看一下ApplicationHelper这个类做了什么事情：

这是一个单例的类，调用init方法传入上下文，然后调用init开头的方法，比如initNetWork()就表示初始化网络操作的一些逻辑。

代码看图http://upload-images.jianshu.io/upload_images/6098829-724ff551f0cb1e2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240


3.再看看ApplicationHelper这个类

ApplicationHelper实现了IInitMethods接口，这个接口主要用来规范有哪些逻辑要处理，它是初始化的所有方法的顶层接口，用于规范有哪些逻辑需要做，比如网络库，图片库等。

代码看图http://upload-images.jianshu.io/upload_images/6098829-60d9d78ee254bd46.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240



4.ApplicationHelper类调用了InitWrapperImpl这个类

ApplicationHelper通过InitWrapperImpl.getInstance()返回一个实例对象，然后调用了init(mContext)方法，传入一个上下文，最后调用execute(XX,XX,XX)执行库的初始化的具体操作。

代码看图http://upload-images.jianshu.io/upload_images/6098829-e276da4ce3138d7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240

5.InitWrapperImpl这个类里面用到了常量类Contants，主要保存type类型，和库的名字的信息。

代码看图http://upload-images.jianshu.io/upload_images/6098829-625be7b2eafac0d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240
