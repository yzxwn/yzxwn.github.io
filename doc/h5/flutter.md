## flutter

- [掘金](https://juejin.im/tag/Flutter)
- [云社区](https://cloud.tencent.com/developer/column/6114)
- [flutter 实战电子书](https://book.flutterchina.club/)
- [flutter 源码](https://github.com/flutter/flutter)
- [flutter 官网](https://flutter.dev/)
- [Dart 语言](https://dart.dev/guides/language/language-tour)

#### 简介

- Hybrid 开发主要依赖于 Webview。Webview 是一个重量级的控件，容易产生内存问题，复杂的 UI 显示性能不好
- React Native 抛开 Webview，利用 JavaScript Core 做桥接，将 JavaScript 调用转为 Native 调用，生成对应的原生控件
- Flutter 跨平台开发技术（Android、ios、MacOS、Windows、Linus 等）
  - 自己实现了一套 UI 框架，直接在 GPU 上渲染 UI 页面
  - 极速构建漂亮的原生应用、Dart 语言编写逻辑、Widget 框架构建 UI
  - 特点：跨平台、丝滑般的体验、响应式框架、支持插件访问平台本地 API、60fps 超高性能
  - 核心概念：
    - 组件：一切皆为组件（统一对象模型 Widget），组件嵌套
    - 构建：重写 Widget 的 build 方法来构建一个组件
    - 状态：处理用户交互，有状态 Widget 继承 StatefulWidget,将可变状态储存在 State 的子类中
    - 框架：分层的框架（Foundation,Rendering,Widgets,Material）

#### Dart

- 简介

```
特性：
    Dart是AOT（静态）编译的，在程序运行前编译
    Dart也可以（动态）编译，开发周期异常快
    Dart可以更轻松地创建以60fps运行的流程动画和转场，可以在没有锁的情况下进行内存分配和垃圾回收。由于Flutter被编译成本地代码，因此不需要建立缓慢的类似JavaScript到本地代码的过程，它的启动速度也快得多
    Dart使Flutter不需要单独的声明式布局语言（如JSX和XML）
    Dart容易学习，因为具有静态和动态语言用户都熟悉的特性
核心概念：
    所有的东西都是对象
    指定数据类型使得程序合理分配内存空间
    在运行前解析，可以提高运行速度
    统一的程序入口：main()
    没有public、protected、private的概念，私有特性通过加上下划线表示
    Dart得工具可以检查出编译和运行时的警告信息和错误信息
    支持anync/await异步处理
```

- 总结
  - 基本数据类型：Number、String、Boolean、List、Map
  - 常量：const 必须是编译时常量，final 可以是运行时常量
  - a ?? b：a 为 null 返回 b，否则返回 a
  - a ??= b：a 为 null 赋值 b，否则 a 不变
  - a?.b：a 为 null 取 null，否则取 a.b，可避免发生异常
  - a ~/ b：取整
  - assert(text != null)：assert 的判断条件是任何可以转化成 boolean 类型的对象，true 继续执行，false 抛出异常
  - 类：实例化、构造函数、读取写入、方法重载、继承类、抽象类、枚举类型、Mixins(多继承)
  - 泛型：为了类型安全而设计
  - import：as、show、hide
  - 异步支持：async 函数和 await 表达式，返回 Future 或 Stream 对象
  - 元数据：@override 重写父类方法、@proxy 代理
  - [...?list]：避免 list 为 null 报错，支持 map 和 set
  - as|is|is!：类型转换|类型判断|类型否定，obj is Object 始终为真

#### 组件

- 容器组件：Container
- 图片组件：Image（network：网络图片、asset：资源图片、file：本地图片文件、memory：Uint8List 资源图片）
- 文本组件：Text
- 图标组件：Icon
- 按钮组件：IconButton 图标、RaisedButton 凸起、FlatButton 扁平、OutlineButton 边框
- 基础列表组件：ListView
- 长列表组件：ListView.builder
- 网格列表组件：GridView
- 表单组件：Form、TextFormField

#### Material Design 风格

- MaterialApp：使用纸墨设计风格的应用的主组件
- Scaffold：显示单个界面的布局组件
- AppBar：固定在应用最上面，SliverAppBar（随内容滚动）
- ButtomNavigationBar：底部导航条组件
- TabBar：水平选项卡组件
- Drawer：抽屉组件
- FloatingActionButton：悬停按钮组件
- PopupMenuButton：弹出菜单组件
- SimpleDialog：简单对话框组件
- AlertDialog：提示对话框组件
- SnackBar：轻量提示组件
- TextField：文本框组件
- Card：卡片组件

#### Cupertino 风格

- CupertinoActivityIndicator：ios 风格的 loading 指示器
- CupertinoAlertDialog：对话框组件
- CupertinoButton：按钮组件
- CupertinoTabScaffold CupertinoTabBar CupertinoPageScaffold CupertinoNavigationBar

#### 布局

- 基础布局
  - Container：容器布局
  - Center：居中布局
  - Padding：填充布局
  - Align：对齐布局
  - Row：水平布局
  - Column：垂直布局
  - FittedBox：缩放布局
  - Stack：定位布局
  - OverflowBox：溢出布局
- 尺寸处理
  - SizedBox：设置具体宽高
  - ConstrainedBox：限定最大最小宽高
  - LimitedBox：限定最大宽高
  - AspectRatio：设置宽高比
  - FractionallySizedBox：设置百分比
- 列表布局：ListView
- 网格布局：GridView
- 表格布局：Table
- Transform：矩阵转换
- Baseline：基准线布局
- Offstage：控制是否显示组件
- Wrap：按宽高自动换行布局

#### 手势

- GestureDetector：手势检测
- Dismissible：滑动删除

#### 路由

- Navigator.push
- Navigator.pop

#### 组件装饰

- Opacity：透明度
- DecoratedBox：装饰盒子
- RotatedBox：旋转盒子
- Clip：裁剪（ClipOval 圆形、ClipRRect 圆角矩形、ClipRect 矩形、ClipPath 路径）
- CustomPaint：画板

#### 动画

- AnimatedOpacity：渐变效果
- Hero：页面切换动画
