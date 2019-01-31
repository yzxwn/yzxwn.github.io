## htmlDom对象 (文档对象模型)

* [Document](#document：每个载入浏览器的html文档都会成为document对象)
* [Element](#element：表示html元素)
* [Attribute](#attribute：表示html属性)
* [Event](#event：代表事件的状态)

#### Document：每个载入浏览器的HTML文档都会成为Document对象
* 对象集合:
    * **all[i]|all[name]|all.tags[tagname]**：提供对文档中所有 HTML 元素的访问
    * **anchors[]**：返回对文档中所有 Anchor(锚) 对象的引用
    * **applets**：返回对文档中所有 Applet 对象的引用
    * **forms[]**：返回对文档中所有 Form(表单) 对象引用
    * **images[]**：返回对文档中所有 Image 对象引用
    * **links[]**：返回对文档中所有 Area(热点) 和 Link 对象引用
* 对象属性:
    * **body**：提供对 <body> 元素的直接访问。对于定义了框架集的文档，该属性引用最外层的 <frameset>
    * **cookie**：设置或返回与当前文档有关的所有 cookie
    ```js
    //创建
    document.cookie="username=John Doe";
    //使用 expires 为 cookie 添加一个过期时间，默认情况下，cookie 在浏览器关闭时删除
    //使用 path 参数告诉浏览器 cookie 的路径，默认情况下，cookie 属于当前页面
    //删除 Cookie：设置 expires 参数为以前的时间即可
    document.cookie="username=John Doe; expires=Thu, 18 Dec 2043 12:00:00 GMT; path=/";
    //读取
    var x = document.cookie;
    ```
    * **domain**：返回当前文档的域名
    * **lastModified**：返回文档被最后修改的日期和时间
    * **referrer**：返回载入当前文档的文档的 URL
    * **title**：返回当前文档的标题
    * **URL**：返回当前文档的 URL
* 对象方法:
    * **open(mimetype,replace)**：打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出
    * **close()**：关闭用 document.open() 方法打开的输出流，并显示选定的数据
    * **write(exp1,exp2,exp3,....)**：向文档写 HTML 表达式 或 JavaScript 代码
    * **writeln(exp1,exp2,exp3,....)**：等同于 write() 方法，不同的是在每个表达式之后写一个换行符
    * **getElementById()**：返回对拥有指定 id 的第一个对象的引用
    * **getElementsByName()**：返回带有指定名称的对象集合（Collection）
    * **getElementsByTagName()**：返回带有指定标签名的对象集合（Collection）

#### Element：表示HTML元素
* 对象属性:
    * **attributes**：返回元素属性的 NamedNodeMap(属性集合)
    * **style**：设置或返回元素的 style 属性
    * **className**：设置或返回元素的 class 属性(返回class字符串)
    * **id**：设置或返回元素的 id
    * **innerHTML**：设置或返回元素的内容
    * **tagName**：返回元素的标签名（大写）
    * **title**：设置或返回元素的 title 属性
    * **ownerDocument**：返回元素的根元素（文档对象）
    * **length**：返回 NodeList 中的节点数
    * **childNodes**：返回元素子节点的 NodeList(元素中的空格被视为文本，#text节点)
    * **firstChild**：返回元素的首个子节点
    * **lastChild**：返回元素的最后一个子节点
    * **nextSibling**：返回位于相同节点树层级的下一个节点(空格返回undefined)
    * **previousSibling**：返回位于相同节点树层级的前一个元素
    * **parentNode**：返回元素的父节点
    * **nodeName**：返回元素的名称（元素节点：返回大写标签名，属性节点：返回属性的名称）
    * **nodeType**：返回元素的节点类型（元素节点：返回 1，属性节点：返回 2，文本节点：返回 3）
    * **nodeValue**：设置或返回元素节点值
    * **textContent**：设置或返回节点及其后代的文本内容（如果设置了 textContent 属性，会删除所有子节点，并被替换为包含指定字符串的一个单独的文本节点）
    * **contentEditable**：设置或返回元素的内容是否可编辑(boolean，可从父元素继承)
    * **isContentEditable**：返回元素的内容是否可编辑
    * **dir**：设置或返回元素的文本方向（text-direction）
    * **clientHeight|clientWidth**：返回元素的可见高度|宽度
    * **offsetHeight|offsetWidth**：返回元素的高度|宽度
    * **offsetLeft|offsetTop**：返回元素的水平|垂直偏移位置
    * **offsetParent**：返回元素的偏移容器
    * **scrollHeight|scrollWidth**：返回元素的整体高度|宽度
    * **scrollLeft|scrollTop**：返回元素左|上边缘与视图之间的距离
    * **tabIndex**：设置或返回元素的 tab 键控制次序
    * **accessKey**：设置或返回元素的快捷键
    ```js
    //快捷键在不同的浏览器中各有不同：
    IE, Chrome, Safari, Opera 15+: [ALT] + accesskey
    Opera prior version 15: [SHIFT] [ESC] + accesskey
    Firefox: [ALT] [SHIFT] + accesskey
    //如果超过一个元素拥有相同的快捷键，那么：
    IE, Firefox: 激活下一个被按下快捷键的元素
    Chrome, Safari: 激活最后一个被按下快捷键的元素
    Opera: 激活第一个被按下快捷键的元素

    document.getElementById('w3s').accessKey="m";
    <a id="w3s" href="http://www.w3school.com.cn/">W3School</a>
    ===
    <a id="w3s" href="http://www.w3school.com.cn/" accesskey="m">W3School</a>
    ```
    * **lang**：设置或返回元素的语言代码（language-code）
    * **namespaceURI**：返回指定节点的命名空间的 URI
* 对象方法:
    * **addEventListener(event,function,useCapture)**：向指定元素添加事件句柄
    ```js
    //参数：事件的类型，事件触发后调用的函数，布尔值用于描述事件是冒泡（false默认）还是捕获（true）
    //冒泡：内部元素的事件会先被触发，然后再触发外部元素
    //捕获：部元素的事件会先被触发，然后才会触发内部元素的事件
    //添加的事件句柄不会覆盖已存在的事件句柄，可以向一个元素添加多个事件句柄或多个同类型的事件句柄

    // IE 8
    element.attachEvent(event, function);
    element.detachEvent(event, function);
    ```
    * **removeEventListener(event,function) **：移除事件的监听（事件类型和调用的函数名都要一致）
    ```js
    //
    ```
    * **appendChild(newListItem)**：向元素添加新的子节点，作为最后一个子节点（可以插入/移动已有元素）
    * **insertBefore(newnode,existingnode)**：在指定的已有的子节点之前插入新节点（可以插入/移动已有元素）
    * **removeChild(node)**：从元素中移除子节点
    * **replaceChild(newnode,oldnode)**：替换元素中的子节点（新节点可以是文档中某个已存在的节点移动，也可创建新的节点）
    * **cloneNode(deep)**：克隆元素（创建节点的拷贝，并返回该副本，deep：boolean克隆所有后代）
    * **getAttribute(attributename)**：返回元素节点的指定属性值
    * **getAttributeNode(attributename)**：返回指定的属性节点(Attr 对象)
    * **removeAttribute(attributename)**：从元素中移除指定属性
    * **removeAttributeNode(attributename)**：移除指定的属性节点，并返回被移除的节点
    * **getElementsByTagName(tagname)**：返回拥有指定标签名的所有子元素的集合(参数值 "*" 返回元素的所有子元素)
    * **hasAttribute(attributename)**：如果元素拥有指定属性，则返回true，否则返回 false
    * **hasAttributes()**：如果元素拥有属性，则返回 true，否则返回 false
    * **hasChildNodes()**：如果元素拥有子节点，则返回 true，否则 false
    * **setAttribute(attributename,attributevalue)**：把指定属性设置或更改为指定值
    * **setAttributeNode(attributenode)**：设置或更改指定属性节点
    ```js
    var atr=document.createAttribute("class");
    atr.nodeValue="democlass";
    var h=document.getElementsByTagName("H1")[0];
    h.setAttributeNode(atr); //给h元素添加类名：democlass
    ```
    * **isEqualNode(node)**：检查两个元素是否相等
    ```
    如果下例条件为 true，则两个节点相等：
    节点类型相同
    拥有相同的 nodeName、NodeValue、localName、nameSpaceURI 以及前缀
    所有后代均为相同的子节点
    拥有相同的属性和属性值（属性次序不必一致）
    ```
    * **isSameNode(node)**：检查两个元素是否是相同的节点
    ```
    Firefox 版本 10 停止对此方法的支持，因为 DOM version 4 中已弃用该方法。
    作为替代，使用 === 来比较两节点是否相同
    ```
    * **normalize()**：合并元素中相邻的文本节点，并移除空的文本节点
    * **item(index)**：返回 NodeList 中位于指定下标的节点（childNodes.item(0) === childNodes[0]）
    * **toString()**：把元素转换为字符串
    * **compareDocumentPosition()**：比较两个元素的文档位置
    ```js
    p1.compareDocumentPosition(p2);

    返回值可能是：
    1：没有关系，两个节点不属于同一个文档。
    2：第一节点（P1）位于第二个节点后（P2）。
    4：第一节点（P1）定位在第二节点（P2）前。
    8：第一节点（P1）位于第二节点内（P2）。
    16：第二节点（P2）位于第一节点内（P1）。
    32：没有关系，或是两个节点是同一元素的两个属性。
    //返回值可以是值的组合。例如，返回 20 意味着在 p2 在 p1 内部（16），并且 p1 在 p2 之前（4）
    ```
    * **isSupported(feature,version)**：如果元素支持指定特性，则返回 true
    * **isDefaultNamespace()**：如果指定的 namespaceURI 是默认的，则返回 true，否则返回 false
    * **getFeature()**：返回实现了指定特性的 API 的某个对象
    * **getUserData()**：返回关联元素上键的对象
    * **setIdAttribute()**：
    * **setIdAttributeNode()**：
    * **setUserData()**：把对象关联到元素上的键

#### Attribute：表示HTML属性
* 对象属性:
    * **attr.isId**：如果属性是 id 类型，则返回 true，否则返回 false
    * **attr.name**：返回属性的名称
    * **attr.value**：设置或返回属性的值
    * **attr.specified**：如果已指定属性，则返回 true，否则返回 false
    * **nodemap.length**：返回 NamedNodeMap 中的节点数
* 对象方法:
    * **nodemap.getNamedItem(name)**：从 NamedNodeMap 返回指定的属性节点
    * **nodemap.item(index)**：返回 NamedNodeMap 中位于指定下标的节点
    * **nodemap.removeNamedItem(nodename)**：移除指定的属性节点
    * **nodemap.setNamedItem(node)**：设置指定的属性节点（通过名称）


#### Event：代表事件的状态
* 事件句柄:
    * **onload**：一张页面或一幅图像完成加载
    ```
    支持该事件的 HTML 标签：
    <body>, <frame>, <frameset>, <iframe>, <img>, <link>, <script>
    支持该事件的 JavaScript 对象：
    image, layer, window
    ```
    * **onabort**：图像的加载被中断(仅支持img)
    * **onerror**：在加载文档或图像时发生错误
    ```
    支持该事件的 HTML 标签：
    <img>, <object>, <style>
    支持该事件的 JavaScript 对象：
    image, window
    ```
    * **onunload**：用户退出页面
    ```
    支持该事件的 HTML 标签：
    <body>, <frameset>
    支持该事件的 JavaScript 对象：
    window
    ```
    * **onfocus**：元素获得焦点
    ```
    支持该事件的 HTML 标签：
    <a>, <acronym>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <button>,
    <caption>, <cite>, <dd>, <del>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>,
    <form>, <frame>, <frameset>, <h1> to <h6>, <hr>, <i>, <iframe>, <img>, <input>,
    <ins>, <kbd>, <label>, <legend>, <li>, <object>, <ol>, <p>, <pre>, <q>,
    <samp>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <table>, <tbody>,
    <td>, <textarea>, <tfoot>, <th>, <thead>, <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    button, checkbox, fileUpload, layer, frame, password, radio, reset, select, submit,
    text, textarea, window
    ```
    * **onblur**：元素失去焦点(与onfocus相同)
    * **onchange**：域的内容被改变
    ```
    支持该事件的 HTML 标签：
    <input>, <select>, <textarea>
    支持该事件的 JavaScript 对象：
    fileUpload, select, text, textarea
    ```
    * **onselect**：文本被选中
    ```
    支持该事件的 HTML 标签：
    <input>, <textarea>
    支持该事件的 JavaScript 对象：
    window
    ```
    * **onclick**：当用户点击某个对象时调用的事件句柄
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>, <button>,
    <caption>, <cite>, <code>, <dd>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>,
    <form>, <h1> to <h6>, <hr>, <i>, <img>, <input>, <kbd>, <label>, <legend>,
    <li>, <map>, <object>, <ol>, <p>, <pre>, <samp>, <select>, <small>, <span>,
    <strong>, <sub>, <sup>, <table>, <tbody>, <td>, <textarea>, <tfoot>, <th>,
    <thead>, <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    button, document, checkbox, link, radio, reset, submit
    ```
    * **ondblclick**：当用户双击某个对象时调用的事件句柄
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>,
    <button>, <caption>, <cite>, <code>, <dd>, <dfn>, <div>, <dl>, <dt>,
    <em>, <fieldset>, <form>, <h1> to <h6>, <hr>, <i>, <img>, <input>,
    <kbd>, <label>, <legend>, <li>, <map>, <object>, <ol>, <p>, <pre>,
    <samp>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <table>,
    <tbody>, <td>, <textarea>, <tfoot>, <th>, <thead>, <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    document, link
    ```
    * **onkeydown**：某个键盘按键被按下
    ```
    支持该事件的 HTML 标签：
    <a>, <acronym>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>,
    <button>, <caption>, <cite>, <code>, <dd>, <del>, <dfn>, <div>, <dt>, <em>,
    <fieldset>, <form>, <h1> to <h6>, <hr>, <i>, <input>, <kbd>, <label>, <legend>,
    <li>, <map>, <object>, <ol>, <p>, <pre>, <q>, <samp>, <select>, <small>,
    <span>, <strong>, <sub>, <sup>, <table>, <tbody>, <td>, <textarea>, <tfoot>,
    <th>, <thead>, <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    document, image, link, textarea

    Internet Explorer 使用 event.keyCode 取回被按下的字符，而 Netscape/Firefox/Opera 使用 event.which
    ```
    * **onkeypress**：某个键盘按键被按下并松开(与onkeydown相同)
    * **onkeyup**：某个键盘按键被松开(与onkeydown相同)
    * **onmousedown**：鼠标按钮被按下
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>, <button>,
    <caption>, <cite>, <code>, <dd>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>,
    <form>, <h1> to <h6>, <hr>, <i>, <img>, <input>, <kbd>, <label>, <legend>,
    <li>, <map>, <ol>, <p>, <pre>, <samp>, <select>, <small>, <span>, <strong>,
    <sub>, <sup>, <table>, <tbody>, <td>, <textarea>, <tfoot>, <th>, <thead>,
    <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    button, document, link
    ```
    * **onmouseup**：鼠标按键被松开(与onmousedown相同)
    * **onmousemove**：鼠标被移动
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>, <button>,
    <caption>, <cite>, <code>, <dd>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>,
    <form>, <h1> to <h6>, <hr>, <i>, <img>, <input>, <kbd>, <label>, <legend>,
    <li>, <map>, <ol>, <p>, <pre>, <samp>, <select>, <small>, <span>, <strong>,
    <sub>, <sup>, <table>, <tbody>, <td>, <textarea>, <tfoot>, <th>, <thead>,
    <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    onmousemove is, by default, not an event of any object,
    because mouse movement happens very frequently
    ```
    * **onmouseover**：鼠标移到某元素之上
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <area>, <b>, <bdo>, <big>, <blockquote>, <body>, <button>,
    <caption>, <cite>, <code>, <dd>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>,
    <form>, <h1> to <h6>, <hr>, <i>, <img>, <input>, <kbd>, <label>, <legend>,
    <li>, <map>, <ol>, <p>, <pre>, <samp>, <select>, <small>, <span>, <strong>,
    <sub>, <sup>, <table>, <tbody>, <td>, <textarea>, <tfoot>, <th>, <thead>,
    <tr>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    layer, link
    ```
    * **onmouseout**：鼠标从某元素移开(与onmouseover相同)
    * **onsubmit**：确认按钮被点击
    ```
    支持该事件的 HTML 标签：
    <form>
    支持该事件的 JavaScript 对象：
    form
    ```
    * **onreset**：重置按钮被点击(与onsubmit相同)
    * **onresize**：窗口或框架被重新调整大小
    ```
    支持该事件的 HTML 标签：
    <a>, <address>, <b>, <big>, <blockquote>, <body>, <button>, <cite>, <code>,
    <dd>, <dfn>, <div>, <dl>, <dt>, <em>, <fieldset>, <form>, <frame>, <h1> to <h6>,
    <hr>, <i>, <img>, <input>, <kbd>, <label>, <legend>, <li>, <object>, <ol>, <p>,
    <pre>, <samp>, <select>, <small>, <span>, <strong>, <sub>, <sup>, <table>,
    <textarea>, <tt>, <ul>, <var>
    支持该事件的 JavaScript 对象：
    window
    ```
* 鼠标 / 键盘属性:
    * **altKey**：返回当事件被触发时，"ALT" 是否被按下
    ```js
    event.altKey=true|false|1|0
    ```
    * **ctrlKey**：返回当事件被触发时，"CTRL" 键是否被按下
    ```js
    event.ctrlKey=true|false|1|0
    ```
    * **shiftKey**：返回当事件被触发时，"SHIFT" 键是否被按下
    ```js
    event.shiftKey=true|false|1|0
    ```
    * **metaKey**：返回当事件被触发时，"meta" 键是否被按下
    * **button**：返回当事件被触发时，哪个鼠标按钮被点击
    ```js
    event.button=0|1|2 //左键|中键|右键
    event.button=1|4|2 //IE 左键|中键|右键
    ```
    * **relatedTarget**：返回与事件的目标节点相关的节点
    ```
    对于 mouseover 事件来说，该属性是鼠标指针移到目标节点上时所离开的那个节点。
    对于 mouseout 事件来说，该属性是离开目标时，鼠标指针进入的节点。
    对于其他类型的事件来说，这个属性没有用。(不支持 IE)
    ```
    * **clientX|clientY**：返回当事件被触发时鼠标指针向对于浏览器页面（或客户区）的水平|垂直坐标
    * **screenX|screenY**：返回事件发生时鼠标指针相对于屏幕的水平|垂直坐标

