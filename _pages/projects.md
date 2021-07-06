---
permalink: /projects/
title: "Projects"
---

## [LoLog.me](https://LoLog.me){:target="_blank"} - 리그오브레전드 전적검색 사이트

### 개요
리그오브레전드 유저의 전적을 검색할 수 있는 사이트 입니다. 기본적인 전적 외에 게임 플레이 그래프, 팀별 승률 등의 차별화된 정보를 제공합니다.

### 기술스택
* HTML + CSS + JavaScript
* Node.js
* MySQL
* AWS EC2 Linux
* AWS RDS MySQL

### 스크린샷
<details markdown="1">
<summary style="cursor:pointer;">보기</summary>

![LoLog Menu](/assets/images/portfolio/lolog-main.png)

![LoLog Graph](/assets/images/portfolio/lolog-graph.png)

![LoLog Recent](/assets/images/portfolio/lolog-recent.png)

![LoLog Detail](/assets/images/portfolio/lolog-detail.png)

![LoLog Deal](/assets/images/portfolio/lolog-deal.png)

</details>

### 서비스 소개
<details markdown="1">
<summary style="cursor:pointer;">보기</summary>
[LoLog.me](https://LoLog.me){:target="_blank"}에서 리그오브레전드 유저 닉네임을 검색하면, 유저의 게임 전적 데이터를 확인할 수 있습니다. 최근 2년간의 데이터가 제공되며, 유저들이 흥미로워할만한 여러가지 데이터들이 제공됩니다. 전적 상세 조회 등의 기본 데이터 외에도 팀별 승률 게임 플레이 빈도수 그래프 등의 차별화된 데이터를 추가로 제공합니다.

제공되는 데이터
* 프로필 이미지, 랭크 등의 유저 데이터
* K/D/A, 골드, 레벨, 데미지, 아이템 등의 게임 상세 데이터
* 날짜별, 기간별, 챔피언별, 포지션별 게임 전적 데이터
* 팀별, 게임 길이별 승률

유저 사용성
* 다양한 검색 옵션
* 유저에게 익숙한 게임 클라이언트 내 UI 다수 차용
* 반응형 웹으로 모바일 완벽 지원
* 한국어 / 영어 두가지 언어 제공

</details>

### 개발 후기
<details markdown="1">
<summary style="cursor:pointer;">보기</summary>
웹서비스를 처음부터 끝까지 개발해나가면서 웹 프로그래밍에 관한 지식 뿐만 아니라 도메인, SSL 인증, DB, AWS 서비스 등 다양한 지식을 쌓을 수 있었습니다. 특히, 많은 양의 데이터를 API를 통해 가져오고 가공하여 다시 유저에게 전송하여 보여주는 과정을 서버, 클라이언트, 데이터베이스가 균형있게 분담하게 하여 효율성을 높이고 응답시간을 줄이는 과정은 매우 흥미로웠습니다.

설계 과정에서 주의깊게 고려한 사항들은 게임사 API의 형태와 Rate Limit, 서버와 클라이언트의 부하, 네트워크 통신량, 데이터베이스 용량 등이었습니다. 서버는 게임사 API를 이용하여 데이터를 가져오고 서비스에 필요한 데이터만을 추출하여 데이터베이스에 저장합니다. 서버는 이 데이터들을 JSON 형태로 클라이언트에게 제공합니다. 클라이언트는 가져온 데이터를 직접 가공하여 HTML 문서를 만들고 화면을 표시합니다.

이 과정은 서버가 게임사 API에 동일한 요청을 하지 않도록 하여 서버의 API 호출량과 부하를 줄입니다. 또한 중복되는 HTML 코드를 클라이언트에게 한번만 전송하도록 하여 서버와 클라이언트 간의 네트워크 통신량을 줄입니다. 그리고 데이터베이스에는 필요한 데이터만을 저장하여 데이터베이스 용량이 효율적으로 사용됩니다.

웹 서비스를 완성해나가는 과정에서 프로그래밍 내, 외적으로 시행착오가 많았지만 웹 서비스가 조금씩 발전해나가는 과정을 보면서 뿌듯했습니다. 또한 새로운 지식을 재밌는 방법으로 배워나간다는 사실이 매우 만족스러웠습니다. 이 여러 지식과 더불어 프로젝트를 진행하면서, 앞으로 새로운 프로젝트에 자신감있게 도전할 수 있는 힘을 얻은 것 같습니다.
</details>

### 관련 포스트
* [Category - LoL](/categories/#lol){:target="_blank"}

### GitHub Repository
* [unionyy/lolog-me](https://github.com/unionyy/lolog-me){:target="_blank"}


## 앵무새 - Discord Bot

### 개요
음악을 스트리밍해주고, 간단한 채팅을 할 수 있는 디스코드봇 "앵무새"입니다.

### [앵무새 소개 링크](https://koreanbots.dev/bots/795333228662751253){:target="_blank"}

### 기술스택
* Node.js
* MySQL
* AWS EC2 Linux


## LEGOTRIS (유니티 x LEGO microgame)

### 개요
유니티 x LEGO microgame 공모전 참가용으로 만든 게임입니다. 방향키로 블럭을 움직이고 화살과 레이져를 발사해 위에서 내려오는 블럭이 쌓이지 못하도록 하는 캐주얼 게임입니다.

### [게임 플레이 링크](https://play.unity.com/mg/lego/legotris){:target="_blank"}

### 기술스택
* Unity
* C#

### 스크린샷

![LEGOTRIS Menu](/assets/images/portfolio/legotrismenu.png)

![LEGOTRIS Play](/assets/images/portfolio/legotrisplay.png)

