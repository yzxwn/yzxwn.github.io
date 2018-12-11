## js技巧

[小结](#小结)、
[代理](#代理)、
[数组去重](#数组去重)、
[复制](#复制)、
[系统检测](#系统检测)

#### 小结
* **this**
```
this，函数执行的上下文，可以通过apply，call，bind改变this的指向。
对于匿名函数或者直接调用的函数来说，this指向全局上下文（浏览器为window，nodejs为global），
剩下的函数调用，那就是谁调用它，this就指向谁。
当然还有es6的箭头函数，箭头函数的指向取决于该箭头函数声明的位置，在哪里声明，this就指向哪里。
```
* **图片懒加载**
```

```
* **服务端渲染（SSR）**
```

```
* **MVC MVVM**
```

```
* **serves work**
```

```
* **跨域**
```

```

#### 代理

[原文](https://segmentfault.com/a/1190000016468988)

#### 数组去重

[原文](https://segmentfault.com/a/1190000016418021)

**1、es6 set去重**

代码最少，无法去掉空对象
```js
function unique (arr) {
  return Array.from(new Set(arr))
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
console.log(unique(arr))
 //[1, "true", true, 15, false, undefined, null, NaN, "NaN", 0, "a", {}, {}]
```

**2、for循环，splice去重**
```js
function unique(arr){
        for(var i=0; i<arr.length-1; i++){
            for(var j=i+1; j<arr.length; j++){
                if(arr[i]==arr[j]){         //第一个等同于第二个，splice方法删除第二个
                    arr.splice(j,1);
                    j--;
                }
            }
        }
return arr;
}
var arr = [1,1,'true','true',true,true,15,15,false,false, undefined,undefined, null,null, NaN, NaN,'NaN', 0, 0, 'a', 'a',{},{}];
    console.log(unique(arr))
    //[1, "true", 15, false, undefined, NaN, NaN, "NaN", "a", {…}, {…}]     //NaN和{}没有去重，两个null直接消失了
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

#### web sorket

```js

```
