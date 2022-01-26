#   stream API, for문 무엇을 사용해야 할까?
평소 stream이 for문 보다 느리다는 것은 코딩 테스트를 통해서 경험으로는 알고 있었지만

어떤 이유로 느린지 정확히 알지 못 하였다.

stream에 대해 공부하던 중 관련 내용을 분석한 미디엄 글을 찾게 되어 공부해본다.

#   TL;DR
stream이 느린 이유는 반복의 최적화 문제가 있다.

(최근 만든 API이기 때문에 for-loop 처럼 긴 시간 최적화를 거치지 못 했다.)

-   primitive type을 사용할 때는 for-loop이 압도적으로 빠르다.(15배 이상)
-   wrapped type을 사용할 떄는 for-loop이 근소하게 빠르다.(1.27배 차이)

##  결론
-   primitive type : for-loop
-   wrapped type : for-loop이 근소하게 빠르나 stream을 사용하여도 무방


### 참조
[Java Stream API는 왜 for-loop보다 느릴까?](https://jypthemiracle.medium.com/java-stream-api%EB%8A%94-%EC%99%9C-for-loop%EB%B3%B4%EB%8B%A4-%EB%8A%90%EB%A6%B4%EA%B9%8C-50dec4b9974b)