## js技巧

* [复制](#复制)
* [系统检测](#系统检测)
* [元素距离顶部高度](#元素距离顶部高度)
* [节流函数](#节流函数)


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

#### 节流函数

```js
/**
 * 持续触发事件，每隔一段时间，只执行一次事件。
 * @param fun 要执行的函数
 * @param delay 延迟时间
 * @param time 在 time 时间内必须执行一次
 */
function throttle(fun, delay, time) {
    var timeout;
    var previous = +new Date();
    return function () {
        var now = +new Date();
        var context = this;
        var args = arguments;
        clearTimeout(timeout);
        if (now - previous >= time) {
            fun.apply(context, args);
            previous = now;
        } else {
            timeout = setTimeout(function () {
                fun.apply(context, args);
            }, delay);
        }
    }
}
window.addEventListener('scroll', throttle(fun, 200, 1000), false);
```
