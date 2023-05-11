# cordova-plugin-app-weibosdk

这是一个微博的 Cordova 插件. [English](https://github.com/Wgga/cordova-plugin-app-weibosdk/blob/main/README.md)

## 功能
- 微博 SSO 登录
- 微博登出
- 微博分享(网页、文字、图片)
- 检查微博官方客户端是否安装

## 安装要求
- Cordova Version >= 3.5
- Cordova-Android >= 7.0
- Cordova-iOS >= 4.0

## 安装
1. 命令行运行 ```cordova plugin add cordova-plugin-app-weibosdk --variable WEIBO_APP_ID=YOUR_WEIBO_APPID```			
2. 在你的config.xml文件中添加 ```<preference name="REDIRECTURI" value="YOUR_WEIBO_REDIRECTURI" />``` 如果你不添加这个选项，那么默认的 redirecturi 是 https://api.weibo.com/oauth2/default.html               
3. 命令行运行 cordova build   					

# 注意事项
1. 这个插件要求 Cordova-Android 的版本 >=4.0,推荐使用 Cordova 5.0 或更高的版本，因为从 Cordova 5.0 开始 Cordova-Android 4.0 是默认使用的 Android 版本
2. 请在 Cordova 的 deviceready 事件触发以后再调用本插件!!!!!  

## 使用方法
### 微博SSO登录
```Javascript
WeiboSDK.ssoLogin(function (args) {
   alert('access token is ' + args.access_token);
   alert('userId is ' + args.userId);
   alert('expires_time is ' + new Date(parseInt(args.expires_time)) + ' TimeStamp is ' + args.expires_time);
}, function (failReason) {
   alert(failReason);
});
```


### 微博登出
```Javascript
WeiboSDK.logout(function () {
   alert('logout success');
}, function (failReason) {
   alert(failReason);
});
```

### 微博网页分享
```Javascript
var args = {};
args.url = 'https://cordova.apache.org/';
args.title = 'Apache Cordova';
args.description = 'This is a Cordova Plugin';
args.image = 'https://cordova.apache.org/static/img/pluggy.png';
WeiboSDK.shareToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```

### 微博图片分享
```Javascript
var args = {};
args.image = 'https://cordova.apache.org/static/img/pluggy.png';
WeiboSDK.shareImageToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```

### 微博文字分享
```Javascript
var args = {};
args.text = 'This is a Cordova Plugin';
WeiboSDK.shareTextToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```

### 检查微博客户端是否安装
```Javascript
WeiboSDK.checkClientInstalled(function () {
   alert('client is installed');
}, function () {
   alert('client is not installed');
});
```

### 获取用户信息
```Javascript
var url = 'https://api.weibo.com/2/users/show.json?uid=' + usrid + '&&access_token=' + token;
http.get(url)
```

# 测试Demo
在安装完这个插件以后，把 Cordova 工程中的代码替换为 example_www 中的代码，在 build 以后可以进行各个功能测试，以下为运行效果图：
<div style="text-align:center"><img src="https://github.com/Wgga/cordova-plugin-app-weibosdk/blob/master/ScreenShot.png?raw=true" alt="example" style="width:300px"></div>		

## 关于微博SDK
你可以在[这里](https://github.com/sinaweibosdk)，找到最新的微博 SDK，如果发现 bug 请开 issus，同时也欢迎 star 和 fork
