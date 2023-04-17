---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
voice: Yuriko
---

(pause: 1)

![](07-kong-background.png)

(font-size: 30)

```
Kong GatewayのOpenTelemetry Pluginを使って、リクエストの性能をトレースで確認しよう
```

このビデオでは、OpenTelemetryプラグインを使用して、パフォーマンスの問題をトラブルシューティングする方法を紹介します。

---

(pause: 1)

![](CreateSvc.mp4)

まず、echoのアップストリームAPIを指すサービスを作成します。ここでは、httpbinというHTTPリクエスト＆レスポンスサービスを使っています。サブパスは/anythingとし、レスポンスのBodyがリクエストと同じ内容となります。。

---

(pause: 1)

![](CreateRoute.mp4)

次に、このサービスに外部からアクセスできるように、ルートを作成します。

---

(pause: 1)

![](ConfirmAccess.mp4)

Kong Gatewayを使ってhttpbinサーバにアクセスしてみます。kongゲートウェイインスタンスのポート8000に、ルートで設定したサブパス/demoを指定してリクエストを送ります。200レスポンスが返ってきたので、設定は問題なさそうです。

---

(pause: 1)

![](EnableOTLplugin.mp4)

次のステップでは、サービスレベルでOpenTelemetry Pluginを有効にしましょう。このプラグインは、リクエストのトレースをOTLP互換サーバーに送信します。

(pause: 1)

このデモでは、OTLPサーバーとしてHoneyCombを使用しています。トレースをアカウント内のデータバケットに送るには、画面で示したように、いくつかのヘッダを設定する必要があります。

---

![](ConfirmAPIkey.png)

HoneyCombをテストにも使用したい場合は、HoneyCombのダッシュボードからAPIキーを確認することができます。

---

(pause: 1)

![](EnableRouteTransPlugin.mp4)

パフォーマンステストのために、もう一つのプラグイン、Route Transformer Advancedを追加してみましょう。このプラグインは、Kongのルーティングを即座に変換し、上流のサーバー、ポート、またはヒットするパスを変更することができます。この例では、サービスパスを/xmlに変更しました。
このプラグインを追加したので、レイテンシーが増加するかどうかをトレース情報から確認したいと思います。

---

(pause: 1)

![](SendRequest.mp4)

同じパスにリクエストを送り、パスを/xmlに変更すると、クライアントからいくつかのxmlレスポンスが返ってきます。

---

(pause: 1)

![](CheckTrace.mp4)

HoneyCombのWebページでリクエストのトレースを確認してみましょう。各リクエストのトレースエントリーをクリックすると、このリクエストの各スパンのレイテンシーを見ることができます。この例では、ほとんどの時間がアップストリームAPIへのアクセスに費やされ、Route Transformer Advancedプラグインは52マイクロ秒しかかかっていないことがわかります。
まとめとして、open telemetryプラグインを使用してリクエストのトレース情報をエクスポートすると、その中の各段階のパフォーマンスを確認することができ、運用・保守担当者にとって非常に強力なツールです。
ご視聴ありがとうございました、次回もよろしくお願いします。
