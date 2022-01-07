#   DB Lock

---

# Java garbage collection(GC)

##  stop-the-world
stop-the-world란, GC을 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것이다.  
stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다.  
GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작한다. 어떤 GC 알고리즘을 사용하더라도 stop-the-world는 발생한다.  
대개의 경우 GC 튜닝이란 이 stop-the-world 시간을 줄이는 것이다.  

Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않는다.  
가끔 명시적으로 해제하려고 해당 객체를 null로 지정하거나 System.gc() 메서드를 호출하는 개발자가 있다.  
null로 지정하는 것은 큰 문제가 안 되지만, System.gc() 메서드를 호출하는 것은 시스템의 성능에 매우 큰 영향을 끼치므로 System.gc() 메서드는 절대로 사용하면 안 된다(다행히도 NHN에서 System.gc() 메서드를 호출하는 개발자를 보진 못했다).  
Java에서는 개발자가 프로그램 코드로 메모리를 명시적으로 해제하지 않기 때문에 가비지 컬렉터(Garbage Collector)가 더 이상 필요 없는 (쓰레기) 객체를 찾아 지우는 작업을 한다.  

##  가비지 컬렉터가 만들어진 전제 조건
-   대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다.  
-   오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.  


### 참조
-   [JAVA 7 garbage collection](https://d2.naver.com/helloworld/1329)
-   [JAVA 8 이후 garbage collection](https://www.baeldung.com/jvm-garbage-collectors)
-   [What is Java Garbage Collection? How It Works, Best Practices, Tutorials, and More](https://stackify.com/what-is-java-garbage-collection/)

---

#   enum vs constant
-   constant(상수)
-   enum(열거형) : enumeration : 셈, 계산, 열거, 목록

### 참조
-   [Java enum](https://www.nextree.co.kr/p11686/)
-   [what's the advantage of a java enum](https://stackoverflow.com/questions/9969690/whats-the-advantage-of-a-java-enum-versus-a-class-with-public-static-final-fiel)
-   [enum vs constant](https://gorbeia.wordpress.com/2015/03/11/java-enums-vs-constants/)
-   [enum사용법](https://limkydev.tistory.com/66)

---

#   static final vs enum

-   차이점과 이점에 대해 알아보자