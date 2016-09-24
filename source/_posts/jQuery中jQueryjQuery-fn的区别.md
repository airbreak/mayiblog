---
title: jQuer $和 $.fn的区别
date: 2016-04-13 23:55:21
tags:
---
讨论下jQuery中$和$.fn的区别。  
我们先看几个实例：    

	$(function() {
		/*写法一 $.addNum*/
		$.addNum=function(a,b) {
			return a+b;
		}
		console.log($.addNum(10,20));  //30

		/*写法二 $.extend（）*/
		$.extend({
			diffNum:function(a,b) {
				return a-b;
			}
		});
		console.log($.diffNum(10,20)); //-10

		/*写法四 $.fn*/
		$.fn.times=function(a,b) {
			return a*b;
		}
		console.log($('body').times(3,5));  //15

		/*写法二 $.fn.extend（）*/
		$.fn.extend({
			divide:function(a,b) {
				return a/b;
			}
		});
		console.log($('body').divide(20,10)); //1
	});
上面的实例中，我们看到给jquery添加一个自己定义的方法有四种方式：    

1. $.a 这样的方式， 通过$.a( )来调用。  
2. $.extend({ a:function() }) 方式， 通过$.a( )来调用。  
3. $.fn.a 方式，通过jquery DOM 对象 的 a( )来调用。  
4. $.fn.extend({ a:function() }) 方式，通过jquery DOM 对象 的 a( )来调用。  

我们可以看出，1、2的方式基本一致，只是定义方法时的写法的不同。3、4的也基本一致，也是定义方法方式不同。    

我们通过调用方式的不同，着重解释1、2和3、4的区别：  
 * 1、2方法给jquery添加的是“静态方法”。  
 * 3、4 方法添加的则是 实例方法（非静态方法）。  
用C#语法来说就是，第一个是不用实例化类就可以直接调用的，第二是要实例化类之后，通过类来调用。$('body') 的意思就是将一个javacript对象转换成jquery对象，所以能使用实例的方法。  
   
   我们拓展下，这个$.fn 是什么东西，看jquery的源码，我们可以看到  
	  
	   jQuery.fn = jQuery.prototype = {};  
   了解过prototype就一定知道这个是jquery的原型，给原型添加一个方法。
  
	
