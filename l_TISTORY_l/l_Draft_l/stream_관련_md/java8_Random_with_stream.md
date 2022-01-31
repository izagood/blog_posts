# java8 랜덤 함수

##      스트림을 이용한 랜덤 출력 함수
```java
public int getRandomNumberUsingInts(int min, int max) {
        Random random = new Random();
        return random.ints(min, max).findFirst().getAsInt();
}
```

##      스트림을 이용한 랜덤 출력
```java
// generate 100 random number between 0 to 100 
int[]  randomIntsArray = IntStream.generate(() -> new Random().nextInt(100)).limit(100).toArray();

//generate 100 random number between 100 to 200
int[]  randomIntsArray = IntStream.generate(() -> new Random().nextInt(100) + 100).limit(100).toArray();

//Math 클래스를 이용
IntStream limit = IntStream.generate(() -> (int)(Math.random() * 100)).limit(2);
limit.forEach(System.out::println);
```

##      스트림을 이용해 랜덤 만든 후 arry 변환
```java
int[] array = IntStream.generate(() -> (int)(Math.random() * 100)).limit(2).toArray();
```

##      랜덤으로 만든 후 List 변환
```java
List<String> collect = IntStream
        .generate(() -> (int)(Math.random() * 1000))
        .limit(100)
        .mapToObj(e1 -> ((Integer)e1).toString())
        .collect(Collectors.toList());
```