---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
voice: Dawei
---

(pause: 1)

![](00-kong-background.png)

(font-size: 30)

```
 使用Kong Gateway 的JWT插件来保证你的API安全
```

在这个视频中，我们将向你演示如何使用JWT插件来保护你的API。

---

(pause: 1)

![](01_CreateService.mp4)

首先，让我们创建一个服务，它指向一个公共的HTTP请求和响应服务，叫做httpbin。我把子路径设置为/anything，所以响应将与我的请求相同。

---

(pause: 1)

![](02_CreateRoute.mp4)

接下来，为这个服务创建一个路由，这样我们就可以从外部访问它。我将设置路径为/demo，这样我们就可以用这个路径访问这个API。

---

(pause: 1)

![](03_ConfrirmAccess.mp4)

让我们试着用Kong Gateway访问httpbin服务器。向Kong网关节点的8000端口发送一个请求，其中有一个我们在路由中设置的子路径/demo。我们得到一个200的响应，所以我们的设置看起来没有问题。

---

(pause: 1)

![](04_EnableJWTPlugin.mp4)

接下来，让我们在服务层面上启用JWT插件。在这个演示中，我们将保持所有的默认设置并点击Install。请注意，密钥要求的名称是`ISS`，我们将在创建token时使用它。

---

(pause: 1)

![](05_AccessBlock.mp4)

让我们再次访问刚才的API。因为没有提供一个有效的token，所以这次被阻止了。

---

(pause: 1)

![](06_CreateConsumer.mp4)

下一步，让我们开始创建一个有效的JWT Token。首先，创建一个名为Joe的Consumer。

---

(pause: 1)

![](07_GenJWTCred.mp4)

其次，为Joe创建一个JWT凭证。如果你把Key和Secret留空并点击确认，Kong将为你生成它们。JWT插件可以使用多种算法来验证Token的签名。在这个演示中，我们将使用默认的HS256。

(pause: 1)

由于安全原因，Secret没有显示在GUI中。我们可以从CLI命令行、通过Admin API中确认它。我们将使用Key和secret来创建令牌。

---

(pause: 1)

![](10_CreateJWTCustomCred.mp4)

你也可以为JWT插件使用你自己的凭证信息。只需在Key和Secret字段中输入它们、

(pause: 3)

而且，你也可以通过管理员API看到它们。

---

(pause: 1)

![](08_GenToken.mp4)

我们可以在jwt.io中创建Token。在payload部分添加一个名为iss的新字段，其中包含Key的值。
然后在verify signature 的部分输入Secret。你可以在页面的左侧获得Token。

---

(pause: 1)

![](09_AccessWithToken.mp4)

让我们用这个Token再次访问刚才的API。复制这个Token并将其添加到authorization Header中作为一个Bearer token。这次你应该能够成功访问。

(pause: 1)

由此可见，使用jwt插件可以帮助你非常容易地保护你的API。它可以帮助你在不同的算法中验证JSON Web Token。
谢谢你的观看，我们下期再见。
