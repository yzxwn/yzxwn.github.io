## sass

* 跳出嵌套：
```css
.parent {
    background:#f00;
    @at-root .child {
            width:300px;
    }
    @at-root {
        .child1 {
            width:300px;
        }
        .child2 {
            width:300px;
        }
    }
}
```