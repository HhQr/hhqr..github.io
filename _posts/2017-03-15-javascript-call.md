---
layout: post
title: Javascript：揭秘call
summary: 深入了解call，手写call方法
featured-img: javascript
categories: Javascript
---
一、call方法主要有以下两个作用：

1.call改变了this的指向  

2.函数执行了  


二、call的应用场景：
1.验证类型  

例如 验证是否是数组  


```javascript
function isArray(obj){ 
    return Object.prototype.toString.call(obj) === '[object Array]';
}
```
如图所示：

![]({{site.url}}{{site.baseurl}}/assets/img/no_subject/call_1.jpg)  

2.调用父构造函数实现继承  


三、手写实现call方法

1.判断调用时否是函数

2.context 为可选参数，如果不传则为window

3.给context创建一个fn属性，并将其值赋值为需要调用的函数（使用this获取需要调用的函数）

如图所示：

![]({{site.url}}{{site.baseurl}}/assets/img/no_subject/call_2.jpg)

4.将传入的参数剥离出来作为 执行函数的参数 使用arguments对象

5.调用函数，并将对象上的函数删除

```javascript
Function.prototype.call1 = function(context) {
    //1.判断调用时否是函数
    if(typeof this !== 'function'){
        throw new  TypeError('Error')
    }
    //2.context 为可选参数，如果不传则为window
    context = context || window
    //3.给context创建一个fn属性，并将其值赋值为需要调用的函数（使用this获取需要调用的函数）
    context.fn = this;
    //4.将传入的参数剥离出来作为 执行函数的参数 使用arguments对象
    const args = [...arguments].slice(1);
    //5.调用函数，并将对象上的函数删除
    const result = context.fn(...args);
    delete context.fn;
    return result;
}
```
使用自定义call方法

![]({{site.url}}{{site.baseurl}}/assets/img/no_subject/call_3.jpg)

以上是全部内容！