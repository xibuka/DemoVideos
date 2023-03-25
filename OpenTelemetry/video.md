---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
---

(pause: 1)

![](07-kong-background.png)

(font-size: 30)

```
Checking requests tracing by OpenTelemetry plugin to check the tracing span of your requests
```

In this video, we'll show you how to use the OpenTelemetry plugins to troubleshoot your performance issue.

---

(pause: 1)

![](CreateSvc.mp4)

First, let's create a service which is point to an echo upstream API. I'm using a public HTTP Request & Response Service, called httpbin. I set the sub path to /anything so the response will be the same of my request.

---

(pause: 1)

![](CreateRoute.mp4)

Next, create a route for this service so we can access it from outside. 

---

(pause: 1)

![](ConfirmAccess.mp4)

Let's try to access the httpbin server using Kong Gateway. Send a request to port 8000 of the kong gateway instance, with a subpath /demo which we set in the route. We got a 200 response so our settings looks good.

---

(pause: 1)

![](EnableOTLplugin.mp4)
OK next step let's enable the OpenTelemetry Plugin on the service level. So this plugin will propagate distributed tracing spans and report low-level spans of this service to a OTLP compatible server.

(pause: 1)

In this demo I'm using HoneyComb as my OTLP server. You need to config some addtional headers to let the tracing spans go to the data bucket in your account. 

---

![](ConfirmAPIkey.png)
If you also want to use HoneyComb for testing, you can find your API keys from your dashboard of HoneyComb. 

---

(pause: 1)

![](EnableRouteTransPlugin.mp4)
Let try to add another plugin, Route Transformer Advanced for performance testing. This plugin can transforms the routing on the fly in Kong, changing the upstream server, port, or path to hit. In this example we changed the service path to /xml. 
We want to see if this plugin will increase the latency from the tracing information.

---

(pause: 1)

![](SendRequest.mp4)

Send some requests to the same path, as we change the path to /xml, some xml response will be get by the client.

---

(pause: 1)

![](CheckTrace.mp4)

Let's check the tracing span in HoneyComb's webpage. Click the tracing entry of each request, you can see the latency of every span in this requests. In this example you can see most of the time was cost for access the upstream API and the Route Transformer Advanced plugin only took 52 micro seconds. 
As a conclusion, using open telemetry plugin to export the tracing information of the request can help you to see the performance of each parts in it. This is a very powerful tool for Operators and maintainers.
Thanks for watching, see you next time.