#   DISTINCT의 성능

-   distinct를 추가했을 때 sort unique를 수행하여 작업량이 2배가 됨
-   count로 group by 수행되었지만 내부 '컬럼' 당 sort unique를 실행하기 때문이다.

##  추가적인 sort와 중복제거 개선 방법

-   

### 참조

[COUNT(Distinct 컬럼)의 성능](https://scidb.tistory.com/entry/COUNTDistinct-%EC%BB%AC%EB%9F%BC%EC%9D%98-%EC%84%B1%EB%8A%A5)

#   오라클 메모리(PGA, SGA)

-   PGA(Program Global Area) - 사용자마다 공유하지 않고 개별적으로 사용

-   SGA(System Global Area) - 모든 사용자가 공유 가능하여 사용


### 참조

[3장. 오라클 메모리(PGA, SGA)](https://1duffy.tistory.com/18)