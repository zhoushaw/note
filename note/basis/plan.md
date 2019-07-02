## 横屏处理


```
var screenDirection = window.matchMedia("(orientation: portrait)");

screenDirection.addListener(handleOrientationChange);

handleOrientationChange(screenDirection);

function handleOrientationChange(screenDirection) {
    var width = document.documentElement.clientWidth

    var height = document.documentElement.clientHeight;
    var $print = document.querySelector('body');
    if (screenDirection.matches) {
        /* The device is currently in portrait orientation */
        /* 竖屏处理事件 */
        $print.style.position = 'absolute';
        $print.style.width = width + 'px';
        $print.style.height = height + 'px';
        $print.style.top = 0
        $print.style.left = 0
        $print.style.transform = 'none'
        $print.style.transformOrigin = '50% 50%'
    } else {
        /* The device is currently in landscape orientation */
        /* 横屏屏处理事件 */
        $print.style.position = 'absolute';
        $print.style.width = height + 'px';
        $print.style.height = width + 'px';
        $print.style.top = (height - width) / 2 + 'px';
        $print.style.left = 0 - (height - width) / 2 + 'px';
        $print.style.transform = 'rotate(-90deg)'
        $print.style.transformOrigin = '50% 50%'
    }
}
```


## 滚动加载

### 判断页面是否滑动到底部

```
let clientHeight = document.documentElement.clientHeight;
let scrollTop = document.documentElement.scrollTop||document.body.scrollTop;
let scrollHeight = document.body.scrollHeight;


if(scrollTop + clientHeight >= scrollHeight){
    // 到达底部
}
```

### vue配置公共mixin

```
//  globalMixin.js
import Utils from 'utils';

export default {
    mounted  () {
        if (this.isEnd || !this.scrollEnd) return;
        window.addEventListener('scroll', Utils.debounce(this.scrollFn, 200));
    },
    methods: {
        // 底部滚动
        scrollFn (event) {
            // 已经结束、活着没有滚动结束回调不执行方法
            if (this.isEnd || !this.scrollEnd) return;

            let clientHeight = document.documentElement.clientHeight;
            let scrollTop = document.documentElement.scrollTop||document.body.scrollTop;
            let scrollHeight = document.body.scrollHeight;

            // 由于pc自带底部banner减去底部banenr高度
            if(scrollTop + clientHeight >= scrollHeight - 594){
                this.scrollEnd()
            }
        }
    }
}

```

> 使用

```
// app.vue
export default {
    data () {
        return {
            isEnd: false
        },
        getOriginDarenList () {

        },
        scrollEnd () {
            this.getOriginDarenList();
        }
    },
}
```

## iphone，输入内容后，页面不回滚


具体表现：
1. iphoneX在微信内的h5，点击input框后，页面会向上滚动，失去焦点页面不会回滚
2. 其他iphone在微信内的h5，点击input框后，失去焦点后，页面会回滚，实际dom没回滚


```
# 在失去焦点是，触发滚动到顶部解决
window.scrollTo(0,0)
```