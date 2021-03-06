---
title: "Express 웹사이트 보안 강화하기 [Helmet]"
excerpt_separator: "<!--more-->"
layout: single
date: 2021-03-06T13:56:30+09:00
categories:
  - Node.js
tags:
  - Node.js
  - Express
  - Helmet
permalink: /nodejs/helmet/
---
---
Express로 만들어진 웹 사이트의 보안을 강화하기 위해 [Helmet](https://helmetjs.github.io/){:target="_blank"} 미들웨어를 사용합니다.
<!--more-->
## 설치 및 사용법
* [Helmet](https://helmetjs.github.io/){:target="_blank"}

* [Production Best Practices: Security](https://expressjs.com/en/advanced/best-practice-security.html){:target="_blank"}

```
$ npm install helmet --save
```

```javascript
// ...

const helmet = require('helmet')

// 모든 기능 사용
app.use(helmet());

// or, 특정 기능 사용
app.use(helmet.contentSecurityPolicy());
app.use(helmet.dnsPrefetchControl());
app.use(helmet.expectCt());
app.use(helmet.frameguard());
app.use(helmet.hidePoweredBy());
app.use(helmet.hsts());
app.use(helmet.ieNoOpen());
app.use(helmet.noSniff());
app.use(helmet.permittedCrossDomainPolicies());
app.use(helmet.referrerPolicy());
app.use(helmet.xssFilter());

// ...
```


## Content Security Policy (CSP)
CSP를 사용하면 웹사이트의 http응답에 CSP 헤더가 추가됩니다. CSP 헤더가 존재할 경우, 브라우저는 CSP 헤더에 언급되지 않은 리소스들을 로드하지 않습니다. Helmet의 CSP 기본설정은 'self' 즉, 자신의 웹사이트에 존재하는 리소스들만을 허용합니다.
그래서 CDN 등의 외부 사이트의 소스를 이용할 경우, 또는 다른 웹사이트에서 이미지 로드하는 경우, 심지어 인라인 스크립트로 자바스크립트 코드를 작성한 경우 모두 에러를 발생시킵니다. 이를 해결하기 위해서는 웹 페이지가 사용할 신뢰할 수 있는 리소스들의 도메인을 CSP 헤더에 추가해야합니다.

```javascript
const cspOptions = {
  directives: {
    // 기본 옵션을 가져옵니다.
    ...helmet.contentSecurityPolicy.getDefaultDirectives(),
    
    // 구글 API 도메인과 인라인된 스크립트를 허용합니다.
    "script-src": ["'self'", "*.googleapis.com", "'unsafe-inline'"],

    // 리그오브레전드 사이트의 이미지 소스를 허용합니다.
    "img-src": ["'self'", "data:", "*.leagueoflegends.com"],
  }
}

// Helmet의 모든 기능 사용. (contentSecurityPolicy에는 custom option 적용)
app.use(helmet({
  contentSecurityPolicy: cspOptions,
}));
```

## 'unsafe-inline' 대체하기
CSP 헤더에 'unsafe-inline'을 추가하면, 인라인된 스크립트의 실행이 허용됩니다. 그러나 이는 해커가 웹사이트의 inline 스크립트를 주입하여 보안상의 위협을 가할 수 있게 합니다. 이를 해결하는 방법은 두가지가 있습니다.

1. nonce 속성 이용
웹페이지를 로드할 때마다 무작위로 생성된 nonce 속성을 인라인 스크립트에 부여하고, 이를 CSP 헤더에 추가합니다. 응답(response) 마다 다른 nonce 값이 설정되므로, 제 3자가 인라인 스크립트를 주입하기 어려워집니다.

2. hash 사용
각각의 인라인 스크립트의 hash 값을 CSP에 추가합니다. 'inline-unsafe' 속성을 제거한 채로 브라우저에서 웹페이지를 로드할 경우 에러 메시지가 뜨는데, 메시지 내부에 해당 인라인 스크립트의 해시값을 얻을 수 있습니다.

hash를 사용할 경우에는 각각의 inline script 마다 해시값을 추가해야하고, inline script가 매번 바뀔 경우 해시값도 매번 바뀌게 된다는 단점이 있습니다. 웹사이트에 inline script가 매우 적고, 항상 동일할 경우에만 사용하는 것이 좋겟습니다.

## CSP에 Google Gtag 추가

## 검색: **ctrl + f**
커서 위치의 단어를 검색합니다.

## 들여쓰기: **ctrl + ]**
커서위치의 줄 또는 블럭설정된 문단 전체를 들여쓰기합니다. (커서가 줄 맨앞에 있거나, 블럭설정된 상태에서는 **tab**키와 동일한 기능을 합니다)

## 내어쓰기: **ctrl + [**
커서위치의 줄 또는 블럭설정된 문단 전체를 내어쓰기합니다.(한칸씩 당깁니다)

## 줄 복사
* 아래로 복사: **shift + alt + &#8593;**
* 위로 복사: **shitf + alt + &#8595;**

커서위치의 줄 또는 블럭설정된 문단 전체를 복사합니다.

## 블럭설정
* 한글자씩: **shift + 방향키**

* 한단어씩: **shift + ctrl + 방향키**

## 다중 커서 (마우스): **alt + click**
클릭한 위치에 커서가 추가로 생성됩니다.

## 다중 커서 (키보드)
* **ctrl + alt + &#8593;**
* **ctrl + alt + &#8595;**

윗줄이나 아랫줄의 동일한 위치에 커서를 추가로 생성합니다.

## 주석 처리: **ctrl + k ctrl + c**
**ctrl**을 누른 상태에서 **k**와 **c**를 순서대로 누릅니다.

커서위치의 줄 또는 블록설정된 문단 전체를 주석처리합니다.

## 주석 처리 취소: **ctrl + k ctrl + u**
**ctrl**을 누른 상태에서 **k**와 **u**를 순서대로 누릅니다.

주석처리된 커서위치의 줄 또는 블록설정된 문단전체의 주석 처리를 취소합니다.


## 동일한 단어 선택: **ctrl + d**
커서 위치의 단어와 동일한 단어를 찾아서 선택합니다. 한번 누를 때마다 아래쪽의 동일한 단어가 하나씩 추가로 선택됩니다.

## 패널(터미널) 열기 & 닫기: **ctrl + j**
아래쪽 패널을 열고 닫습니다. 터미널의 디폴트 위치가 현재 열려있는 폴더로 설정돼서, 프로그램을 작성하고 테스트해볼 때 매우 유용합니다.

## 사이드바 열기 & 닫기: **ctrl + b**
왼쪽의 사이드바를 열고 닫습니다. 화면을 분할해서 작업할 때, 에디터 화면을 크게 볼 수 있어서 유용합니다.

## 전체화면: **f11**
브라우저의 전체화면과 비슷하게 작업표시줄과 메뉴바를 숨깁니다.

## Markdown 미리보기: **ctrl + k v**
**ctrl + k**를 누르고 **v**를 누르면, 화면이 분할되고 오른쪽에 미리보기 창이 열립니다.
* 참고 포스트: [Visual Studio Code에서 Markdown(.md) 미리보기](/vscode/markdown/){:target="_blank"}

## 키보드 단축키 설정창: **ctrl + k ctrl + s**
**ctrl**을 누른 상태에서 **k**와 **s**를 순서대로 누르면 키보드 단축키를 확인하고 설정할 수 있는 창이 열립니다.

## 내가 설정해놓은 단축키
![mine](/assets/post-images/vscode-shortcuts/toggleminimap.png)

Activity Bar는 왼쪽 끝의 아이콘 패널입니다. Minimap은 오른쪽 끝에 있는, 코드 전체를 한눈에 보여주는 패널 입니다. 이 두개의 패널은 항상 열려있지만 키보드 단축키 설정창에서 토글키를 설정해주면 숨길 수 있습니다.
노트북으로 작업할 때에 화면이 부족해서 답답한 경우에 전체화면에서 양옆의 패널까지 모두 숨겨주면 훨씬 쾌적하게 작업할 수 있습니다.

## Reference
* [Helmet](https://helmetjs.github.io/){:target="_blank"}

* [Production Best Practices: Security](https://expressjs.com/en/advanced/best-practice-security.html){:target="_blank"}

* [Content Security Policy (CSP)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP){:target="_blank"}

* [CSP: script-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src){:target="_blank"}

* [Content Security Policy](https://developers.google.com/web/fundamentals/security/csp){:target="_blank"}

* [Using Google Tag Manager with a Content Security Policy](https://developers.google.com/tag-manager/web/csp){:target="_blank"}