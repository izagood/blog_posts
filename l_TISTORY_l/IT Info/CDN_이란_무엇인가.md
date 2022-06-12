#   CDN(Content Delivery Network)이란 무엇인가?

CDN(Content Delivery Network)이란 전세계 사용자에게 웹 콘텐츠를 효율적으로 제공할 수 있는 서버의 분산 네트워크이다.

CDN은 최종 사용자와 가까운 POP(Point-Of-Presence)위치의 서버에 캐시된 콘텐츠를 저장하여 대기 시간을 최소화한다.

컨텐츠는 웹 요소 (텍스트, 그래픽, 스크립트), 다운로드 가능한 요소 (미디어 파일, 소프트웨어, 문서), 애플리케이션 (전자상거래, 포털), 실시간 미디어, 주문형 스트리밍, 그리고 소셜 네트워크 등이 있다.


##  동작 방식

1.  사용자가 도메인 이름이 있는 URL을 사용하여 파일을 요청

2.  DNS는 가장 성능이 좋은 POP 위치로 요청을 라우팅(일반적으로 가장 가까운 POP)

3.  POP 서버의 캐시에 파일이 없으면 POP는 원본 서버에 파일을 요청

4.  원본 서버는 파일을 POP 서버에 응답

5.  POP 서버는 파일을 캐싱하고 사용자에게 파일을 응답  
    파일은 HTTP 헤더로 지정된 TTL(Time-To-Live)이 만료될 때까지 POP 서버에 캐시된 상태로 유지  
    (원본 서버가 TTL을 지정하지 않은 경우, 기본 7일)  

6.  다른 사용자가 요청할 경우 파일의 TTL이 만료되지 않았다면 POP의 캐시된 파일을 응답


## CDN의 장정

-   성능

콘텐츠를 로드하기 위해 장거리의 많은 왕복이 필요한 애플리케이션을 사용 중인 최종 사용자의 성능 및 사용자 환경 향상
e.g. 한국과 미국 서버간 통신을 통해 콘텐츠를 소비하는 사용자

-   가용성

-   병목 현상 해결

-   트래픽 양 감소



-   보안

CDN은 대규모 분산 서버 장비로 공격 트래픽을 완화할 수 있으므로 컨텐츠 제공자에게 DDoS(Distributed Denial of Service) 공격에 대해서 어느정도 보호해 줄 수 있다.


#   참고

[콘텐츠 전송 네트워크](https://www.akamai.com/ko/our-thinking/cdn/what-is-a-cdn)
[Azure의 콘텐츠 배달 네트워크란?](https://docs.microsoft.com/ko-kr/azure/cdn/cdn-overview)
[콘텐츠 전송 네트워크](https://ko.wikipedia.org/wiki/%EC%BD%98%ED%85%90%EC%B8%A0_%EC%A0%84%EC%86%A1_%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)