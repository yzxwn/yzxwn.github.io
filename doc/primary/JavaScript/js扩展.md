## js扩展

* [this](#this)
* [继承与原型链](#继承与原型链)
* [闭包](#闭包)
* [事件机制](#事件机制)
* [Event Loop](#EventLoop：事件循环)
* [复制](#复制)
* [系统检测](#系统检测)
* [元素距离顶部高度](#元素距离顶部高度)
* [节流函数](#节流函数)
* [深拷贝浅拷贝](#深拷贝浅拷贝)
* [跨域/代理](#跨域/代理)

* 纯函数：相同的输入，永远会得到相同的输出，而且没有任何可观察的副作用（Object.freeze()：冻结对象，无法冻结嵌套的对象）
* 函数记忆：主要通过存储代价高的函数调用的结果，当需要执行同样的计算时直接返回已经缓存的结果，来加速计算机程序运行
* 高阶函数：接收一个或多个函数作为参数，并返回一个新函数
* 函数组合：将两个函数组合成一个函数，让代码从右向左运行，而不是由内而外运行，可读性大大提升
* javascript:：伪协议，表示在触发默认动作时，执行一段JavaScript代码（平稳退化（支持搜索机器人）：在不支持这个协议或者禁用javascript的浏览器中也能正常执行）
* 函数柯里化：把接受多个参数的函数变换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数(延迟执行，有助于提升函数的复用性)
    * 将多元函数转换为一元函数
    * 核心思想：降低通用性，提高适用性
    * 特点：把一个函数分成多步执行，避免重复计算和多次判断，提高性能，提前获取参数，缓存参数延迟执行，用空间换时间
        * 参数复用：如果是相同参数，在计算之后不需要重新传值计算（提高性能）
        * 提前返回：避免多次调用多次内部判断，可以直接把第一次判断的结果返回外部接收（提高性能）
        * 延迟执行：避免重复执行程序，等真正需要结果的时候，再执行
* 反柯里化：创建一个适用范围更广的函数
* 偏函数：固定函数的某一个或几个参数，返回一个新的函数来接收剩下的变量参数

#### this
```
this，函数执行的上下文，可以通过apply，call，bind改变this的指向。
对于匿名函数或者直接调用的函数来说，this指向全局上下文（浏览器为window，nodejs为global），
剩下的函数调用，那就是谁调用它，this就指向谁。
当然还有es6的箭头函数，箭头函数的指向取决于该箭头函数声明的位置，在哪里声明，this就指向哪里。
apply 和 call 的区别是 call 方法接受的是若干个参数列表，而 apply 接收的是一个包含多个参数的数组
bind 接受的是若干个参数列表，是创建一个新的函数，我们必须要手动去调用
```
#### 继承与原型链
[文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
```
//Object.prototype：表示 Object 的原型对象
//Object.__proto__：指向对应的构造函数的prototype属性
//Object.getPrototypeOf(obj)：返回指定对象的原型（内部[[Prototype]]属性的值）
//prototypeObj.isPrototypeOf(object)：一个对象是否存在于另一个对象的原型链上
//object instanceof constructor：测试构造函数的prototype属性是否出现在对象的原型链中的任何位置
function Person() {
}
var person1 = new Person();
person1.__proto__ === Person.prototype // true
person1 instanceof Person // true
Person.prototype.isPrototypeOf(person1) // true
Object.getPrototypeOf(person1) === Person.prototype // true
Person.prototype.constructor === Person // true
person1.constructor === Person  // true
```
#### 闭包
```
有权访问另一个函数作用域中的变量的函数（内部函数被保存到外部）
作用：
1.在外部获取函数体内部的局部变量
2.维持函数中的局部变量在内存中不被销毁，可能造成内存泄漏
3.避免全局冲突，防止污染，保证内部变量的安全
```
#### 事件机制
```js
捕获阶段->目标阶段->冒泡阶段
element.addEventListener(event, function, useCapture) //useCapture:false(冒泡)，true(捕获)
//阻止冒泡
e.stopPropagation?e.stopPropagation():window.event.cancelBubble = true;
//阻止浏览器默认行为
e.preventDefault?e.preventDefault():window.event.returnValue=false;
事件代理/事件委托：利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件（把事件委托到其父对象上）
```
#### EventLoop：事件循环
```js
当一个任务执行结束后，当当前的微任务队列为空时，再去执行宏任务队列中的任务
主线程->宏任务
setTimeout、click、渲染html文档
异步任务->任务队列（微任务队列）
promise、MutationObserver
```
#### 复制
```js
// 创建'虚拟'DOM
const input = document.createElement('input');
document.body.appendChild(input);
input.setAttribute('value', "内容内容");
input.select();
if (document.execCommand('copy')) {
    document.execCommand('copy');
    console.log("复制成功");
}
// 删除'虚拟'DOM
document.body.removeChild(input)
```

#### 系统检测
**1、浏览器**
```js
getBroswer = () =>{
    let sys = {};
    let ua = navigator.userAgent.toLowerCase();
    let s;
    (s = ua.match(/edge\/([\d.]+)/)) ? sys.edge = s[1] :
        (s = ua.match(/rv:([\d.]+)\) like gecko/)) ? sys.ie = s[1] :
            (s = ua.match(/msie ([\d.]+)/)) ? sys.ie = s[1] :
                (s = ua.match(/firefox\/([\d.]+)/)) ? sys.firefox = s[1] :
                    (s = ua.match(/chrome\/([\d.]+)/)) ? sys.chrome = s[1] :
                        (s = ua.match(/opera.([\d.]+)/)) ? sys.opera = s[1] :
                            (s = ua.match(/version\/([\d.]+).*safari/)) ? sys.safari = s[1] : 0;

    if (sys.edge) return { broswer : "Edge", version : sys.edge };
    if (sys.ie) return { broswer : "IE", version : sys.ie };
    if (sys.firefox) return { broswer : "Firefox", version : sys.firefox };
    if (sys.chrome) return { broswer : "Chrome", version : sys.chrome };
    if (sys.opera) return { broswer : "Opera", version : sys.opera };
    if (sys.safari) return { broswer : "Safari", version : sys.safari };
    return { broswer : "", version : "0" };
};
```
**2、检测**
```js
const devices = navigator.mediaDevices.enumerateDevices();
const audios = [], cameras = [], speaks = [];
devices.then((stream) => {
    (stream||[]).map((device)=>{
        switch (device.kind){
            case "audioinput":
                audios.push(device);//麦克风
                break;
            case "videoinput":
                cameras.push(device);//摄像头
                break;
            case "audiooutput":
                speaks.push(device);//扬声器
                break;
            default:
                break;
        }
    });
});
devices.catch((err) => { console.log(err); });
```
**3、扬声器**
```js
//<audio controls={false} ref={ref=>this.audioPlay=ref}/>
const speakerVolume = 0.6;
//播放/暂停声音
playAudio=()=>{
    if(!this.audioPlay.paused){
        this.audioPlay.pause();
        this.audioPlay.load();
    }else{
        this.audioPlay.src="...mp3";
        this.audioPlay.volume=speakerVolume;//音量0~1
        this.audioPlay.play();
    }
};
//减小音量
downSpeakerVolume=()=>{
    const {speakerVolume}=this.state;
    if(speakerVolume*100>0){
        let volume=(speakerVolume*100-1)/100;
        volume=volume>1?volume/100:volume;
        speakerVolume:volume;
        this.audioPlay.volume=volume;
    }
};
//增大音量
upSpeakerVolume=()=>{
    const {speakerVolume}=this.state;
    if(speakerVolume*100<100){
        let volume=(speakerVolume*100+1)/100;
        volume=volume>1?volume/100:volume;
        speakerVolume:volume;
        this.audioPlay.volume=volume;
    }
};
//手动拖动音量
changeSpeakerVolume=(value:any)=>{
    const volume=parseInt(value);
    if(volume<=100&&volume>=0){
        speakerVolume = volume/100;
        this.audioPlay.volume=volume/100;
    }
};
```
**4、麦克风**
```js
//初始化
let micp = "";
const p = navigator.mediaDevices.getUserMedia({
    audio: true,
    video: false
});
p.then((stream) => {
    micp = stream;
    //此处显示音频变化
});
p.catch((e) => {
    let audioError;
    const errorName=e.name;
    if(errorName==="NotAllowedError"||errorName==="PermissionDeniedError"){
        audioError={
            name:"NotAllowedError",
            message:"当前浏览器已禁止访问麦克风，请设置为允许后刷新页面"
        };
    }else if(errorName==="DevicesNotFoundError"||errorName==="NotFoundError"){
        audioError={
            name:"DevicesNotFoundError",
            message:"未检测到麦克风"
        };
    }else if(errorName==="NotSupportedError"){
        audioError={
            name:"NotSupportedError",
            message:"该浏览器不支持使用麦克风"
        };
    }else if(errorName==="NotReadableError"||errorName==="TrackStartError"){
         audioError={
             name:"TrackStartError",
             message:"麦克风被其他程序占用"
         };
    }else{
        audioError=e;
    }
    console.log(audioError.message);
});
//切换麦克风
changMic = (deviceId) => {
    navigator.getUserMedia({audio: {
        deviceId:{
            exact:deviceId
        }
    }, video: false}, (stream) => {
        micp = stream;
        //此处显示音频变化
    }, (error) => {
        console.log("navigator.getUserMedia error:", error)
    })
};
//关闭麦克风
micp.getTracks().forEach(function(track) {
    track.stop();
});
//处理音频数据
const audioContext = new AudioContext({
    latencyHint: 'interactive',
    sampleRate: 44100
});//页面关闭之后需要执行audioContext.close();否则在360中执行6次之后报错
if(audioContext.state === "suspended"){
    audioContext.resume();
}
const input = audioContext.createMediaStreamSource(stream);
const processor = audioContext.createScriptProcessor(256, 1, 1);
input.connect(processor);
processor.connect(audioContext.destination);
processor.onaudioprocess = (e) => {
    filterData(e.inputBuffer.getChannelData(0));//number[]
};
const filterData=(data)=>{
    let length=data.length;
    let result=[];
    for(let i =0;i<length;i+=4){
        result.push(data.slice(i,i+4));
    }
    return result.map((arr)=>{
        let ave=arr.reduce(function(prev, curr){
            return prev + curr;
        })/4;
        const num=Math.min(Math.abs(Math.ceil(1000* ave)),this.rateMax);
        let pixal=this.canvasHeight/this.rateMax;
        pixal=((this.rateMax-num)/(this.rateMax/2))*pixal+pixal;
        return Math.abs(num*pixal/2);
    });
};
```
**5、摄像头**
```js
//初始化
let video = "";
const ratio = {
    普清: {width: 320, height: 180},
    标清: {width: 640, height: 360},
    高清: {width: 1280, height: 720},
};
const p = navigator.mediaDevices.getUserMedia({
    video: {
        deviceId:{
            exact:deviceId//摄像头id
        },
        width:{
            ideal:width//不同分辨率
        },
        height:{
            ideal:height//不同分辨率
        },
        aspectRatio: 1.777777778//画面比例
    },
    audio: false
});
p.then((stream) => {
    video = stream;
    //在<video/>内显示画面
});
p.catch((e) => {
    let videoError;
    const errorName=e.name;
    if(errorName==="NotAllowedError"||errorName==="PermissionDeniedError"){
        //权限未允许
        videoError={
            name:"NotAllowedError",
            message:"当前浏览器已禁止访问摄像头，请设置为允许后刷新页面"
        };
    }else if(errorName==="DevicesNotFoundError"||errorName==="NotFoundError"){
        videoError={
            name:"DevicesNotFoundError",
            message:"未检测到摄像头"
        };
    }else if(errorName==="NotSupportedError"){
        videoError={
            name:"NotSupportedError",
            message:"该浏览器不支持使用摄像头"
        };
    }else if(errorName==="NotReadableError"||errorName==="TrackStartError"){
         videoError={
             name:"NotReadableError",
             message:"摄像头被其他程序占用"
         };
    }else{
        videoError=e;
    }
    console.log(videoError.message);
});
//切换摄像头
changMic = (deviceId) => {
    navigator.getUserMedia({
        video:{
            deviceId:{
                exact:deviceId//摄像头id
            },
            width:{
                ideal:width//不同分辨率
            },
            height:{
                ideal:height//不同分辨率
            },
            aspectRatio: 1.777777778
        },
        audio: false
    }, (stream) => {
        video = stream;
        //在<video/>内显示画面
    }, (error) => {
        console.log("navigator.getUserMedia error:", error)
    })
};
//关闭摄像头
video.getTracks().forEach(function(track) {
    track.stop();
});
//在<video/>内显示画面
setTimeout(()=>{
    if(stream&&stream.active){
        videoDocument.srcObject = stream;
        //videoDocument.src = window.URL.createObjectURL(stream); 在cream7.1报错
        videoDocument.onloadedmetadata = () => {
            videoDocument.play();
        };
    }else{
        alert("摄像头被其他程序占用");//在cream7.1中不报错，stream.active===false会延时
    }
},1000);
```

#### 元素距离顶部高度

```js
function getTop(el, initVal) {
    let top = el.offsetTop + initVal;
    if (el.offsetParent !== null) {
        top += el.offsetParent.clientTop;
        return getTop(el.offsetParent, top);//尾递归
    } else {
        return top;
    }
}
//等于 e1.getBoundingClientRect().top
```

#### 函数节流/函数防抖
```js
//节流：持续触发事件，每隔一段时间，只执行一次事件（鼠标移动事件回调）
function throttle(fn, gapTime) {
    let oldTime = 0; // 保证第一次一定执行
    return function () {
        const newTime = new Date().getTime();
        if(newTime - oldTime > gapTime) {
            fn();
            oldTime = newTime;
        }
    };
}
function fn() {
    console.log(`当前秒数：${new Date().getSeconds()}`);
}
setInterval(throttle(fn, 3000), 1000);//1秒执行一次变成3秒执行一次

//防抖：在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时（输入触发搜索事件）
function debounce(fn, wait) {
    let timer = null;
    return function () {
        clearInterval(timer);
        timer = setTimeout(fn.bind(this,...arguments),wait);
    }
}
function fn() {
    console.log(`当前秒数：${new Date().getSeconds()}`);
}
const action = debounce(fn, 2000);
```

#### 深拷贝浅拷贝
[文档](https://juejin.im/post/59ac1c4ef265da248e75892b)
```
栈：自动分配的内存空间，它由系统自动释放
基本数据类型：undefined，boolean，number，string，null
基本数据类型存放在栈中：存放在栈内存中的简单数据段，数据大小确定，内存空间大小可以分配，是直接按值存放的，所以可以直接访问。
基本数据类型值不可变
基本类型的比较是值的比较
堆：动态分配的内存，大小不定也不会自动释放
引用数据类型：array，object，function
引用类型存放在堆中：变量实际上是一个存放在栈内存的指针，这个指针指向堆内存中的地址。每个空间大小不一样，要根据情况开进行特定的分配。
引用类型值可变
引用类型的比较是引用的比较
深拷贝：将 B 对象拷贝到 A 对象中，包括 B 里面的子对象
浅拷贝：将 B 对象拷贝到 A 对象中，但不包括 B 里面的子对象
```

#### 跨域/代理
```
同源策略："协议+域名+端口"三者相同
允许跨域加载资源：<img src=XXX>、<link href=XXX>、<script src=XXX>、<iframe src=XXX>
//关闭同源策略：chrome.exe
jsonp：使用<script>元素作为Ajax传输的技术称为JSONP，利用script标签可跨域的特点，在跨域脚本中可以直接回调当前脚本的函数，JSONP请求一定需要对方的服务器做支持才可以（响应数据是经过JSON编码的）
cors：服务器设置HTTP响应头中Access-Control-Allow-Origin的值，解除跨域限制
iframe：postMessage传递数据、window.name 传值、location.hash 传值、设置document.domain（只能用于二级域名相同的情况下）
websocket：允许跨域通讯
Node 中间件：代理服务器
nginx：高性能的HTTP和反向代理服务器，可以顺便修改 cookie 信息
proxy：webpack配置代理
```

