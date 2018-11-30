# Flutter

## 许多的跨平台方案比较
1. 基于WebView的Cordova、AppCan：
优点：完全继承现代Web开发的所有成果
缺点：WebView的渲染效率和JavaScript执行性能太差。再加上Android各个系统版本和设备厂商的定制，很难保证所在所有设备上都能提供一致的体验。
2. HTML+JavaScript渲染成原生控件的React Native、Weex：
优点：将最终渲染工作交还给了系统，生成对应的自定义原生控件，充分利用原生控件相对于WebView的较高的绘制效率。
缺点：将框架本身和App开发者绑在了系统的控件系统上，不仅框架本身需要处理大量平台相关的逻辑，随着系统版本变化和API的变化，开发者可能也需要处理不同平台的差异，甚至有些特性只能在部分平台上实现，这样框架的跨平台特性就会大打折扣。
3. Flutter：
渲染引擎依靠跨平台的Skia图形库来实现，依赖系统的只有图形绘制相关的接口，可以在最大程度上保证不同平台、不同设备的体验一致性，逻辑处理使用支持AOT的Dart语言，执行效率也比JavaScript高得多。

## 分层结构
Flutter控件主要分为两大类，StatelessWidget和StatefulWidget，StatelessWidget用来展示静态的文本或者图片，如果控件需要根据外部数据或者用户操作来改变的话，就需要使用StatefulWidget。

![flutter1](/assets/flutter1.png)

## Flutter渲染
Flutter 的渲染流水线也包括两个线程 —— UI 线程和 GPU 线程。
UI 线程主要负责的是根据 UI 界面的描述生成 UI 界面的绘制指令，而 GPU 线程负责光栅化和合成。

![flutter2](/assets/flutter2.png)

## Flutter UI界面绘制

![flutter3](/assets/flutter3.png)

上图显示了 Flutter 更新 UI 界面的过程：
1. 运行动画，动画的结果会导致 Widget State 的改变；
2. State Changes 触发 Flutter 生成一棵新的 Widget 树；
3. Flutter 根据新/旧 Widget 树的差异更新 Render 树，重新排版更新界面布局；
4. Flutter 根据新的 Render 树更新 Composited Layer（合成图层）的 Display List；
5. 输出新的图层树；

## 消息机制
dart是基于单线程模型的语言，在dart也有自己的进程机制叫isolate
Dart线程中有一个消息循环机制（event loop）和两个队列（event queue和microtask queue）。
1. event queue
包含所有外来的事件：I/O，mouse events，drawing events，timers，isolate之间的message等。任意isolate中新增的event（I/O，mouse events，drawing events，timers，isolate的message）都会放入event queue中排队等待执行，好比机场的公共排队大厅。
2. microtask queue
只在当前isolate的任务队列中排队，优先级高于event queue，好比机场里的某个VIP候机室，总是VIP用户先登机了，才开放公共排队入口。

![flutter4](/assets/flutter4.png)

## state对象的生命周期

![flutter5](/assets/flutter5.png)

## Flutter和原生代码的通信

![flutter6](/assets/flutter6.png)

## 其它文档
Flutter中文网：https://flutterchina.club/
Flutter插件库：https://pub.dartlang.org/
API文档：https://docs.flutter.io/
原生插件：https://github.com/flutter/plugins

相关文章：https://tech.meituan.com/waimai_flutter_practice.html
