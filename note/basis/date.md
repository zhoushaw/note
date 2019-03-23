## 一、创建日期

### 日期声明

```javascript
new Date(); // 获取当前时间
new Date(1453094034000); // 将时间戳转换成日期，需传入毫秒时间戳
new Date(1995, 11, 17); // 传入时间转换成Date
Date.now(); // 将当前时间转换成时间戳，转换成毫秒时间戳
```

### 获取时间

#### 获取天


```javascript
let Date = new Date(); // 获取当前时间
let day = Date.getDate();
```

#### 获取周几


```javascript
let Date = new Date(); // 获取当前时间
let day = Date.getDay();
```

#### 获取小时

```javascript
let Date = new Date(); // 获取当前时间
let day = Date.getHours();
```

#### 获取分钟

```javascript
let Date = new Date(); // 获取当前时间
let day = Date.getMinutes();
```

#### 获取秒

```javascript
let Date = new Date(); // 获取当前时间
let day = Date.getSeconds();
```



#### 将时间转换成毫秒时间戳

```javascript
let Date = new Date(); // 获取当前时间
let millSeconds = Date.setMilliseconds();
```

## 二、使用场景

#### 倒计时