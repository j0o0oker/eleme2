# eleme

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

第一天
 1 需求分析
     *主页面
		 ---header
			---推荐页
				---模态框
		 ---countent
			---快速导航
			---商品简单信息
		 ---footer
			---购物车
     *商家详情
	 *评价
	 *购物车
	 
	 结果：第五节完成
	 疑问：1 mock后台数据的过程不明白

第二天  
	---完成header组件
	
	
	结果：header交互效果实现，样式没写
	疑问：1 组件里的this不就是指向组件本身吗，为什么打印data里的数据结果是一个对象(..__ob__.dep)；
		 2 用display：inner-block是怎样
		 
		 

第三天
	---goods组件
	
	
	
	结果：基础布局
	疑问：关于stylus
	关于实现手机一像素boeder
	
	

第四天
	---goods组件
	结果：利用beter-scroll插件实现页面滚动，用手机端查看发现头部组件并没有实现响应式
	疑问：复习理解回调函数
	     学习stylus



第五天
	---goods组件
	结果：完成菜单和食物列表的联动,购物车组件内容
	疑问：手机端查看响应式出错，监听不到点击事件