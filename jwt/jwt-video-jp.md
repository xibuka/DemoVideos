---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
voice: Yuriko
---
(pause: 1)

![](00-kong-background.png)

(font-size: 30)

```
 Kong Gateway JWTプラグインを使用してAPIを保護
```

このビデオでは、JWTプラグインを使用してAPIを保護する方法を紹介します。

---

(pause: 1)

![](01_CreateService.mp4)

まず、デモのためにechoというAPIを指すサービスを作成します。ここでは httpbin という public HTTP Request & Response Service を使用します。サブパスは /anything とし、リクエストと同じレスポンスになるようにしました。

---

(pause: 1)

![](02_CreateRoute.mp4)

次に、このサービスに外部からアクセスできるように、ルートを作成します。ここではパスを /demo とし、このパスでこの API にアクセスできるようにします。
--------------------------------------------------------------------------------------------------------------------------------------------------

(pause: 1)

![](03_ConfrirmAccess.mp4)

Kong Gatewayを使ってhttpbinサーバにアクセスしてみます。kongゲートウェイインスタンスのポート8000に、ルートで設定したサブパス/demoを指定してリクエストを送ります。200のレスポンスが返ってきたので、設定はうまくいっているようです。

---

(pause: 1)

![](04_EnableJWTPlugin.mp4)

では、サービスレベルでJWT Pluginを有効にしてみましょう。このデモでは、すべてのデフォルト設定を維持したまま、インストールをクリックすることにします。キークレーム名が `ISS`であることに注意してください、トークン作成時に使用します。

---

(pause: 1)

![](05_AccessBlock.mp4)

もう一度APIにアクセスしてみましょう。有効なトークンがないので、今度はブロックされました。

---

(pause: 1)

![](06_CreateConsumer.mp4)

次に、有効なJWTトークンの作成に取りかかりましょう。まず、Joeというコンシューマーを作成します。

---

(pause: 1)

![](07_GenJWTCred.mp4)

次に、JoeのためにJWTクレデンシャルを作成します。キーとシークレットは空欄にしておくと、Kongが生成してくれます。JWTプラグインは、トークンの署名を検証するためにいくつかのアルゴリズムを使用することができます。このデモでは、デフォルトのHS256を使用することにします。

(pause: 1)

セキュリティの関係上、シークレットはGUIに表示されません。CLIでAdmin APIから確認することができます。このキーとシークレットを使って、トークンを作成します。

---

(pause: 1)

![](10_CreateJWTCustomCred.mp4)

JWTプラグインには、自分の認証情報を使うこともできます。キーとシークレットのフィールドに入力するだけです、

(pause: 3)

また、Admin APIで確認することもできます。

---

(pause: 1)

![](08_GenToken.mp4)

jwt.ioでトークンを作成することができます。Payload sectionにissという新しいフィールドを追加し、JWTクレデンシャルのキーの値を入力します。
そして、verify signatureセクションでsecretを入力します。トークンはページの左側で取得することができます。

---

(pause: 1)

![](09_AccessWithToken.mp4)

このトークンを使って、もう一度APIにアクセスしてみましょう。トークンをコピーして、authorizationヘッダーにBearerトークンとして追加してください。今度は正常にアクセスできるはずです。

(pause: 1)

jwtプラグインを使用すると、非常に簡単にAPIを保護するのに役立ちます。また、JSON Web Tokenを様々なアルゴリズムで検証することができます。
