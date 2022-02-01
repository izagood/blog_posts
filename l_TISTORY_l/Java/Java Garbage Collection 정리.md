#   Java Garbage Collection 정리

##  서론



---

##  stop-the-world

stop-the-world란, GC을 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것이다.  
stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춘다.  
GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작한다. 어떤 GC 알고리즘을 사용하더라도 stop-the-world는 발생한다.  
대개의 경우 GC 튜닝이란 이 stop-the-world 시간을 줄이는 것이다.  

Java는 프로그램 코드에서 메모리를 명시적으로 지정하여 해제하지 않는다.  
가끔 명시적으로 해제하려고 해당 객체를 null로 지정하거나 System.gc() 메서드를 호출하는 개발자가 있다.  
null로 지정하는 것은 큰 문제가 안 되지만, System.gc() 메서드를 호출하는 것은 시스템의 성능에 매우 큰 영향을 끼치므로 System.gc() 메서드는 절대로 사용하면 안 된다(다행히도 NHN에서 System.gc() 메서드를 호출하는 개발자를 보진 못했다)  
Java에서는 개발자가 프로그램 코드로 메모리를 명시적으로 해제하지 않기 때문에 가비지 컬렉터(Garbage Collector)가 더 이상 필요 없는 (쓰레기) 객체를 찾아 지우는 작업을 한다.  

---

##  가비지 컬렉터가 만들어진 전제 조건

-   대부분의 객체는 금방 접근 불가능 상태(unreachable)가 된다.  
-   오래된 객체에서 젊은 객체로의 참조는 아주 적게 존재한다.  

이러한 가설을 'weak generational hypothesis'라 한다.  

이 가설의 장점을 최대한 살리기 위해서 HotSpot VM에서는 크게 2개로 물리적 공간을 나누었다.  
둘로 나눈 공간이 Young 영역과 Old 영역이다.  

Young 영역(Yong Generation 영역): 새롭게 생성한 객체의 대부분이 여기에 위치한다.  
대부분의 객체가 금방 접근 불가능 상태가 되기 때문에 매우 많은 객체가 Young 영역에 생성되었다가 사라진다.  
이 영역에서 객체가 사라질때 Minor GC가 발생한다고 말한다.  

Old 영역(Old Generation 영역): 접근 불가능 상태로 되지 않아 Young 영역에서 살아남은 객체가 여기로 복사된다.  
대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생한다.  
이 영역에서 객체가 사라질 때 Major GC(혹은 Full GC)가 발생한다고 말한다.

이외에 영역이 또 있다.

Permanent Generation 영역(이하 Perm 영역)은 Method Area라고도 한다.  
객체나 억류(intern)된 문자열 정보(out of memory error를 방지하기 위해 String pool에서 동일한 값이 있으면 해당 주소를 가져온다.)를 저장하는 곳이며, Old 영역에서 살아남은 객체가 영원히 남아 있는 곳은 절대 아니다.  
이 영역에서 GC가 발생할 수도 있는데, 여기서 GC가 발생해도 Major GC의 횟수에 포함된다.

그렇다면 "Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 경우가 있을 때에는 어떻게 처리될까?"라고 궁금해 하는 분도 더러 있을 것이다.  
이러한 경우를 처리하기 위해서 Old 영역에는 512바이트의 덩어리(chunk)로 되어 있는 카드 테이블(card table)이 존재한다.  

카드 테이블에는 Old 영역에 있는 객체가 Young 영역의 객체를 참조할 때마다 정보가 표시된다.  
Young 영역의 GC를 실행할 때에는 Old 영역에 있는 모든 객체의 참조를 확인하지 않고, 이 카드 테이블만 뒤져서 GC 대상인지 식별한다.

카드 테이블은 write barrier를 사용하여 관리한다. write barrier는 Minor GC를 빠르게 할 수 있도록 하는 장치이다.  
write barrirer때문에 약간의 오버헤드는 발생하지만 전반적인 GC 시간은 줄어들게 된다.

##  Young 영역의 구성

Young 영역은 3개의 영역으로 나뉜다.  

Eden 영역  
Survivor 영역(2개)  
Survivor 영역이 2개이기 때문에 총 3개의 영역으로 나뉘는 것이다.  
각 영역의 처리 절차를 순서에 따라서 기술하면 다음과 같다.  

### 참고

[Java Garbage Collection Basics](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)
[Java Garbage Collection : JAVA 7 garbage collection](https://d2.naver.com/helloworld/1329)
[JVM Garbage Collectors : JAVA 8 이후 garbage collection](https://www.baeldung.com/jvm-garbage-collectors)
