---
title: angular-ui-router基本使用
date: 2016-09-26 00:29:23
tags: angularjs
---
 <font author color=#e78170>**jimmy** </font>    
 
最近做公司项目时要使用 <font color="#f38c00" >angularjs</font> 框架，所以认真地研究了angularjs。  

既然是mvc框架，那么路由肯定是要理解的了。看了一些教程都推荐使用<font color="#f38c00" > angular-ui-router </font>这个第三方的库。按照网上的说法，说angularjs 自带的<font color="#f38c00" >  angular-route </font>，不合适做多层的嵌套。如下图的嵌套

![image](http://7xqnxu.com1.z0.glb.clouddn.com/angular-ui-router1.gif)

有一个固定的头部菜单，然后点击UserManage时的页面，有左右菜单。相当于上下，然后左右的布局。

据说这个效果要使用angular-route实现，比较困难，我没有尝试。直接使用了angular-ui-router，也没有网上说的那么简单，也花了点时间摸索。  

#### 示例站点说明

新建实例站点目录，我的目录结构如图，比较简陋，只是为了说明 angular-ui-router 的用法。

![image](http://7xqnxu.com1.z0.glb.clouddn.com/angular-ui-route2.png)  

**js文件夹**：主要存放基本的js文件，其中config.js就是我们自己的重点——<font color="#f38c00" >路由配置</font>，具体的内容后面说。  

**pages文件夹**：存放内部的各个跳转的页面，包括二层的导航页面<font color="#075b8d">  nav.html </font>、二层的<font color="#075b8d" > ui－view </font>容器页面<font color="#075b8d">  mian.html </font>和三层的用户管理的页面。

**index.html 和 index.css**：index.css就是样式文件，没什么好说的。index.html  则是网站的最外层的视图页面，装载所有的子页面。

#### 具体使用方法说明  
<font color="#E68551">在说具体的代码之前，我们先理下页面的总体结构。按照我们的示例设计图，我们将整个页面结构分成三层。如图：</font>  

![image](http://7xqnxu.com1.z0.glb.clouddn.com/angular-ui-router3.png)

 -  <font color="#59ABD0">蓝色框</font> 是我们的第一层，即页面的第一个页面视图容器。用来装载绿色框的二级页面。    
 
 -  <font color="#52A241">绿色框</font> 是我们的第二层，包括导航页面记忆对应的视图页面。也可以用来转载三级页面，如 用户管理页面。所以我们在用户管理的总页面，也写了一些 ui－view，用来转载用户管理的三级页面。  
 
- <font color="#F9CE4F">黄色框</font>是第三层，主要是用户管理的详细页面。

##### 具体说明


1. **第一层 **。下载 [angular-ui-router.js](https://pan.baidu.com/s/1eSqNED0) ，然后引用到index.html页面中，并编写index.html页面内容。具体如下：  

**html**:

	<!DOCTYPE html>
		<html lang="en" ng-app="routerApp">
			<head>
    				<meta charset="UTF-8">
    				<title>angular - ui router</title>
    				<link rel="stylesheet" href="index.css" type="text/css">
				<script type="text/javascript" src="js/angular.min.js"></script>
				<script type="text/javascript" src="js/angular-ui-router.js"></script>
				<script type="text/javascript" src="js/config.js"></script>
			</head>
			<body> 
    				<div ui-view></div>
			</body>
	</html>   
	
	
  需要使用到的 js 文件都引用进来，注意顺序不能乱。  

angular-ui-router 的原则是 使用 ui-view 这个指令作为页面的视图指令，区别于原生的 ng-view。  

这个最外层的页面很简单。

2.**第二层**。配置第二层页面，第二层包括：

*  顶部导航页面

*  Home欢迎页面

*  用户管理页面总容器
	* 左侧菜单  
	
	* 高端用户业面

	* 中端用户业面
	
	* 低端用户业面

*  设置页面
*
其中，除了顶部导航页面和用户管理页面外，其他页面都没有任何的 ui-view 配置信息。
###### 顶部导航页面：  
**html**

###### 用户管理页面如下：

**html**

	<div class="user-manage-container">
    		<div class="left-bar" ui-view="leftBar"></div>
    		<div class="user-main" ui-view="userMain"></div>       
	</div>
	
其中<font color="#075b8d" > leftBar </font>是用户管理的菜单页面，<font color="#075b8d" > userMain </font> 则是用来对应高端、中端、低端的用户详细页面
	

2. 配置<font color="#075b8d" > config.js </font>。具体如下：  

**js**:

	var routerApp=angular.module('routerApp',['ui.router']);

		routerApp.run(function($rootScope, $state, $stateParams) {
    			$rootScope.$state = $state;
    			$rootScope.$stateParams = $stateParams;
	});

	routerApp.config(function($stateProvider, $urlRouterProvider) {
    		$urlRouterProvider.otherwise('/index');
    		$stateProvider
        		.state('index',{
            			url:'/index',
            			views:{
                			'':{
                    			templateUrl:'pages/main.html'
                			},
               			   'topbar@index':{
                    			templateUrl:'pages/nav.html'
                			},
                			'main@index':{
                    			templateUrl:'pages/welcome.html'
                		},              
            		}
        	 })
        	.state('usermng',{
            		url:'/usermng',
            		views:{
                		'':{
                    		templateUrl:'pages/main.html'
                		},
                		'topbar@usermng':{
                    		templateUrl:'pages/nav.html'
                		},
                		'main@usermng':{
                    		templateUrl:'pages/usermng/usermng.html',
                		},
                		'leftBar@usermng':{
                   		   	templateUrl:'pages/usermng/leftbar.html'
                		},
                		'userMain@usermng':{
                   			templateUrl:'pages/usermng/hightendusers.html'
                		},
            		}
        })

        .state('usermng.hightendusers',{
             url:'/hightendusers' ,
             views:{
                'userMain@usermng':{
                    templateUrl:'pages/usermng/hightendusers.html'
                }
            }
        })
        .state('usermng.normalusers',{
             url:'/normalusers' ,
             views:{
                'userMain@usermng':{
                    templateUrl:'pages/usermng/normalusers.html'
                }
            } 
        })
        .state('usermng.slowusers',{
             url:'/slowusers' ,
             views:{
                'userMain@usermng':{
                    templateUrl:'pages/usermng/slowusers.html'
                }
            } 
        })
        .state('settings',{
            url:'/settings',
            views:{
                '':{
                    templateUrl:'pages/main.html'
                },
                'topbar@settings':{
                    templateUrl:'pages/nav.html'
                },
                'main@settings':{
                    template:'<div class="normal-word">这是系统设置</div>'
                }
            }
        });
	});

最后附上整个实例的源码，[这里下载](https://github.com/airbreak/angular-ui-router)
