## 前言

> 感谢 [Huxpro](https://github.com/Huxpro) 设计的主题.

> 感谢[Hux Blog](https://github.com/Huxpro/huxpro.github.io) 将主题移植到hexo中

![](http://huangxuan.me/img/blog-desktop.jpg)

我在windows系统中建立了自己博客项目，希望将其部署到自己服务器上，使用hexo相关命令进行部署遇到了很多问题，因此我打算将生成的静态文件直接同步到服务器上，来实现部署。因此对这个项目进行了一些修改，来替换hexo自带的部署方式。

## 使用

### 1.配置rsync服务

具体步骤可以参考我的文章[Ubuntu配置rsync服务](https://segmentfault.com/a/1190000010310496)

### 2.项目初始化

```
git clone https://github.com/yan358941877/blog.git
cd blog
npm install
```

### 3.修改

使用自己的信息修改 `_config.yml`文件

特别是这一部分

```
# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
url: http://yanxinxin.cn/blog
root: /blog/
permalink: :year/:month/:day/:title/
permalink_defaults:
```


### 4.新建文章

```
hexo new post IMAPOST
```

## 5.generate

```
npm run generate
```

## 6.部署

```
npm run deploy
```
