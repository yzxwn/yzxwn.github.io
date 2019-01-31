## browser（浏览器）对象

* [Window](#window：浏览器中打开的窗口)
* [Navigator](#navigator：有关浏览器的信息)
* [Screen](#screen：有关客户端显示屏幕的信息)
* [History](#history：包含用户（在浏览器窗口中）访问过的url)
* [Location](#location：包含有关当前url的信息)

#### Window：浏览器中打开的窗口
* 对象集合:
    * **frames[]**：返回窗口中所有命名的框架
    ```
    该集合是 Window 对象的数组，每个 Window 对象在窗口中含有一个框架或 <iframe>。
    属性 frames.length 存放数组 frames[] 中含有的元素个数。
    注意，frames[] 数组中引用的框架可能还包括框架，它们自己也具有 frames[] 数组
    ```
* 对象属性:
    * **closed**：返回窗口是否已被关闭
    * **name**：设置或返回窗口的名称
    * **opener**：设置或返回对创建此窗口的窗口（父窗口）的引用
    * **parent**：返回父窗口
    * **document**：对 [Document](htmlDom对象.md) 对象的只读引用
    * **history**：对 [History](history) 对象的只读引用
    * **location**：用于窗口或框架的 [Location](#location) 对象
    * **Navigator**：对 [Navigator](navigator) 对象的只读引用
    * **Screen**：对 [Screen](#screen) 对象的只读引用
    * **length**：设置或返回窗口中的框架数量
    * **innerheight|innerwidth**：返回窗口的文档显示区的高度|宽度（像素）
    ```js
    //不包括菜单栏、工具栏以及滚动条等。

    //兼容IE5、6、7、8
    var w=window.innerWidth
    || document.documentElement.clientWidth
    || document.body.clientWidth;
    var h=window.innerHeight
    || document.documentElement.clientHeight
    || document.body.clientHeight;
    ```
    * **outerheight|outerwidth**：返回窗口的外部高度|宽度
    ```js
    IE 不支持此属性，且没有提供替代的属性
    ```
    * **pageXOffset|pageYOffset**：设置或返回当前页面相对于窗口显示区左上角的 X | Y 位置
    * **screenLeft、screenTop、screenX、screenY**：只读整数。声明了窗口的左上角在屏幕上的的 x 坐标和 y 坐标。IE、Safari 和 Opera 支持 screenLeft 和 screenTop，而 Firefox 和 Safari 支持 screenX 和 screenY
    * **top**：返回最顶层的先辈窗口
    * **window**：window 属性等价于 self 属性，它包含了对窗口自身的引用
    * **self**：返回对当前窗口的引用。等价于 Window 属性
    * **defaultStatus**：设置或返回窗口状态栏中的默认文本
    * **status**：设置窗口状态栏的文本
* 对象方法:
    * **消息框**：（调用消息框暂停对 JavaScript 代码的执行）
    ```js
    //警告框
    alert("文本"); //用户点击确认之后才会继续执行
    //确认框
    confirm("文本"); //用户点击确认或取消之后才会继续执行，返回布尔值
    //提示框
    prompt("文本","默认值"); //用户点击确认或取消之后才会继续执行，返回用户输入值
    ```
    * **计时**：
    ```js
    //在指定的毫秒数后调用函数或计算表达式
    var t = setTimeout("alert('5 seconds!')",5000); //5s之后执行一次
    clearTimeout(t); //清除定时器
    //按照指定的周期（以毫秒计）来调用函数或计算表达式
    var t = setInterval("alert('5 seconds!')",5000); //5s之后循环执行
    clearInterval(t); //清除定时器
    ```
    * **open(URL?,name?,features?,replace?)**：打开一个新的浏览器窗口或查找一个已命名的窗口
    * **close()**：关闭浏览器窗口
    * **focus()**：把键盘焦点给予一个窗口
    * **blur()**：把键盘焦点从顶层窗口移开
    * **createPopup()**：创建一个 pop-up 窗口
    * **print()**：打印当前窗口的内容
    * **moveBy(x,y)**：可相对窗口的当前坐标把它移动指定的像素
    * **moveTo(x,y)**：把窗口的左上角移动到一个指定的坐标
    * **resizeBy(width,height)**：按照指定的像素调整窗口的大小
    * **resizeTo(width,height)**：把窗口的大小调整到指定的宽度和高度
    * **scrollBy(xnum,ynum)**：按照指定的像素值来滚动内容
    * **scrollTo(xpos,ypos)**：把内容滚动到指定的坐标

#### Navigator：有关浏览器的信息
* 对象集合:
    * **plugins[]**：返回对文档中所有嵌入式对象的引用
    ```
    该集合是一个 Plugin 对象的数组，其中的元素代表浏览器已经安装的插件。
    Plug-in 对象提供的是有关插件的信息，其中包括它所支持的 MIME 类型的列表。
    虽然 plugins[] 数组是由 IE 4 定义的，但是在 IE 4 中它却总是空的，因为 IE 4 不支持插件和 Plugin 对象。
    ```
* 对象属性:
    * **appCodeName**：返回浏览器的代码名
    * **appMinorVersion**：返回浏览器的次级版本
    * **appName**：返回浏览器的名称
    * **appVersion**：返回浏览器的平台和版本信息
    * **browserLanguage**：返回当前浏览器的语言
    * **cookieEnabled**：返回指明浏览器中是否启用 cookie 的布尔值
    * **cpuClass**：返回浏览器系统的 CPU 等级
    * **onLine**：返回指明系统是否处于脱机模式的布尔值
    * **platform**：返回运行浏览器的操作系统平台
    * **systemLanguage**：返回 OS 使用的默认语言
    * **userAgent**：返回由客户机发送服务器的 user-agent 头部的值
    * **userLanguage**：返回 OS 的自然语言设置
* 对象方法:
    * **javaEnabled()**：规定浏览器是否启用 Java
    * **taintEnabled()**：规定浏览器是否启用数据污点 (data tainting)

#### Screen：有关客户端显示屏幕的信息
* 对象属性:
    * **width|height**：返回显示器屏幕的宽度|高度
    * **availWidth|availHeight**：返回显示屏幕的宽度|高度 (除 Windows 任务栏之外)
    * **bufferDepth**：设置或返回调色板的比特深度
    * **colorDepth**：返回目标设备或缓冲器上的调色板的比特深度
    * **deviceXDPI|deviceYDPI**：返回显示屏幕的每英寸水平|垂直点数
    * **fontSmoothingEnabled**：返回用户是否在显示控制面板中启用了字体平滑
    * **logicalXDPI|logicalYDPI**：返回显示屏幕每英寸的水平|垂直方向的常规点数
    * **pixelDepth**：返回显示屏幕的颜色分辨率（比特每像素）
    * **updateInterval**：设置或返回屏幕的刷新率

#### History：包含用户（在浏览器窗口中）访问过的URL
* 对象属性:
    * **length**：返回浏览器历史列表中的 URL 数量
* 对象方法:
    * **back()**：加载 history 列表中的前一个 URL
    * **forward()**：加载 history 列表中的下一个 URL
    * **go(number|URL)**：加载 history 列表中的某个具体页面

#### Location：包含有关当前URL的信息
* 对象属性:
    * **hash**：设置或返回从井号 (#) 开始的 URL（锚）
    * **host**：设置或返回主机名和当前 URL 的端口号
    * **hostname**：设置或返回当前 URL 的主机名
    * **href**：设置或返回完整的 URL
    * **pathname**：设置或返回当前 URL 的路径部分
    * **port**：设置或返回当前 URL 的端口号
    * **protocol**：设置或返回当前 URL 的协议
    * **search**：设置或返回从问号 (?) 开始的 URL（查询部分）
* 对象方法:
    * **assign(URL)**：加载新的文档
    * **reload(force)**：重新加载当前文档
    * **replace(newURL)**：用新的文档替换当前文档
