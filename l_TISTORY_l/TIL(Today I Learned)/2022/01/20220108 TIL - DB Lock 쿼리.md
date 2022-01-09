#   DB Lock을 유발하는 쿼리란?

#   DB Lock
-   DB Lock은 트랜잭션 처리의 순차성을 보장하기 위한 방법

-   공유 Lock
    -   공유 lock 끼리는 동시 접근 가능
-   베타 Lock
    -   데이터를 변경할 때 사용
    -   베타 lock은 해제될 때까지 다른 트랜젝션(읽기 포함)이 해당 리소스에 접근할 수 없다.

참조 : [DB Lock](https://sabarada.tistory.com/121)


#   트랜젝션
-   DB는 트랜젝션 단위로 처리된다.


참조 : [트랜젝션과 격리성](https://sabarada.tistory.com/117)

DB Lock 이란?



DB Lock을 유발하는 쿼리란?