---
title: js的命名提升
date: 2016-04-03 19:08:49
tags: js
---
 <font color=#e78170>jimmy</font>   
 
怎么理解js的命名提升,请大家看这个代码片段：         
 
    var num1 = 10;  
    
    function test1(){
        if(num1==10){
            num1 = 1;
        }
        else{
            num1 = 2;
        }
        return num1;
    }
    test(); //返回1  
    
       var num1 = 10;  
    function test(){
        if(num1==10){
            var num1 = 1;
        }
        else{
            var num1 = 2;
        }
        return num1;
    }
    test(); //返回2  
    var num1 = 10;  
    
    function test1(){
        if(num1==10){
            num1 = 1;
        }
        else{
            num1 = 2;
        }
        return num1;
    }
    test(); //返回1  
    

