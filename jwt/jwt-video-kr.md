---
size: 1080p
transition: crossfade 0.2
background: corporate-1 fade-in fade-out
theme: light
subtitles: embed
voice: Min-ho
---
(pause: 1)

![](00-kong-background.png)

(font-size: 30)

```
 콩 게이트웨이 JWT 플러그인으로 API 보안 유지
```

이 비디오에서는 JWT 플러그인을 사용하여 업스트림 API를 보호하는 방법을 보여드립니다.

---

(pause: 1)

![](01_CreateService.mp4)

먼저 에코 업스트림 API를 가리키는 서비스를 만들어 보겠습니다. 저는 httpbin이라는 공용 HTTP 요청 및 응답 서비스를 사용하고 있습니다. 응답이 요청과 동일하도록 하위 경로를 /anything으로 설정했습니다.

---

(pause: 1)

![](02_CreateRoute.mp4)

다음으로 외부에서 이 서비스에 액세스할 수 있도록 경로를 생성합니다. 이 경로로 이 API에 액세스할 수 있도록 경로를 /demo로 설정하겠습니다.

---

(pause: 1)

![](03_ConfrirmAccess.mp4)

콩 게이트웨이를 이용해 httpbin 서버에 접속해 봅시다. 경로에 설정한 하위 경로 /데모를 사용하여 콩 게이트웨이 인스턴스의 포트 8000으로 요청을 보냅니다. 200 응답을 받았으므로 설정이 잘 된 것 같습니다.

---

(pause: 1)

![](04_EnableJWTPlugin.mp4)

이제 서비스 수준에서 JWT 플러그인을 활성화해 보겠습니다. 이 데모에서는 모든 기본 설정을 그대로 유지하고 설치를 클릭합니다. 키 클레임 이름은 `ISS`이며 토큰을 생성할 때 사용할 것입니다.

---

(pause: 1)

![](05_AccessBlock.mp4)

API에 다시 접속해 보겠습니다. 유효한 토큰이 없으므로 이번에는 차단됩니다.

---

(pause: 1)

![](06_CreateConsumer.mp4)

이제 유효한 JWT 토큰을 생성해 보겠습니다. 먼저 Joe라는 소비자를 생성합니다.

---

(pause: 1)

![](07_GenJWTCred.mp4)

둘째, Joe에 대한 JWT 자격 증명을 만듭니다. 키와 비밀번호는 비워두면 Kong이 자동으로 생성합니다. JWT 플러그인은 여러 알고리즘을 사용하여 토큰의 서명을 확인할 수 있습니다. 이 데모에서는 기본 HS256을 사용하겠습니다.

(pause: 1)

보안상의 이유로 비밀 번호는 GUI에 표시되지 않습니다. 관리자 API인 CLI에서 확인할 수 있습니다. 키와 비밀을 사용하여 토큰을 생성하겠습니다.

---

(pause: 1)

![](10_CreateJWTCustomCred.mp4)

JWT 플러그인에 고유한 자격 증명을 사용할 수도 있습니다. 키와 비밀 필드에 입력하기만 하면 됩니다,

(pause: 3)

관리자 API를 통해서도 확인할 수 있습니다.

---

(pause: 1)

![](08_GenToken.mp4)

jwt.io에서 토큰을 생성할 수 있습니다. 페이로드 섹션에 iss라는 새 필드를 추가하고 키 값을 입력합니다.
그런 다음 서명 확인 섹션에 비밀을 입력합니다. 페이지 왼쪽에서 토큰을 얻을 수 있습니다.

---

(pause: 1)

![](09_AccessWithToken.mp4)

이 토큰으로 API에 다시 액세스해 보겠습니다. 토큰을 복사하여 인증 헤더에 베어러 토큰으로 추가합니다. 이번에는 성공적으로 액세스할 수 있을 것입니다.

(pause: 1)

결론적으로 jwt 플러그인을 사용하면 API를 매우 쉽게 보호할 수 있습니다. 다양한 알고리즘에서 JSON 웹 토큰을 검증하는 데 도움이 될 수 있습니다.
시청해주셔서 감사합니다, 다음에 뵙겠습니다.