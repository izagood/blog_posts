#   PG 결제 망 취소(망상 취소)
-   망취소 : 결제 후 각종 오류로 인해서 결제가 취소되는 것을 말한다.
-   PG 제공 API를 사용하면 된다.
-   Java의 경우 jar로 제공되고 JSP 파일 중 취소 부분에 DB 처리 에러 발생시 호출하는 예시가 있다.

#   request remote address 가져오기
-   RequestContextHolder 는 Spring에서 전역으로 Request에 대한 정보를 가져오고자 할 때 사용하는 유틸성 클래스
-   MVC 모델에서는 이 방법을 사요하면 된다.

```java
HttpServletRequest request = ((ServletRequestAttributes) RequestContextHolder.getRequestAttributes()).getRequest();

request.getRemoteAddr();
```

request.getRemoteAddr() 를 조회하면 request 쓰레드 단위로 address를 가져올 수 있다.

참조
[Spring RequestContextHolder](https://gompangs.tistory.com/entry/Spring-RequestContextHolder)

#   서버 로컬 IP 가져오기
-   InetAddress.getLocalHost();
-   이 방법은 서버의 로컬 IP를 가져오기 때문에 실제 API에서 요청을 보내는 IP와 다를 수 있다.
    -   예를 들어 WAS와 WEB이 나누어져 있을 경우 WAS의 아이피를 가져오지만 실제 WEB의 아이피로 요청이 나간다.
-   단일 서버에서 직접 request를 보내는 경우를 제외하고는 이 방식으로 불러오면 일반적으로 실제 원격지에 요청하는 IP와 다르다.