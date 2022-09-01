# uniapp商城类小程序

## 一、创建项目

创建空白uniapp项目----my-uni-shop

## 二、设置全局样式

### 1. 新建文件夹common，包含以下文件

- uni.css ---- uniapp官方css库，从uniapp示例项目中复制

- animate.css ---- 第三方css动画库

- icon.css ---- 自定义项目所需图标库

- common.css ---- 项目公共样式

- 按顺序引入到App.vue中

  ```vue
  <style>
  	/* 官方uni css */
  	@import "@/common/uni.css";
  	/* 第三方动画库 */
  	@import "@/common/animate.css";
  	/* 自定义图标库 */
  	@import "@/common/icon.css";
  	/*每个页面公共css */
  	@import "@/common/common.css"
  </style>
  ```

### 2. 引入后uni.css报错

- 原因：uni.css引入了static中的uni.ttf文件
- 解决：把static中的uni.ttf文件也复制过来

### 3. 动画库的使用

1. uniapp中使用animate.css 版本4.1.1在微信小程序中不生效解决办法

   - animate.css文件修改以下内容：

     ```css
     :root {
       --animate-duration: 1s;
       --animate-delay: 1s;
       --animate-repeat: 1;
     }
     修改为:
     page {
       --animate-duration: 1s;
       --animate-delay: 1s;
       --animate-repeat: 1;
     }
     ```

2. 使用

   ```vue
   // animate__animated  animate__效果名称 animate__显示速度
   <image v-if="show" class="logo animate__animated animate__bounceIn animate__faster" src="/static/logo.png">
   ```

### 4. 图标库的创建

- 阿里巴巴图标库iconfont

- 选中图标添加到购物车 - 添加至项目 - 下载到本地 - 解压 

- demo_index.html 图标库

- iconfont.css 图标样式

- 把iconfont.css文件中src引用了iconfont.xxx的部分删除掉，再把剩下的部分复制到icon.css

- 使用

  ```vue
  // iconfont icon-图标名称
  <view style="font-size: 50upx;" class="iconfont icon-weixinzhifu"></view>
  ```

### 5. 公共样式

```css
/* 设置全局样式 */
/* (1) 页面高度100%,默认字体28upx,默认行高1.8,背景颜色 */
page {
	height: 100%;
	font-size: 28upx;
	line-height: 1.8;
	background: #FFFFFF;
}

/* (2) 图片默认100%宽度 */
image {
	width: 100%;
}

/* 主色调 */
/* 主背景颜色（橙色）*/
.main-bg-color {
	background-color: #FD6801;
}

/* 主点击背景颜色（淡橙色）*/
.main-bg-hover-color {
	background-color: rgba(253, 104, 1, 0.85);
}

/* 主字体颜色（橙色）*/
.main-text-color {
	color: #FD6801;
}

/* 主边框颜色 */
.main-border-color {
	border-color: #F1F1F1;
}
```

## 三、底部导航开发(pages.json)

### 1. 全局配置

```json
// 全局配置
	"globalStyle": {
		"navigationBarTextStyle": "black",
		"navigationBarTitleText": "商城",
		"navigationBarBackgroundColor": "#FFFFFF",
		"backgroundColor": "#FFFFFF"
	},
```

### 2. 底部导航

- 先准备好页面和图片

  ```json
  // 底部导航
  	"tabBar": {
  		"color": "#B5B5B5",
  		"selectedColor": "#FD6801",
  		"borderStyle": "black",
  		"backgroundColor": "#FFFFFF",
  		"list": [{
  				"pagePath": "pages/index/index",
  				"text": "首页",
  				"iconPath": "static/tabbar/index.png",
  				"selectedIconPath": "static/tabbar/indexSelected.png"
  			},
  			{
  				"pagePath": "pages/cate/cate",
  				"text": "分类",
  				"iconPath": "static/tabbar/class.png",
  				"selectedIconPath": "static/tabbar/classSelected.png"
  			},
  			{
  				"pagePath": "pages/cart/cart",
  				"text": "购物车",
  				"iconPath": "static/tabbar/cart.png",
  				"selectedIconPath": "static/tabbar/cartSelected.png"
  			},
  			{
  				"pagePath": "pages/my/my",
  				"text": "我的",
  				"iconPath": "static/tabbar/my.png",
  				"selectedIconPath": "static/tabbar/mySelected.png"
  			}
  		]
  	},
  ```

