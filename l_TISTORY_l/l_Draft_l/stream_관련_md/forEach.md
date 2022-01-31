#   forEach 문

## forEach
- Stream의 forEach는 loop가 아니다. 따라서 특정 조건이 발생했을 때 Stream 자체를 중단 시킬 방법이 없다.
-	for문을 람다식으로 처리하기 위해서 추가됨.
-   stream은 모든 요소가 파이프라인을 지나는데 이를 멈춰줄 방법이 없다.  
    for문을 사용하면 break문을 사용하여 해당하는 조건에 일치하면 다음 요소를 돌지 않지만  
    stream은 해당 조건이 충족되어도 모든 요소를 전부 도는 문제가 있다.  
    그렇지만 break 기능이 누락되어 있기 때문에 break 기능을 커스텀하여 사용하여야 한다.

-   java9 이상에서는 takeWhile()을 사용하여 break를 사용할 수 있다.
    ```java
    Stream.of("cat", "dog", "elephant", "fox", "rabbit", "duck")
    .takeWhile(n -> n.length() % 2 != 0)
    .forEach(System.out::println);
    ```

    해당 takeWhile의 코드를 참조하여 적용한다.
    ```java
    public static <T> Stream<T> takeWhile(Stream<T> stream, Predicate<T> predicate) {
        CustomSpliterator<T> customSpliterator = new CustomSpliterator<>(stream.spliterator(), predicate);
        return StreamSupport.stream(customSpliterator, false);
    }
    ```

### forEach break 커스텀 방법1 - Custom Spliterator

-   Spliterator 커스텀
```java

public class CustomSpliterator<T> extends Spliterators.AbstractSpliterator<T> {

    private Spliterator<T> splitr;
    private Predicate<T> predicate;
    private boolean isMatched = true;

    public CustomSpliterator(Spliterator<T> splitr, Predicate<T> predicate) {
        super(splitr.estimateSize(), 0);
        this.splitr = splitr;
        this.predicate = predicate;
    }

    @Override
    public synchronized boolean tryAdvance(Consumer<? super T> consumer) {
        boolean hadNext = splitr.tryAdvance(elem -> {
            if (predicate.test(elem) && isMatched) {
                consumer.accept(elem);
            } else {
                isMatched = false;
            }
        });
        return hadNext && isMatched;
    }
}

```

-   사용 예시
```java
@Test
public void whenCustomTakeWhileIsCalled_ThenCorrectItemsAreReturned() {
    Stream<String> initialStream = 
      Stream.of("cat", "dog", "elephant", "fox", "rabbit", "duck");

    List<String> result = 
      CustomTakeWhile.takeWhile(initialStream, x -> x.length() % 2 != 0)
        .collect(Collectors.toList());

    assertEquals(asList("cat", "dog"), result);
}
```

### forEach break 커스텀 방법2 - Custom forEach

-   forEach 커스텀
```java

public class CustomForEach {

    public static class Breaker {
        private boolean shouldBreak = false;

        public void stop() {
            shouldBreak = true;
        }

        boolean get() {
            return shouldBreak;
        }
    }

    public static <T> void forEach(Stream<T> stream, BiConsumer<T, Breaker> consumer) {
        Spliterator<T> spliterator = stream.spliterator();
        boolean hadNext = true;
        Breaker breaker = new Breaker();

        while (hadNext && !breaker.get()) {
            hadNext = spliterator.tryAdvance(elem -> {
                consumer.accept(elem, breaker);
            });
        }
    }
}

```

-   사용 예시
```java

@Test
public void whenCustomForEachIsCalled_ThenCorrectItemsAreReturned() {
    Stream<String> initialStream = Stream.of("cat", "dog", "elephant", "fox", "rabbit", "duck");
    List<String> result = new ArrayList<>();

    CustomForEach.forEach(initialStream, (elem, breaker) -> {
        if (elem.length() % 2 == 0) {
            breaker.stop();
        } else {
            result.add(elem);
        }
    });

    assertEquals(asList("cat", "dog"), result);
}

```

## forEach문 테스트 케이스
```java
@Test
@DisplayName("forEach break문 커스텀")
public void forEachCustomTest() {
    
    /* break문을 커스텀 하여 사용 */
    
    int[] randomIntsArray = IntStream.generate(() -> new Random().nextInt(100)).limit(100).toArray();
    
    List<Integer> readList = new ArrayList<>();
    List<Integer> MatchList = new ArrayList<>();
    
    List<Integer> collect = CustomTakeWhile.takeWhile(Arrays.stream(randomIntsArray).boxed().filter(item -> {
        System.out.print("현재 숫자: " + item + "  ");
        readList.add(item);
        return item < 50;
    }), item -> {
        if (item < 10) {
            System.out.println("break");
            return false;
        }
        System.out.println("매칭 숫자: " + item);
        MatchList.add(item);
        return true;
    }).collect(Collectors.toList());
    System.out.println("collect List : " + collect);
    
    System.out.println("===================================================================================================");
    System.out.println("모든 숫자 List: " + Arrays.stream(randomIntsArray).collect(ArrayList::new, List::add, List::addAll));
    System.out.println("모든 숫자: " + Arrays.stream(randomIntsArray).collect(ArrayList::new, List::add, List::addAll).size());
    System.out.println("매칭된 숫자 List: " + MatchList);
    System.out.println("읽은 숫자 List: " + readList );
    
    
}
```


## 참조 링크
[forEach break 누락 보완](https://www.baeldung.com/java-break-stream-foreach)