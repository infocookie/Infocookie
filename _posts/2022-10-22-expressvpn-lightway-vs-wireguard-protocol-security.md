---
layout: default
title: ExpressVPN Lightway vs Wireguard 프로토콜 추천 보안성 비교
date: "2022-10-22 20:30"
description: 고의 VPN 회사인 ExpressVPN은 Lightway라는 훌륭한
  프로토콜을 자체적으로 제작했습니다. 이는 Wireguard라는 새로운
  프로토콜이 대세가 되어가는게 현제 상황인데, 따라가느냐 리드하느냐의
  기로에서 익스프레스VPN은 리드하길 선택한 것 같습니다.
---

# ExpressVPN은 왜 와이어가드 대신 라이트웨이 프로토콜을 만들었을까?

## ExpressVPN의 LIghtway 프로토콜이란?

ExpressVPN이 다른 회사들 처럼 Wireguard를 수정해서 사용하지 않고
처음부터 끝까지 구축한 VPN 프로토콜이 Lightway 입니다. 처음 이
프로토콜을 발표했을 때 많은 사용자가 왜 WireGuard를 채택하지 않고
독자적인 프로토콜을 제작했는지 궁금해했습니다.

실제 ExpressVPN은 와이어가드 초창기 시작 재정적인 기여도 했었다고
합니다. 하지만 세계 1위 VPN 업체로서 몇가지 요인을 고려하지 않을 수
없었다고 합니다. ExpressVPN은 고가의 서비스이지만 3백만이 넘는 유저를
보유하고 있는데, 신기술을 채택할때 최대한 많은 고민을 하지 않을 수
없습니다. 10년이 넘게 쌓아온 신뢰와 평판이 흔들릴 수 있기 때문이죠.

ExpressVPN 측에서 WireGuard를 신중하게 분석한 후, 삼백만 유저를 위한
서비스로 적합하지 않다고 판단한 뒤 WireGuard의 장점을 포함하면서 더 나은
프로토콜을 만들기 위해 Lightway를 개발하기로 결정했다고 밝혔습니다.

**다음은 익스프레스VPN 측에서 Lightway와 WireGuard의 세 가지 주요 차이점
그리고 ExpressVPN 사용자에게 Lightway가 더 적합한 이유에 대해 밝힌 글을
요약한 것 입니다.**

## 1. 개인정보 보호

WireGuard를 Top2 업체인 NordVPN도 그대로 탑재하지 않고, 수정해서
NordLynx라는 프로토콜오 제공중인데요. VPN 서비스 회사 입장에서 볼 땐,
와이어가드가 개인 정보 보호에 단점이 있기 때문입니다.

WireGuard는 서버에 IP 주소를 저장하고 동적할당(DHCP)을 하지 않으며 키는
모든 endpoint 사이에서 미리 설정된 상태에서 접속하기 때문에 이를 통해
시간 경과에 따른 특정 사용자의 트래픽을 쉽게 식별할 수 있습니다고
판단했습니다. WireGuard 보안 자체는 매우 우수하지만, 기본 설계 자체가
접속 대상을 신뢰할 수 있으므로 IP를 숨길 필요가 없고 기존 VPN 서비스들이
제공하는 '익명성' 즉, IP 주소 보안을 위해 설계된 것이 아니기 때문
입니다.

Lightway는 LRU(최소 최근 사용) IP 주소가 할당됩니다. 각 사용자에게 고유
주소가 할당되어 있지만 사용자에게 표시되는 주소는 동일한 서버의 다른
모든 사용자에게 표시되는 동일한 IP 주소입니다. 모든 로그 또는 시스템
정보에는 대체 IP 주소만 표시됩니다.

## 2. TCP와 UDP

Lightway는 서로 다른 이점을 제공하는 두 가지 유형의 인터넷 프로토콜인
TCP와 UDP를 모두 지원합니다. WireGuard는 기본적으로 UDP 전용 프로토콜
입니다.

UDP는 더 빠른 속도를 자랑하지만, 네트워크 관리자 및 방화벽이 차단하기가
더 쉽습니다. 다양한 환경에서 VPN을 사용하기 위해서는 TCP도 함께 사용되는
것이 이점이기 때문에 Lightway는 TCP도 지원하도록 설계되었습니다.

## 3. 난독화

WireGuard는 [공식적으로](https://www.wireguard.com/known-limitations/)
난독화 지원을 염두하지 않았다고 밝혔습니다. 이 또한 좀 더 차단되기가
쉽다는 뜻이 됩니다. 물론 와이어가드 역시 난독화 구현이 가능하지만
전문가가 추가적인 작업을 해야하는 부분이지 우리같은 일반인들이 손댈 수
있는 부분이 아닙니다. Lightway Core에는 난독화 등 기능을 쉽게 추가할 수
있는 내장 플러그인 인프라가 있다고 합니다.

## Lightway 결론

Wireguard는 4000줄 정도의 코드로 이루어져있어, OpenVPN 대비 1% 정도밖에
안되는 초경량 프로토콜이라 보안 유지 및 속도에서 매우 이점이 있는 것으로
알려져있습니다. Lightway는 놀랍게도 와이어가드의 절반인 2000줄 정도밖에
안된다고 합니다.

그리고 Lightway의 핵심 코드 [오픈
소스](https://www.expressvpn.com/blog/lightway-open-source-security-audit/)
로 공개 되어있어 명분과 투명성도 함께 확보하게 되었습니다. Cure53이라는
유명 독일 보안 기업을 통해 Lightway을 독립적으로 감사받는다고 하네요.

직접 사용해보니 굉장히 빠르고, 국가 서버를 바꿀때 거의 실시간으로 바뀌는
느낌입니다. 최근 서버도 업그레이드해서 그런지 Web Download, Torrent
Download 속도 모두 엄청 향상되어서 그렇지않아도 가장 빠른 VPN이었던
ExpressVPN이 넘사벽이 된 느낌입니다.

[VPN 프로토콜 비교글](https://netxhack.com/network/vpn-protocols/) 한번
읽어보시면 큰 도움이 될거라 생각합니다.
