## flutter_dafaBooks
初探fluuter技术原理，深入浅出flutter文档


#1.flutter 跨平台和其他跨平台技术的差异
其他部分跨平台技术使用的是解释性语言作为中转层 调用原生系统框架来渲染视图，这样无疑增加了一层开销。
flutter 则是采用将dart 转化为机器码使用自带引擎，来渲染视图，并以此来消除不同平台间的显示 差异化。
针对于传统安卓app，视图的渲染特性依靠手机系统的更新，而flutter 是在在分发app时，就已将runtime和渲染引擎一同下发，这就意味着，传统安卓app 需要更新安卓系统来使用新特性，而flutter app 只要更新flutter 版本（确保更新了渲染引擎），下发新版app，就可以将新特性展现出来，而不依赖用户更新安卓系统。

而flutter 自带引擎则是分别使用了impeller 和 skia，目前ios和mac os端已默认使用impeller，安卓则是3.27以后版本默认使用impeller ，之前则为skia。web端截止到3.35一直延用skia。
skia是通用即时绘图引擎，兼容性普及，但即时渲染也会带来 首帧卡顿问题（当然这并不是一定发生的）。
impeller是flutter专用Gpu渲染引擎，于skia不同的是为预编译渲染，来保证帧率稳定，但缓存肯定会造成体积大。
 从安全分析的角度来看，在逆向时需要知道对应的flutter 的版本，也是因为内置引擎的版本不同，Gpu调用逻辑不同导致的。但更多的，我想应该是flutter engine的变化导致符号表snapshot的变化
