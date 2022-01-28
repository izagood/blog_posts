#   stream map collection 활용하기

stream의 map은 람다를 사용하여 stream 내에 있는 객체들을 변환시키는데 사용한다.

단순 람다 사용 이외에도 collection을 원활히 사용하기 위해 분석한다.



#   Comparator 분석하기

stream에서 정렬할때 sorted를 많이 사용한다.

sorted()를 그냥 사용하면 오름차순 정렬이 되지만 내가 원하는 조건으로 정렬하기 위해서는 sorted​(Comparator<? super T> comparator) 형식으로 사용하여야 한다.

Comparator를 원활하게 사용하기 위해 분석한다.

[Comparator](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Comparator.html)