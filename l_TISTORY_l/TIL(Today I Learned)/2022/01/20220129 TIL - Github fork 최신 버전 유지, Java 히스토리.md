#   20220129 TIL - Github fork 최신 버전 유지, Java 히스토리

#   GitHub fork repository 최신 버전 유지 하기

[\[GitHub\] fork repository 최신 버전으로 유지하기](https://jybaek.tistory.com/775)


#   Java 1부터 Java 17 까지의 변화

## TL;DL

최신 프로그래밍 언어들(Kotlin, Rust, Clojure 등)이 가지고 있는 개념들(자동 형변환, 함수형 프로그래밍, 자동 병렬 프로세싱을 지원 등)을 Java에서도 새롭게 개발, 적용하고 있다.

Java 8의 지원 기간이 [2030년 12월](https://www.oracle.com/java/technologies/java-se-support-roadmap.html)이므로 기업들의 다음 Java 버전은 Java 17 이상이 될 것이다.

---

현재 회사(솔루션 업체이지만 SM, SI 업체와 비슷하다)에서 주로 사용하는 Java 버전은 7과 8 이다.

대기업들의 SM과 SI를 진행하고 있기 때문에 매우 보수적인 Java 버전이 사용되고 있다.

새로 진행되는 SI들은 그래도 Java 8을 사용하고 있지만 기존에 개발된 프로젝트들은 6, 7 버전이 대부분이다.

이러한 업무 환경 때문에 최신 Java 버전을 사용할 기회가 별로 없었다.

그래서 Java 1 버전(JDK 1.0)부터 특징들을 정리해보려고 한다.

아래는 최신순으로 각 Java 버전별 특징에 대해 정리하였다.


---

##  Java SE 17  (2021년 9월)
### LTS(Long Term Support)

### 특징
-   [JEP 398](https://openjdk.java.net/jeps/398):Java Applet 이 완전 제거될 예정이라 Deprecate 처리
-   신규 벡터 API [다음 버전 정식 지원 예정](https://docs.oracle.com/en/java/javase/17/docs/api/jdk.incubator.vector/module-summary.html)
-   [JEP 391](https://openjdk.java.net/jeps/391): 애플 M1 및 이후(MacOS/AArch64) 프로세서 탑재 컴퓨터 제품군에 대한 정식 지원
-   [JEP 382](https://openjdk.java.net/jeps/382): macOS 그래픽 렌더링 베이스를 OpenGL 에서 Metal 로 교체
-   [JEP 356](https://openjdk.java.net/jeps/356): 의사난수 생성기를 통해 예측하기 어려운 난수를 생성하는 API 정식 추가
-   [JEP 415](https://openjdk.java.net/jeps/415): 컨텍스트 기반의 역직렬화 필터링
-   [JEP 409](https://openjdk.java.net/jeps/409): sealed clasee 정식 추가

---

##  Java SE 16  (2021년 3월)
OpenJDK 소스 GitHub 이관

### 특징
-   [JEP 338](https://openjdk.java.net/jeps/338): Vector API(Incubator)
    -   자동 병렬 프로세싱을 지원하는 자동 벡터 API가 추가될 예정
-   [JEP 347](https://openjdk.java.net/jeps/347): 자바 네이티브(JNI 등) 개발 시 C++14 규격을 지원
-   ZGC 기능이 향상
-   유닉스 도메인 소켓이 지원
-   Alpine Linux 리눅스 지원 추가
-   [JEP 387](https://openjdk.java.net/jeps/387): PermGen 대신 Metaspace 방식을 지원하기 시작
-   ARM 64비트 윈도우 운영체제가 지원
-   MacOS의 경우 실리콘 맥 지원이 시험 빌드에서 네이티브 지원을 시작
-   [JEP 389](https://openjdk.java.net/jeps/389): JNI를 대신할 외부 링크 방식의 인터페이스를 인큐베이팅을 통해 시작한다.
-   [JEP 390](https://openjdk.java.net/jeps/390): 값 유형의 클래스를 동기화에 사용 시 경고 메시지가 개선

```java
public class JEP390 {

    public static void main(String[] args) {

        Double d = 20.0;
        synchronized (d) {} // 컴파일 시 해당 줄 내용과 함께한 경고 메시지가 친절히 표시된다.
    }
}
```

-   JEP 343: jpackage 명령어를 통해 각 운영체제별 자바 프로그램을 설치 패키지(pkg, deb, msi 등)로 생성하는 기능이 정식으로 추가되어 자바 프로그램을 손쉽게 배포하는 가능
-   instanceof 패턴 매칭 정식 기능으로 추가
-   record 데이터 오브젝트 타입 정식 지원
-   자바 9부터 추가되어 자바 내부 API 접근에 대한 경고 무시 (--illegal-access) 기능이 강화되어 내부 API 접근 시도 시 기본적으로 오류와 함께 자바 프로그램이 종료될 수 있도록 강화

---

##  Java SE 15  (2020년 9월)
### 특징
-   EdDSA 암호화 알고리즘 추가
-   스케일링 가능한 낮은 지연의 가비지 컬렉터 추가(ZGC)
-   Solaris 및 SPARC 플랫폼 지원 제거
-   외부 메모리 접근 API (Incubating)
-   sealed class (Preview)
-   멀티 라인 문자열 `"""` 지원

---

##  Java SE 14  (2020년 3월)
### 특징
-   instanceof 패턴 매칭(Preview)

```java
if (!(obj instanceof String s)) {
    .. s.contains(..) ..
} else {
    .. s.contains(..) ..
}
```

-   record 데이터 오브젝트 타입 지원(Preview)
    -   [Record 초안 발표](https://openjdk.java.net/jeps/359)

```java
record Point(int x, int y) { }
```


---

##  Java SE 13  (2019년 9월)
### 특징
-   멀티 라인 문자열을 위한 텍스트 블록 초안 발표 `"""`
-   스위치 표현 개선 - 자바 12에 소개된 스위치 표현에 기능 추가
    -   break 대신 yield 키워드 사용
    -   하나의 case에 여러 개의 구문 사용 가능

```java
var a = switch (day) {
    case MONDAY, FRIDAY, SUNDAY:
        yield 6;
    case TUESDAY:
        yield 7;
    case THURSDAY, SATURDAY:
        yield 8;
    case WEDNESDAY:
        yield 9;
};
```


---

##  Java SE 12  (2019년 3월)
### 특징
-   Switch문을 확장

```java
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
}
```
예전에는 이렇게 써야 했던 Switch문을 아래와 같은 형식으로도 쓸 수 있게 되었다.

```java

switch (day) {
    case MONDAY, FRIDAY, SUNDAY -> System.out.println(6);
    case TUESDAY                -> System.out.println(7);
    case THURSDAY, SATURDAY     -> System.out.println(8);
    case WEDNESDAY              -> System.out.println(9);
}
```

-   가비지 컬렉터 개선
-   마이크로 벤치마크 툴


---

##  Java SE 11  (2018년 9월)
LTS(Long Term Support)

### 특징
-   이클립스 재단으로 넘어간 Java EE가 JDK에서 삭제되고, JavaFX도 JDK에서 분리되어 별도의 모듈로 제공
-   hotspot/jvmti 기능
-   람다 파라미터에 대한 지역 변수 문법
-   엡실론 가비지 컬렉터
-   HTTP 클라이언트 표준화


---

##  Java SE 10  (2018년 3월)
### 특징
-   [var 키워드를 이용한 지역 변수 타입 추론](https://openjdk.java.net/jeps/286)
-   병렬 처리 가비지 컬렉션
-   개별 쓰레드로 분리된 Stop-The-World
-   JDK에서 루트 인증 기관(CA) 인증서의 기본 세트를 제공
-   JVM 힙 영역을 시스템 메모리가 아닌 다른 종류의 메모리에도 할당할 수 있게 됨
-   이전 버전에서 Deprecated 처리된 API는 Java SE 10에서 모두 삭제


---

##  Java SE 9  (2017년)
이후 Java SE의 발표 주기를 6개월로 변경

### 특징
-   런타임 모듈화(Jigsaw)
-   JShell(REPL)
-   통합 JVM 로깅
-   HTML5 JavaDoc
-   try-with-resource 개선
-   익명 클래스에 대한 Diamond Operator 허용
-   구조적 불변 컬렉션
-   HTTP/2
-   private Interface Method
-   프로퍼티 파일에 UTF-8이 지원
-   CompletableFuture 개선
-   Reactive stream API

-   Java Applet 지원 종료


---

##  Java SE 8  (2014년)
LTS(Long Term Support)

32비트를 지원하는 마지막 공식 Java 버전

### 특징
-   **Lambda Expression**
-   **[Functional Interfaces](https://docs.oracle.com/javase/specs/jls/se8/html/jls-9.html#jls-9.8)**
-   **Stream API**
-   **Interface Default Method 추가**
-   **Optional**
-   **Future**
-   새로운 날짜와 시간 API(Ex. JodaTime)
-   PermGen 영역 삭제
-   Annotation on Java Types
-   Unsigned Integer 계산
-   Repeating Annotation
-   Static Link JNI Library
-   Rhino 대신 Nashorn JavaScript 엔진 탑재


---

##  Java SE 7  (2011년)
LTS(Long Term Support)

### 특징
-   Generics 사용성 개선
-   리소스 자동 해제
-   Garbage Collector 기능 개선
-   Dynamic Language 지원
-   **Switch문 문자열 지원**
-   try-with-resource 개선
    -   하나의 catch 내에 여러 개의 Exception을 처리할 수 있도록 개선
-   **Diamond Operator <>**
-   이진수 리터럴
-   숫자 리터럴에 `_` 지원
-   새로운 Concurrency API
-   새로운 File NIO 라이브러리(File NIO 2.0)
-   Elliptic Curve Cryptography
-   Java2D를 위한 XRender
-   Upstream
-   Java Deployment Ruleset 


---

##  Java SE 6  (2006년)
### 특징
-   Scripting Language Support
-   JDBC 4.0
-   Java Compiler API
-   Pluggable Annotation
-   Rhino JavaScript 엔진


---

##  J2SE 5  (2004년)
### 특징
-   Generics
-   Enhanced for Loop
-   Metadata(Annotation)
-   AutoBoxing/UnBoxing
-   Enumeration(Typesafe Enums)
-   [Varargs(가변 인자 메서드)](https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EA%B0%80%EB%B3%80%EC%9D%B8%EC%9E%90Varargs%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
-   static import
-   Concurrency API
-   java.util.Scanner


---

##  J2SE 1.4  (2002년)
1.4부터 [JCP(Java Community Process)](https://www.jcp.org/en/home/index)에 의해 오픈소스로 관리
### 특징
-   assert
-   정규표현식
-   IPv6
-   Non-Blocking IO
-   XML API
-   JCE
-   JSSE
-   JAAS
-   Java Web Start
-   JDBC 3.0


---

##  J2SE 1.3  (2000년)
### 특징
-   HotSpot JVM
-   JNDI
-   JPDA
-   JavaSound
-   RMI가 CORBA를 지원하도록 변경


---

##  J2SE 1.2  (1998년)
JDK1.2부터 Java의 제품은 Standard/Enterprise/Micro로 나눠졌다.

### 특징
-   strictfp
-   Swing GUI
-   JIT(Just In Time)
-   Collections
-   [CORBA](https://docs.oracle.com/javase/7/docs/technotes/guides/idl/corba.html)
-   Java Applet
-   JNI(Java Native Interface)
-   JDBC 2.0


---

##  JDK 1.1  (1997년)
###   특징
-   JavaBeans
-   Java Archive (JAR) 파일 형식
-   Java Database Connectivity (JDBC 1.0)
-   Inner Class
-   RMI(Remote Method Invocation)
-   Reflection
-   Calendar
-   Unicode 지원
-   Internationalization


---

##  JDK 1.0   (1996년)
Java의 공식적인 첫번째 버전이다.

안정화 작업을 거친 1.0.2버전에서 Java로 이름을 변경하였다.


---

#   JDK 1.0a2 (1995년)
Oak라는 이름으로 처음 공식 발표


---

#   JDK 1.0a  (1994년)
그린 프로젝트(Green Project)에서 스마트 가전제품에 사용할 프로세스 독립적인 언어 Oak가 웹 브라우저에 이식되며 Java의 역사가 시작된다.


---

### 참조

[Java 17로 전환을 고려해야 하는 이유](https://velog.io/@riwonkim/Java-17%EB%A1%9C-%EC%A0%84%ED%99%98%EC%9D%84-%EA%B3%A0%EB%A0%A4%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)

[New Features in Java 17](https://www.baeldung.com/java-17-new-features)

[Java 버전별 변경점](https://johngrib.github.io/wiki/java-enhancements/)

[자바 버전별 역사 및 특징](https://techvu.dev/136)

[혼란스러운 Java 버전의 진실](https://www.whatap.io/ko/blog/12/)

[자바 가변인자](https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EA%B0%80%EB%B3%80%EC%9D%B8%EC%9E%90Varargs%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)

[Java/버전](https://namu.wiki/w/Java/%EB%B2%84%EC%A0%84)

[Java Platform, Standard Edition Documentation](https://docs.oracle.com/en/java/javase/index.html)