# JAVA Interface 메소드 정리

-	Interface : default method, static method 사용 가능(JAVA8 이후)


##  static
-   인터페이스가 static키워드로 선언되면 메소드가 구현될 수 있다.
    -	default와 다른점은 static method는 재정의 불가하며
    -   클래스 변수와 마찬가지로 객체를 생성하지 않고 '클래스명.메서드명'으로만 호출 가능하다.

-   Static 메서드가 되면 호출 시간이 짧아진다.
    -   Static을 안 붙인 메서드(인스턴스 메서드)는 실행 시,  
        호출되어야 할 메서드를 찾는 과정이 추가적으로 필요하기 때문에 시간이 더 걸린다.

-   Static method는 인스턴스 변수를 사용할 수 없다.
    -   Static method는 인스턴스 생성 없이 호출 가능하므로  
        Static method가 호출되었을 때, 인스턴스가 존재하지 않을 수도 있다.  
        따라서, Static method에서 인스턴스 변수를 사용해서는 안된다.  

    -   이와 반대로,Instance method에서는 Static이 붙은 멤버들을 사용하는 것이 언제나 가능하다.  
        (인스턴스 변수가 존재한다는 것은 Static 변수가 이미 메모리에 존재한다는 것을 의미하기 때문)

    ### static 적용
    -   메서드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려

##  default

-	인터페이스가 default키워드로 선언되면 메소드가 구현될 수 있다.  
	또한 이를 구현하는 클래스는 default메소드를 오버라이딩 할 수 있다.  
	인터페이스를 구현할 때 모든 메소드를 구현해야하는 불편함을 해결하기 위해서 필요한 메소드는 인터페이스에 메소드를 구현해 놓을 수 있도록 하였다.

##  instance

-	Static method와는 달리, 반드시 객체를 생성한 후에 호출 가능하다.  
	Instance method는 인스턴스가 반드시 존재해야만 사용할 수 있다.

##  abstract

-   추상 클래스는 body부분


