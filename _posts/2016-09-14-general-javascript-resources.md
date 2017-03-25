---
layout: post
title: JavaScript This详解
category: 资源
tags: JavaScript
keywords: JavaScript
description: 
---
## THIS指向，来试试吗？
   this的指向问题，想必大家都很熟悉了。
   js作用域是词法作用域，即书写时决定的变量的可见性，
   又由于函数是对象，是引用类型，会产生闭包现象。
   而动态作用域是取决于运行时的，this是最接近动态作用域这个概念的。
   因此this指向，取决于函数的调用形式。
   四种调用形式（函数、方法、call、new），四种指向。

## 我出几道题，考考大家
## 1.this丢失问题:
    var a = {
    value: 'a',
    fn:function() {
    alert(this.value);
    }
    };
    var b = a.fn;
    b();
	alert: undefined
### 上面明白的话，下面这个呢:
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	setTimeout(a.fn);

### 可以认为是作为“函数”调用。换种形式写呢：
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	var b;
	(b = a.fn)();
### 没问题吧？再来个：
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	var b = {
	    value: 'b'
	};
	(b.fn = a.fn)();
### 至于这个为啥this指向window，可以认为进行表达式求值时，返回的是个函数，因此作为函数调用，再看
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	(a.fn = a.fn)();
	(a.fn, a.fn, a.fn)();
### 哈哈，那么下面这个别晕菜：
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	(a.fn)();
## 2.bind绑定问题
	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	var b = {
	    value: 'b'
	};
	a.fn = a.fn.bind(b);
	a.fn();
	绑定过了，就不能改了？

	var a = {
	    value: 'a',
	    fn:function() {
	        alert(this.value);
	    }
	};
	var b = {
	    value: 'b'
	};
	a.fn = a.fn.bind(b);
	new a.fn();
### 3.ES6的箭头函数
	我们知道如下的this指向window

	var fn = function() {
	    setTimeout(function() {
	        alert(this.value)
	    });
	};
	fn.call({value:'a'});

	但对应的箭头函数呢？

	var fn = function() {
	    setTimeout(() => {
	        alert(this.value)
	    });
	};
	fn.call({value:'a'});

### 以上总总有感于《你不知道的JavaScript》，
	书中关于this的介绍还是很详细的。
	还起了几个名字呢？
	默认绑定（函数调用）,
	隐式绑定（方法调用）,
	显式绑定（call或apply）,
	new绑定（new构造函数）
	还像模像样的给出了调用优先级(上面四种逆序)。。。
	此书有英文版(共六本)，可以去啃啃。