## 一、常见dom操作

### 页面是否达到底部

```javascript

let clientHeight = document.documentElement.clientHeight; // 可视区高度
let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;// 页面滚动高度
let scrollHeight = document.body.scrollHeight; // 总高度

if(scrollTop + clientHeight >= scrollHeight){
    // 页面达到底部
}
```