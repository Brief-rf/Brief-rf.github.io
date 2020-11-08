# Google Drive免费搭建网盘

#  Google Drive免费搭建个人网盘

上篇博客讲了怎么获得无限网盘容量，这篇博客讲一下怎么用Google Drive免费搭建个人永久直链网盘。

## 1.GoIndex获取代码

首先访问[GoIndex网站](https://install.gd.workers.dev)

![image-20200305182836755](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305182836755.png)

### 第一步：获取认证码

选择你的账号登陆

![image-20200305183147534](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305183147534.png)

![image-20200305183451309](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305183451309.png)

复制粘贴到下面第一个输入框内

![image-20200305183537798](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305183537798.png)

![image-20200305194309672](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305194309672.png)

复制，粘贴到目录ID，根目录密码可以不用填写，后面可以修改的。

### 第二步：生成代码

```html
var authConfig = {
    "siteName": "GoIndex", // 网站名称
    "root_pass": "index",  // 根目录密码，优先于.password
    "version" : "1.0.6", // 程序版本
    "theme" : "material", // material  classic 
    "client_id": "**********.apps.googleusercontent.com",
    "client_secret": "***********************",
    "refresh_token": "**************************", // 授权 token
    "root": "0AMaMyTwt7_s3Uk9PVA" // 根目录ID
};

var gd;

var html = `
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
  <title>${authConfig.siteName}</title>
  <script src="//cdn.jsdelivr.net/combine/gh/jquery/jquery@3.2/dist/jquery.min.js,gh/donwa/goindex@${authConfig.version}/themes/${authConfig.theme}/app.js"></script>
</head>
<body>
</body>
</html>
`;

addEventListener('fetch', event => {
    event.respondWith(handleRequest(event.request));
});

/**
 * Fetch and log a request
 * @param {Request} request
 */
async function handleRequest(request) {
    if(gd == undefined){
      gd = new googleDrive(authConfig);
    }
*************************
```

复制代码，马上要用到呢

## Cloud flare快速部署

进入[Cloud flare网站](https://dash.cloudflare.com)注册一个账号。然后看下图

![image-20200305195414967](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305195414967.png)

![image-20200305195439264](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305195439264.png)

![image-20200305195539924](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305195539924.png)

把代码替换为你原来复制的

![image-20200305200140569](https://gitee.com//Brief-rf/BlogImages/raw/master/img/image-20200305200140569.png)

然后你就可以拥有你自己的网盘了，并且访问不需要梯子，文件下载可以用idm或者adm专用下载器。

至此，教程结束！
