JVM(Java Virtual Machine) 이란?
JVM은 컴파일된 자바의 바이트코드(.class)들을 OS에서 실행하기 위한 표준 스펙이며 다양한 구현체가 존재한다.

Java 언어 자체는 OS 독립적이지만 JVM은 각 OS에 종속적이다.



JVM의 메모리 구조에 대해서 알아본다.



JVM은 크게 아래와 같이 분류할 수 있다.



Class Loader
JVM Memory
Execution Engine

https://en.wikipedia.org/wiki/Java_virtual_machine


위 구성요소 중 JVM Memory에 대해서 알아본다.



JVM Memory


JVM 메모리는 위 그림과 같이

Method Area
Heap
JVM Language Stacks
PC Registers
Native Method Stacks
로 구성되어 있다.



각각에 대해서 알아보자.





JVM 전체 구조


Source Code(.java) : 우리가 작성한 java 파일
Source Code(소스코드)는 우리가 java 언어로 구현하는 .java 파일을 말한다.



Java Compiler : source code를 byte code로 변환해준다.
우리가 작성한 Source Code(.java 파일)를 JVM에서 실행시킬 수 있는 Byte Code(.class)로 컴파일 시켜준다.

Byte Code(.Class) : JVM에서 실행할 수 있는 


JVM(Java Virtual Machine)


Garbage Collector : 사용하지 않는 객체들을 메모리에서 제거하는 역할

Class Loader : Class 파일을 불러와 메모리에 저장

Execution Engine : Class Loader에 저장된 Byte Code를 명령어 단위로 분류하여 하나씩 실행하게 하는 엔진

Runtime Data Area(Memory Area) : JVM이 프로그램을 실행하기 위해 운영체제로부터 할당받은 메모리 공간



Memory Area
- JVM이 실행되면 생기는 공간



Method Area
Class
전역변수
static 변수
Runtime Constant Pool : 상수
모든 스레드에서 정보 공유
Heap
new 로 생성된 객체
Array와 같이 동적으로 생성된 데이터
Garbage Collector 가 제거하지 않는한 데이터 유지
Reference Type의 데이터
모든 스레드에서 정보 공유
Stack
지역변수
지역변수 이지만 Reference Type인 경우 Heap에 저장된 데이터의 주소값을 Stack에 저장해서 사용
메소드의 매개변수
스레드마다 개별 Stack을 가지고 있음
PC Register
스레드가 생성되면서 생기는 메모리 영역
스레드가 어느 명령어를 처리하고 있는지 그 주소를 등록
JVM이 실행하고 있는 현재 위치를 저장하는 역할
Native Method Stacks
Java가 아닌 다른 언어(C, C++)로 구성된 메소드를 실행할때 사용되는 영역


참조
http://www.tcpschool.com/java/java_intro_programming