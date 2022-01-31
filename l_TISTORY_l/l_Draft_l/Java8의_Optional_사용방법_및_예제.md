# Java8의 Optional 사용 방법 및 예제

-   Optional은 어떤 객체를 wrapping하는 객체입니다. 즉, 어떤 객체를 포함할 수 있고 또는 null 객체를 포함할 수 있습니다. 자바의 null 처리를 유연하게 하고자 도입된 것 같습니다.
    ```java
    String string = "a string in optional";
    Optional<String> opString = Optional.of(string);
    System.out.println(opString.get());
    ```

-   만약 null을 wrapping하는 Optional 객체를 만드려면 어떻게 해야 할까요? Optional.of(null)은 허용되지 않습니다. Optional.of()는 null이 아닌 객체만 사용할 수 있습니다. 반면에 Optional.ofNullable()은 객체 생성 시 null을 허용합니다. 이를 이용하면 null을 포함하는 Optional 객체를 만들 수 있습니다.
    ```java
    String nullString = null;
    Optional<String> nullOpString = Optional.ofNullable(nullString);

    // 또는 이렇게 해도 null이 들어감
    Optional<String> emptyOptional = Optional.empty();
    ```

-   isPresent() : null인지 체크하고 사용하기 위한 method
    ```java
    if(findFirst.isPresent()){
        System.out.println("null 아님");
    }
    ```

-   ifPresent() : null인지 체크하고 사용하기 위한 method
    ```java
    //null이 아닐때만 출력됨.
    findFirst.ifPresent(System.out::println);
    ```

-    orElse() : null일때 다른 값을 같도록 하는 method
    ```java
    ///만약 Optional이 null인 경우 orElse()의 param이 리턴됩니다.
    Optional<String> opString = Optional.of("a string in optional");
    Optional<String> nullOpString = Optional.ofNullable(nullString);

    String str = opString.orElse("new string from orElse");
    System.out.println(str);

    String str2 = nullOpString.orElse("new string from orElse");
    System.out.println(str2);
    ```

-    orElseGet() : null일 때 특정함수 실행 및 결과 대입
    ```java
    Optional<String> opString = Optional.of("a string in optional");
    Optional<String> nullOpString = Optional.ofNullable(nullString);

    String str3 = opString.orElseGet(() -> "new string from orElseGet");
    System.out.println(str3);

    String str4 = nullOpString.orElseGet(() -> "new string from orElseGet");
    System.out.println(str4);
    ```

-    orElseThrow() : null일때 exception 던지기
    ```java
    Optional<String> opString = Optional.of("a string in optional");
    Optional<String> nullOpString = Optional.empty();

    try {
        String str5 = opString.orElseThrow(NullPointerException::new);
        System.out.println(str5);
    } catch (NullPointerException e) {
        System.out.println("NullPointerException");
    }

    try {
        String str6 = nullOpString.orElseThrow(NullPointerException::new);
        System.out.println(str6);
    } catch (NullPointerException e) {
        System.out.println("NullPointerException");
    }
    ```

-    filter() : Predicate 조건에 부합할 때만 Optional 객체를 리턴한다.
    ```java
    Optional<String> opStr1 = Optional.of("first string");
    Optional<String> opStr2 = Optional.of("second string");

    Optional<String> filtered1 = opStr1.filter(s -> s.contains("first"));
    Optional<String> filtered2 = opStr2.filter(s -> s.contains("first"));
    
    filtered1.ifPresent(System.out::println);
    filtered2.ifPresent(System.out::println);

    /* -------------------------------출력--------------------------------------- */
    first string
    ```