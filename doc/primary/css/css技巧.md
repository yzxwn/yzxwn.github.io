## css技巧

[css水平垂直居中](https://segmentfault.com/a/1190000016389031)

[伸缩布局（flex）](https://www.cnblogs.com/Assist/p/9682076.html)

#### 文字省略号
```
// css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
width: 60px;
```

#### 修改checkbox样式
```
// html
<label>
    <input type="checkbox"/>
    <div class="show-box"/>
    <span>复选框</span>
</label>
// scss
label {
    position: relative;
    cursor: pointer;
    input{
        display: none;//隐藏默认样式
    }
    input:checked + .show-box {//选中时样式
        background: #09ca51;
        border: 0;
    }
    &>span{
        display: inline-block;
        margin: 0 10px 0 18px;
    }
    .show-box {//未选中时样式
        position: absolute;
        top: 3px;
        left: 0;
        width: 14px;
        height: 14px;
        border-radius: 2px;
        border: 1px solid #e8e8e8;
        background: white;
        &:before {//选中时勾的样式
            content: '';
            position: absolute;
            top: 2px;
            left: 4px;
            width: 5px; // 勾的短边
            height: 8px; // 勾的长边
            border: 1px solid white; // 勾的颜色
            border-width: 0 2px 2px 0; // 勾的宽度
            transform: rotate(45deg); // 定制宽高加上旋转可以伪装内部的白色勾
        }
    }
}
```