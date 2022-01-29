#   stream map collection 활용하기

stream의 map은 람다를 사용하여 stream 내에 있는 객체들을 변환시키는데 사용한다.

단순 람다 사용 이외에도 collection을 원활히 사용하기 위해 분석한다.


### 참조

#   Comparator 분석하기

stream에서 정렬할때 sorted를 많이 사용한다.

sorted()를 그냥 사용하면 오름차순 정렬이 되지만 내가 원하는 조건으로 정렬하기 위해서는 sorted​(Comparator<? super T> comparator) 형식으로 사용하여야 한다.

Comparator를 원활하게 사용하기 위해 분석한다.
### 참조

[Comparator](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Comparator.html)

#   람다 함수란?

@FunctionalInterface인 경우 람다 표현식을 적용시킬 수 있다.

Interface를 Override할때 단 하나의 함수만 존재하는 경우 람다 표현식을 사용할 수 있고 이것이 @FunctionalInterface이다.

https://openjdk.java.net/jeps/11
### 참조
[[JAVA] 람다식(Lambda)의 개념 및 사용법](https://khj93.tistory.com/entry/JAVA-%EB%9E%8C%EB%8B%A4%EC%8B%9DRambda%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B4%EA%B3%A0-%EC%82%AC%EC%9A%A9%EB%B2%95)