## 四、UI基础库封装

- 把封装的基础库css(common/ui-main.css)引入到App.vue中

  ```css
  /* 基础ui库 */
  @import "@/common/ui-main.css";
  ```

- 常用样式封装

  - 颜色----背景颜色/边框颜色/文本颜色

  - 布局

  - 边框

  - 内外边距

  - 字体大小、行高

  - flex布局

    ```css
    /* 防止图片闪一下 */
    image{will-change: transform}
    /* scroll-view 设置横向滚动*/
    .scroll-row{ width: 100%;white-space: nowrap;line-height: 44px; }
    .scroll-row-item{ display: inline-block!important; }
    
    body{
    	--primary:#007bff;
    	--secondary: #6c757d;
    	--success: #28a745;
    	--danger: #dc3545;
    	--warning: #ffc107;
    	--info: #17a2b8;
    	--light: #f8f9fa;
    	--dark: #343a40;
    	--muted: #6c757d;
    	--white: #fff;
    	--borderColor:#dee2e6;
    	--lightmuted:#B2B2B2;
    }
    
    /* 阴影 */
    .shadow-sm {
        box-shadow: 0 2upx 4upx rgba(114, 130, 138, 0.2)!important;
    }
    .shadow {
        box-shadow: 0 8upx 16upx rgba(114, 130, 138, 0.2)!important;
    }
    .shadow-lg {
        box-shadow: 0 16upx 48upx rgba(114, 130, 138, 0.2)!important;
    }
    /* 定位 */
    .position-absolute{ position: absolute; }
    .position-fixed{ position: fixed; }
    .position-relative{ position: relative; }
    .left-0{ left: 0; }
    .top-0{ top: 0; }
    .bottom-0{ bottom: 0; }
    .right-0{ right: 0; }
    /* 宽高 */
    .w-100{ width: 100%;}
    .w-50{ width: 50%;}
    .h-100{ height: 1250upx;}
    .h-50{ width: 625upx; }
    /* 字体 */
    .font{ font-size: 25upx; }
    .font-sm{ font-size: 22upx; }
    .font-md{ font-size: 30upx; }
    .font-lg{ font-size: 40upx; }
    .font-big{ font-size: 60upx; }
    .font-weight{ font-weight: bold!important; }
    .font-weight-100{ font-weight: 100!important; }
    
    .line-h0{ line-height: 0!important; }
    .line-h{ line-height: 1!important; }
    .line-h-sm{ line-height: 1.2!important; }
    .line-h-md{ line-height: 1.5!important; }
    .line-h-lg{ line-height: 2!important; }
    .line-h-big{ line-height: 3!important; }
    
    .line-through{ text-decoration: line-through; }
    
    .text-center{ text-align: center; }
    .text-left{ text-align: left; }
    .text-right{ text-align: right; }
    
    .row { box-sizing: border-box!important; display: flex!important; flex-direction: row!important; flex-wrap: wrap;}
    [class*='col-'],[class*='span-'],[class*='span24-'] { min-height: 1px;box-sizing: border-box!important;}
    /* 栅栏一 */
    .col-1{ width: 62.5upx; } 
    .col-2{ width: 125upx; } 
    .col-3{ width: 187.5upx; } 
    .col-4{ width: 250upx;} 
    .col-5{ width: 312.5upx; } 
    .col-6{ width: 375upx; }
    .col-7{ width: 437.5upx; }
    .col-8{ width: 500upx; }
    .col-9{ width: 562.5upx; }
    .col-10{ width: 625upx; }
    .col-11{ width: 687.5upx; }
    .col-12{ width: 750upx; }
    /* 栅栏二 */
    .span-1{ width: 5%; } 
    .span-2{ width: 10%; } 
    .span-3{ width: 15%; } 
    .span-4{ width: 20%;} 
    .span-5{ width: 25%; } 
    .span-6{ width: 30%; }
    .span-7{ width: 35%; }
    .span-8{ width: 40%; }
    .span-9{ width: 45%; }
    .span-10{ width: 50%; }
    .span-11{ width: 55%; }
    .span-12{ width: 60%; }
    .span-13{ width: 65%; }
    .span-14{ width: 70%; }
    .span-15{ width: 75%; }
    .span-16{ width: 80%; }
    .span-17{ width: 85%; }
    .span-18{ width: 90%; }
    .span-19{ width: 95%; }
    .span-20{ width: 100%; }
    /* 栅栏三 */
    .span24-1{ width: 4.17%; } 
    .span24-2{ width: 8.33%; } 
    .span24-3{ width: 12.5%; } 
    .span24-4{ width: 16.67%;} 
    .span24-5{ width: 20.83%; } 
    .span24-6{ width: 25%; }
    .span24-7{ width: 29.17%; }
    .span24-8{ width: 33.33%; }
    .span24-9{ width: 37.5%; }
    .span24-10{ width: 41.67%; }
    .span24-11{ width: 45.83%; }
    .span24-12{ width: 50%; }
    .span24-13{ width: 54.17%; }
    .span24-14{ width: 58.33%; }
    .span24-15{ width: 62.5%; }
    .span24-16{ width: 66.67%; }
    .span24-17{ width: 70.83%; }
    .span24-18{ width: 75%; }
    .span24-19{ width: 79.17%; }
    .span24-20{ width: 83.33%; }
    .span24-21{ width: 87.5%; }
    .span24-22{ width: 91.67%; }
    .span24-23{ width: 95.83%; }
    .span24-24{ width: 100%; }
    
    
    /* flex布局 */
    .d-flex{ display: flex;flex-direction: row!important; }
    .d-block{ display: block; }
    .d-inline-block{ display: inline-block; }
    
    .flex-1{ flex: 1; }
    .flex-column{ flex-direction: column!important; }
    .flex-row{ flex-direction: row; }
    .flex-wrap{ flex-wrap: wrap; }
    .flex-nowrap{ flex-wrap: nowrap; }
    .flex-shrink{flex-shrink: 0;}
    .j-start{ justify-content: flex-start; }
    .j-center{ justify-content: center!important; }
    .j-end{ justify-content: flex-end; }
    .j-sb{ justify-content: space-between; }
    .a-center{ align-items:center!important; }
    .a-start{ align-items: flex-start; }
    .a-end{ align-items:flex-end; }
    .a-stretch{ align-items: stretch; }
    .a-self-start{ align-self: flex-start; }
    .a-self-auto{ align-self: auto; }
    .a-self-end{ align-self: flex-end; }
    .a-self-stretch{ align-self:stretch; }
    .a-self-baseline{ align-self:baseline; }
    /* Border */
    .border{  border-width: 1upx; border-style: solid; border-color: var(--borderColor);}
    .border-top{ border-top-width: 1upx; border-top-style: solid; border-top-color: var(--borderColor); }
    .border-right{ border-right-width: 1upx; border-right-style: solid; border-right-color: var(--borderColor);}
    .border-bottom{ border-bottom-width: 1upx;border-bottom-style: solid;border-bottom-color:var(--borderColor);}
    .border-left{ border-left-width: 1upx;border-left-style: solid;border-left-color:var(--borderColor);}
    
    .border-0{ border-width: 0; }
    .border-top-0{ border-top-width: 0; }
    .border-right-0{ border-right-width: 0; }
    .border-bottom-0{ border-bottom-width: 0; }
    .border-left-0{ border-left-width: 0; }
    
    .border-primary{ border-color: var(--primary)!important }
    .border-secondary{ border-color:var(--secondary)!important }
    .border-success{ border-color: var(--success)!important }
    .border-danger{ border-color: var(--danger)!important }
    .border-warning{ border-color:var(--warning)!important }
    .border-info{ border-color: var(--info)!important }
    .border-light{ border-color: var(--light)!important }
    .border-dark{ border-color: var(--dark)!important }
    .border-white{ border-color: var(--white)!important }
    .border-light-secondary{border-color: #F1F1F1!important;}
    
    .rounded{ border-radius: 5upx; }
    .rounded-circle{ border-radius:100%; }
    .rounded-0{ border-radius:0; }
    
    /* color */
    .text-primary{ color:var(--primary)!important; }
    .text-secondary{ color:var(--secondary)!important; }
    .text-success{ color:var(--success)!important; }
    .text-danger{ color: var(--danger)!important; }
    .text-warning{ color:var(--warning)!important; }
    .text-info{ color: var(--info)!important; }
    .text-light{ color: var(--light)!important; }
    .text-dark{ color: var(--dark)!important; }
    .text-muted{ color: var(--muted)!important; }
    .text-light-muted{ color: var(--lightmuted)!important; }
    .text-white{ color: var(--white)!important; }
    
    .bg-primary{ background-color:var(--primary)!important; }
    .bg-secondary{ background-color:var(--secondary)!important; }
    .bg-success{ background-color:var(--success)!important; }
    .bg-danger{ background-color: var(--danger)!important; }
    .bg-warning{ background-color:var(--warning)!important; }
    .bg-info{ background-color: var(--info)!important; }
    .bg-light{ background-color: var(--light)!important; }
    .bg-dark{ background-color: var(--dark)!important; }
    .bg-white{ background-color: var(--white)!important; }
    .bg-light-secondary{background-color: #F1F1F1!important;}
    
    /* Spacing */
    .m-0 { margin-left: 0;margin-right: 0;margin-top: 0;margin-bottom: 0;}
    .m { margin-left: 5upx;margin-right: 5upx;margin-top: 5upx;margin-bottom: 5upx;}
    .m-1 { margin-left: 10upx;margin-right: 10upx;margin-top: 10upx;margin-bottom: 10upx;}
    .m-2 { margin-left: 20upx;margin-right: 20upx;margin-top: 20upx;margin-bottom: 20upx;}
    .m-3 { margin-left: 30upx;margin-right: 30upx;margin-top: 30upx;margin-bottom: 30upx;}
    .m-4 { margin-left: 40upx;margin-right: 40upx;margin-top: 40upx;margin-bottom: 40upx;}
    .m-5 { margin-left: 50upx;margin-right: 50upx;margin-top: 50upx;margin-bottom: 50upx;}
    
    .mx-0 { margin-left: 0;margin-right: 0;}
    .mx { margin-left: 5upx;margin-right: 5upx;}
    .mx-1 { margin-left: 10upx;margin-right: 10upx;}
    .mx-2 { margin-left: 20upx;margin-right: 20upx;}
    .mx-3 { margin-left: 30upx;margin-right: 30upx;}
    .mx-4 { margin-left: 40upx;margin-right: 40upx;}
    .mx-5 { margin-left: 50upx;margin-right: 50upx;}
    
    .my-0 { margin-top: 0;margin-bottom: 0;}
    .my { margin-top: 5upx;margin-bottom: 5upx;}
    .my-1 { margin-top: 10upx;margin-bottom: 10upx;}
    .my-2 { margin-top: 20upx;margin-bottom: 20upx;}
    .my-3 { margin-top: 30upx;margin-bottom: 30upx;}
    .my-4 { margin-top: 40upx;margin-bottom: 40upx;}
    .my-5 { margin-top: 50upx;margin-bottom: 50upx;}
    
    .mt-0 { margin-top: 0;}
    .mt { margin-top: 5upx;}
    .mt-auto { margin-top: auto;}
    .mt-1 { margin-top: 10upx;}
    .mt-2 { margin-top: 20upx;}
    .mt-3 { margin-top: 30upx;}
    .mt-4 { margin-top: 40upx;}
    .mt-5 { margin-top: 50upx;}
    
    .mb-0 { margin-bottom: 0;}
    .mb { margin-bottom: 5upx;}
    .mb-auto { margin-bottom: auto;}
    .mb-1 { margin-bottom: 10upx;}
    .mb-2 { margin-bottom: 20upx;}
    .mb-3 { margin-bottom: 30upx;}
    .mb-4 { margin-bottom: 40upx;}
    .mb-5 { margin-bottom: 50upx;}
    
    .ml-0 { margin-left: 0;}
    .ml { margin-left: 5upx;}
    .ml-auto { margin-left: auto;}
    .ml-1 { margin-left: 10upx;}
    .ml-2 { margin-left: 20upx;}
    .ml-3 { margin-left: 30upx;}
    .ml-4 { margin-left: 40upx;}
    .ml-5 { margin-left: 50upx;}
    
    .mr-0 { margin-right: 0;}
    .mr { margin-right: 5upx;}
    .mr-1 { margin-right: 10upx;}
    .mr-2 { margin-right: 20upx;}
    .mr-3 { margin-right: 30upx;}
    .mr-4 { margin-right: 40upx;}
    .mr-5 { margin-right: 50upx;}
    
    .p-0 {padding-left: 0;padding-right: 0;padding-top: 0;padding-bottom: 0;}
    .p {padding-left: 5upx;padding-right: 5upx;padding-top: 5upx;padding-bottom:5upx;}
    .p-1 {padding-left: 10upx;padding-right: 10upx;padding-top: 10upx;padding-bottom: 10upx;}
    .p-2 {padding-left: 20upx;padding-right: 20upx;padding-top: 20upx;padding-bottom: 20upx;}
    .p-3 {padding-left: 30upx;padding-right: 30upx;padding-top: 30upx;padding-bottom: 30upx;}
    .p-4 {padding-left: 40upx;padding-right: 40upx;padding-top: 40upx;padding-bottom: 40upx;}
    .p-5 {padding-left: 50upx;padding-right: 50upx;padding-top: 50upx;padding-bottom: 50upx;}
    
    .px-0 { padding-left: 0;padding-right: 0;}
    .px { padding-left: 5upx;padding-right: 5upx;}
    .px-1 { padding-left: 10upx;padding-right: 10upx;}
    .px-2 { padding-left: 20upx;padding-right: 20upx;}
    .px-3 { padding-left: 30upx;padding-right: 30upx;}
    .px-4 { padding-left: 40upx;padding-right: 40upx;}
    .px-5 { padding-left: 50upx;padding-right: 50upx;}
    
    .py-0 { padding-top: 0;padding-bottom: 0;}
    .py { padding-top: 5upx;padding-bottom: 5upx;}
    .py-1 { padding-top: 10upx;padding-bottom: 10upx;}
    .py-2 { padding-top: 20upx;padding-bottom: 20upx;}
    .py-3 { padding-top: 30upx;padding-bottom: 30upx;}
    .py-4 { padding-top: 40upx;padding-bottom: 40upx;}
    .py-5 { padding-top: 50upx;padding-bottom: 50upx;}
    
    .pt-0 { padding-top: 0;}
    .pt { padding-top: 5upx;}
    .pt-1 { padding-top: 10upx;}
    .pt-2 { padding-top: 20upx;}
    .pt-3 { padding-top: 30upx;}
    .pt-4 { padding-top: 40upx;}
    .pt-5 { padding-top: 50upx;}
    
    .pb-0 { padding-bottom: 0;}
    .pb { padding-bottom: 5upx;}
    .pb-1 { padding-bottom: 10upx;}
    .pb-2 { padding-bottom: 20upx;}
    .pb-3 { padding-bottom: 30upx;}
    .pb-4 { padding-bottom: 40upx;}
    .pb-5 { padding-bottom: 50upx;}
    
    .pl-0 { padding-left: 0;}
    .pl { padding-left: 5upx;}
    .pl-1 { padding-left: 10upx;}
    .pl-2 { padding-left: 20upx;}
    .pl-3 { padding-left: 30upx;}
    .pl-4 { padding-left: 40upx;}
    .pl-5 { padding-left: 50upx;}
    
    .pr-0 { padding-right: 0;}
    .pr { padding-right: 5upx;}
    .pr-1 { padding-right: 10upx;}
    .pr-2 { padding-right: 20upx;}
    .pr-3 { padding-right: 30upx;}
    .pr-4 { padding-right: 40upx;}
    .pr-5 { padding-right: 50upx;}
    ```

## 五、 使用 Git 管理项目

1. 在项目根目录中新建 `.gitignore` 忽略文件，并配置如下：

   ```gitignore
   # 忽略 node_modules 目录
   /node_modules
   /unpackage/dist
   ```

> > 由于忽略了 unpackage 目录中仅有的dist 目录，因此默认情况下 unpackage 目录不会被 Git 追踪
> > 为了让 Git 能够正常追踪 unpackage 目录，按照惯例，可以在 unpackage 目录下创建一个叫做 `.gitkeep` 的文件进行占位

2. 打开终端，切换到项目根目录中，运行如下的命令，初始化本地 Git 仓库：git init
3. 将所有文件都加入到暂存区：git add .
4. 本地提交更新：git commit -m "init project"
5. 远程推送

## 六、首页开发(VUE部分)

## 七、NVUE快速入门

## 八、首页开发(NVUE部分)

