---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
---

(pause: 1)

![](00-kong-background.png)

(font-size: 30)

```
# Secury your API with Kong Gateway JWT plugin
```

In this video, we'll show you how to secure your upstream API use the JWT plugin.

---

(pause: 1)

![](01_CreateService.mp4)

First, let's create a service which is point to an echo upstream API. I'm using a public HTTP Request & Response Service, called httpbin. I set the sub path to /anything so the response will be the same of my request.

---

(pause: 1)

![](02_CreateRoute.mp4)

Next, create a route for this service so we can access it from outside. I will set the path to /demo so we can access this API with this path.

---

(pause: 1)

![](03_ConfrirmAccess.mp4)

Let's try to access the httpbin server using Kong Gateway. Send a request to port 8000 of the kong gateway instance, with a subpath /demo which we set in the route. We got a 200 response so our settings looks good.

---

(pause: 1)

![](04_EnableJWTPlugin.mp4)
OK, let's enable the JWT Plugin on the service level. In this demo, we will keep all the default settings and click install. Please note the key claim name is `ISS`, we will use it when creating the token.

---

(pause: 1)

![](05_AccessBlock.mp4)

Let's try to access the API again. We don't have a valid token so get blocked this time.

---

(pause: 1)

![](06_CreateConsumer.mp4)

Next, let's start to create a valid JWT token. First, create a consumer called Joe.

---

(pause: 1)

![](07_GenJWTCred.mp4)

Second, create a JWT credential for Joe. Leave the key and secret as blank and Kong will generate them for you. JWT plugins can use several algorithms to verify the token's signature. We will use the default HS256 in this demo.

(pause: 1)

The secret is not shown in the GUI due the security reason. We can confirm it from the CLI, the admin API. We will use the key and the secret to create the token.

---

(pause: 1)

![](10_CreateJWTCustomCred.mp4)

You can also use your own credentials for the JWT plugin. Just input them in the key and secret field,

(pause: 3)

and you can also see them via the Admin API.

---

(pause: 1)

![](08_GenToken.mp4)

We can create the token in jwt.io. Add a new field called iss in the payload section, with the value of the key.
Then input the secret in the verify signature section. You can get the token on the left side of the page.

---

(pause: 1)

![](09_AccessWithToken.mp4)

Let's access the API again with this token. Copy the token and add it in the authorization header as a Bearer token. You should be able to access successfully this time.

(pause: 1)

As a conclusion, using jwt plugin can help you to protech your API very easy. It can help you to verify the JSON Web Token in different algorithms.
Thanks for watching, see you next time.
