# V2Ray Heroku

**若需部署 V2Ray VLESS，请转到 [vless](https://github.com/bclswl0827/v2ray-heroku/tree/vless) 分支。**

## 概述

本专案用于在 Heroku 上部署 V2Ray WebSocket，在合理使用的程度下，本镜像不会因为大量占用资源而导致封号。

部署完成后，每次启动应用时，运行的 V2Ray 将始终为最新版本

## 部署

### 步骤

 1. Fork 本专案到自己的 GitHub 账户（用户名以 `example` 为例）
 2. 修改专案名称，注意不要包含 `v2ray` 和 `heroku` 两个关键字（修改后的专案名以 `demo` 为例）
 3. 修改 `README.md`，将 `bclswl0827/v2ray-heroku` 替换为自己的内容（如 `example/demo`）

> [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/jlower/my_own_vps)

 4. 回到专案首页，点击上面的链接以部署 V2Ray

### 变量

对部署时需设定的变量名称做如下说明。

| 变量 | 默认值 | 说明 |
| :--- | :--- | :--- |
| `ID` | `ad806487-2d26-4636-98b6-ab85cc8521f7` | VMess 用户主 ID，用于身份验证，为 UUID 格式 |
| `WSPATH` | `/` | WebSocket 所使用的 HTTP 协议路径 |

## 注意v2rayN客户端中VMess协议的用户ID需要与所设置的ID相同



## 接入 CloudFlare

以下两种方式均可以将应用接入 CloudFlare，从而在一定程度上提升速度。

 1. 为应用绑定域名，并将该域名接入 CloudFlare
 2. 通过 CloudFlare Workers 反向代理

## 注意

 1. **请勿滥用本专案，类似 Heroku 的免费服务少之又少，且用且珍惜**
 2. 若使用域名接入 CloudFlare，请考虑启用 TLS 1.3
 3. AWS 绝大部分 IPv4 地址已被 Twitter 屏蔽





<p>Heroku 是一个支持多种编程语言的云平台即服务，并且提供免费的容器服务（美国、欧洲节点），本文就以免费容器为例，搭建 V2 并配置 CF 加速，你懂得！</p>
<p>注意：Heroku 有滥用危险，后果可能就是封禁账号哦！</p>
<h2 id="一、配置heroku">一、配置Heroku<button class="cnblogs-toc-button" title="显示目录导航"></button><a class="esa-anchor" style="opacity: 0;" href="#一、配置heroku"></a></h2>
<p>1、首先注册Heroku账号，点击通过&nbsp;<a href="https://dashboard.heroku.com/" rel="noopener" target="_blank">https://dashboard.heroku.com</a>&nbsp;注册一个账号，注册时候不能使用QQ邮箱：</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225322234-1361479730.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225322234-1361479730.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>2、注册成功以后登录，登录以后部署应用！名称随便填写就行了，然后点击 Deploy app 系统会自动部署：</p>



> [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/jlower/my_own_vps)



<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225333361-1050518431.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225333361-1050518431.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、部署完成以后，点击 Settings 再点击 Reveal Config Vars 就可以看见 UUID了！记下自己的UUID等会还是用到：</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225343772-278215607.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225343772-278215607.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>4、接着下滑，看见Domains项后有个域名！https://*****.herokuapp.com/ 记下域名，稍后配置CloudFlare 反向代理会用到：</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225353814-2098411255.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225353814-2098411255.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2 id="二、配置cloudflare反向代理">二、配置CloudFlare反向代理<button class="cnblogs-toc-button" title="显示目录导航"></button><a class="esa-anchor" href="#二、配置cloudflare反向代理"></a></h2>
<p>1、首先登陆CloudFlare官网，然后点击 右侧的 Workers ：</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225403899-1690163716.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225403899-1690163716.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>2、接着点击创建 Workers ：</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;<a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225432966-1111581748.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225432966-1111581748.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、接着复制下方代码，并添加进去！注意把下面的中文替换成你之前在Domains项看见的那个域名前缀：</p>

```
addEventListener(
  "fetch",event => {
     let url=new URL(event.request.url);
     url.hostname="你的heroku域名.herokuapp.com";
     let request=new Request(url,event.request);
     event. respondWith(
       fetch(request)
     )
  }
)
```


<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225442552-681864788.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225442552-681864788.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>至此！CF就配置完成了，接下来开始配置V2客户端！</p>
<h2 id="三、配置v2客户端">三、配置V2客户端<button class="cnblogs-toc-button" title="显示目录导航"></button><a class="esa-anchor" href="#三、配置v2客户端"></a></h2>
<p>1、配置客户端，请按照图片的要求设置，否则不能联网：</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225451392-1453325353.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225451392-1453325353.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>3、测试是否生效！我这里用的是笨牛网自选的IP，速度不是很好。如果有大佬有效果理想的，可以分享给我一个：</p>
<p>&nbsp;</p>
<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225500851-1829953283.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200817225500851-1829953283.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h2 id="四、自选ip">四、自选IP<button class="cnblogs-toc-button" title="显示目录导航"></button><a class="esa-anchor" href="#四、自选ip"></a></h2>
<p>下载自选IP程序，然后windows系统运行即可，全自动化。</p>

(https://github.com/XIU2/CloudflareSpeedTest)

<p><a href="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200815205747204-249709069.png" data-title="" data-alt="" data-lightbox="roadtrip"><img src="https://img2020.cnblogs.com/blog/1783030/202008/1783030-20200815205747204-249709069.png" alt="" class="medium-zoom-image" loading="lazy" /></a></p>
<p>&nbsp;</p>




 
