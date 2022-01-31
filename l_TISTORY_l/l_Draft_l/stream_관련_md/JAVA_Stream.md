# JAVA Streams (스트림)
[스트림 설명](https://futurecreator.github.io/2018/08/26/java-8-streams/)

## 스트림을 사용하는 이유
-	데이터를 추상화하고 처리하여 데이터의 종류와 상관 없이 같은 방식으로 데이터를 처리할 수 있다.  
	따라서 재사용성을 높일 수 있다.
-	가독성 향상
-	병렬화 처리를 통한 성능 향상

## 스트림 기본내용

-	스트림은 '데이터 흐름'이다.
-	자바 8에서 추가한 스트림은 람다를 활용할 수 있는 기술 중 하나
-	람다를 이용해서 코드 양을 줄이고 간결하게 표현할 수 있다.
	-	람다함수는 변수에 할당할 수 있다.
-	배열과 컬렉션을 함수형으로 처리할 수 있다.
-	배열 또는 컬렉션 인스턴스에 함수 여러 개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻을 수 있다.
-	간단하게 병렬 처리(multi-threading)가 가능하다.
	-	하나의 작업을 둘 이상의 작업으로 잘게 나눠서 동시에 진행하는 것을 병렬 처리(parallel processing)라고 하며 여러 쓰레드를 이용해서 많은 요소들을 빠르게 처리할 수 있다.
-	원본의 데이터를 변경하지 않는다.
-	일회용이다.
-	내부 반복으로 작업을 처리한다.

-	Stream의 forEach는 loop가 아니다. 따라서 특정 조건이 발생했을 때 Stream 자체를 중단 시킬 방법이 없다.
	-	커스텀하여 break 처럼 사용 가능하기는 하다.  
		[forEach break 커스텀](.\forEach.md)

# Part1 : 스트림 기본

## 스트림 개관

###	생성하기
-	배열 / 컬렉션 / 빈 스트림
-	Stream.builder() / Stream.generate() / Stream.iterate()
-	기본 타입형 / String / 파일 스트림
-	병렬 스트림 / 스트림 연결하기

###	가공하기
-	Filter
-	Map
-	Sorted
-	Iterating
	
###	결과 만들기
-	Calculating
-	Reduction(축약)
-	Collecting
-	Matching
-	Iterating

## 스트림 과정

1. 생성하기 : 스트림(stream) 인스턴스 생성
2. 가공하기 : 필터링(filtering) 및 맵핑(mapping) 등 원하는 결과를 만들어가는 중간 작업
3. 결과 만들기 : 최종적으로 결과를 만들어내는 작업

-	예 : 전체 -> 필터링 1 -> 필터링 2 -> 매핑 -> 결과 만들기 -> 결과물

###	   1. 생성하기
-	보통 배열과 컬렉션을 이용해서 스트림을 만들지만 이외에도 다양한 방법으로 스트림을 만들 수 있다.

####	배열 스트림

-	Arrays.stream 메소드를 사용
```java
String[] arr = new String[]{"a", "b", "c"};
Stream<String> stream = Arrays.stream(arr);
Stream<String> streamOfArrayPart = Arrays.stream(arr, 1, 3); // 1~2 요소 [b, c]
```

#### 	컬렉션 스트림

-	컬렉션 타입(Collection, List, Set)의 경우 인터페이스에 추가된 디폴트 메소드 stream 을 이용해서 스트림을 만들 수 있다.
```java
List<String> list = Arrays.asList("a", "b", "c");
Stream<String> stream = list.stream();

Stream<String> parallelStream = list.parallelStream(); // 병렬 처리 스트림
```

#### 	비어 있는 스트림

-	비어 있는 스트림(empty streams)도 생성할 수 있다. 요소가 없을 때 null 대신 사용할 수 있다.
```java
List<String> list = new ArrayList<>(); //빈 list 생성
list == null || list.isEmpty() 
    ? Stream.empty() //빈 stream 생성
    : list.stream();
```

#### 	Stream.builder()

-	빌더(Builder)를 사용하면 스트림에 직접적으로 원하는 값을 넣을 수 있다.  
	마지막에 build 메소드로 스트림을 리턴한다.
```java
Stream<String> builderStream = Stream.<String>builder()
    .add("Eric").add("Elena").add("Java")
    .build(); // [Eric, Elena, Java]
```

#### 	Stream.generate()

-	generate 메소드를 이용하면 Supplier<T> 에 해당하는 람다로 값을 넣을 수 있다.
-	Supplier<T> 는 인자는 없고 리턴값만 있는 함수형 인터페이스이다. 람다에서 리턴하는 값이 들어간다.
-	generate 메소드로 생성되는 스트림은 크기가 무한(infinite)하기 때문에 특정 사이즈로 최대 크기를 제한해야 한다.
```java
Stream<String> generatedStream = 
  Stream.generate(() -> "gen").limit(5); // [gen, gen, gen, gen, gen]
```

#### 	Stream.iterate()

-	iterate 메소드를 이용하면 초기값과 해당 값을 다루는 람다를 이용해서 스트림에 들어갈 요소를 만든다.
-	iterate 메소드로 생성되는 스트림은 크기가 무한(infinite)하기 때문에 특정 사이즈로 최대 크기를 제한해야 한다.
```java
Stream<Integer> iteratedStream = Stream.iterate(30, n -> n + 2).limit(5); // [30, 32, 34, 36, 38]
```
#### 	기본 타입형 스트림

-	제네릭을 사용하면 리스트나 배열을 이용해서 기본 타입(int, long, double) 스트림을 생성할 수 있다.  
	하지만 제네릭을 사용하지 않고 직접적으로 해당 타입의 스트림을 다룰 수도 있다.  
	-	range 와 rangeClosed 는 두 번째 인자인 종료지점이 포함되느냐 안되느냐의 범위의 차이이다.  
```java
IntStream intStream = IntStream.range(1, 5); // [1, 2, 3, 4]
LongStream longStream = LongStream.rangeClosed(1, 5); // [1, 2, 3, 4, 5]
```
-	제네릭을 사용하지 않기 때문에 불필요한 오토박싱(auto-boxing)이 일어나지 않는다.  
	필요한 경우 boxed 메소드를 이용해서 박싱(boxing)할 수 있다.
```java
Stream<Integer> boxedIntStream = IntStream.range(1, 5).boxed();
```
-	Java 8 의 Random 클래스는 난수를 가지고 세 가지 타입의 스트림(IntStream, LongStream, DoubleStream)을 만들어낼 수 있다.  
	쉽게 난수 스트림을 생성해서 여러가지 후속 작업을 취할 수 있어 유용하다.
```java
DoubleStream doubles = new Random().doubles(3); // 난수 3개 생성

/* generate를 이용한 랜덤 활용 */
int[]  randomIntsArray = IntStream
.generate(() -> new Random().nextInt(100)).limit(100).toArray(); //0부터 100까지 랜덤 int[] 생성
```
#### 	문자열 스트림

-	스트링을 이용해서 스트림을 생성할수도 있다.  
	다음은 스트링의 각 문자(char)를 IntStream 으로 변환한 예제이다.  
	char 는 문자이지만 본질적으로는 숫자이기 때문에 가능하다.
```java
IntStream charsStream = "Stream".chars(); // [83, 116, 114, 101, 97, 109]
```
-	정규표현식(RegEx)을 이용해서 문자열을 자르고, 각 요소들로 스트림을 만든 예제이다.
```java
Stream<String> stringStream = 
Pattern.compile(", ").splitAsStream("Eric, Elena, Java"); // [Eric, Elena, Java]
```
#### 	파일 스트림

-	자바 NIO 의 Files 클래스의 lines 메소드는 해당 파일의 각 라인을 스트링 타입의 스트림으로 만들어준다.
```java
Stream<String> lineStream = 
  Files.lines(Paths.get("file.txt"), 
              Charset.forName("UTF-8"));
```
#### 	병렬 스트림(Parallel Stream)

-	스트림 생성 시 사용하는 stream 대신 parallelStream 메소드를 사용해서 병렬 스트림을 쉽게 생성할 수 
있다.  
	내부적으로는 쓰레드를 처리하기 위해 자바 7부터 도입된 Fork/Join framework 를 사용한다.
```java
List<String> parallelList = IntStream.generate(() -> new Random().nextInt(100)).limit(100)
	.boxed()
	.map(el -> String.valueOf(el))
	.collect(Collectors.toList());

// 병렬 스트림 생성
Stream<String> parallelStream = parallelList.parallelStream();

// 병렬 여부 확인
boolean isParallel = parallelStream.isParallel();
```
-	따라서 다음 코드는 각 작업을 쓰레드를 이용해 병렬 처리된다.
```java
boolean isMany = parallelStream
	.map(item -> Integer.parseInt(item) * 10)
	.anyMatch(amount -> amount > 200);
```
-	컬렉션이 아닌 경우는 다음과 같이 parallel 메소드를 이용해서 처리한다.
-	다음은 배열을 이용해서 병렬 스트림을 생성하는 경우이다.
```java
int[] randomIntsArray = IntStream.generate(() -> new Random().nextInt(100)).limit(100).toArray();

// 배열을 이용한 병렬 스트림 생성
Arrays.stream(randomIntsArray).parallel();

// int stream 병렬 스트림 생성
IntStream intStream = IntStream.range(1, 150).parallel();
boolean isParallel = intStream.isParallel();
```
-	다시 시퀀셜(sequential) 모드로 돌리고 싶다면 다음처럼 sequential 메소드를 사용한다.  
	뒤에서 한번 더 다루겠지만 반드시 병렬 스트림이 좋은 것은 아니다.
```java
IntStream intStream = intStream.sequential();
boolean isParallel = intStream.isParallel();
```
#### 	스트림 연결하기

-	Stream.concat 메소드를 이용해 두 개의 스트림을 연결해서 새로운 스트림을 만들어낼 수 있다.
```java
Stream<String> stream1 = Stream.of("Java", "Scala", "Groovy");
Stream<String> stream2 = Stream.of("Python", "Go", "Swift");
Stream<String> concat = Stream.concat(stream1, stream2);
// [Java, Scala, Groovy, Python, Go, Swift]
```

### 	2. 가공하기

-	전체 요소 중에서 다음과 같은 API 를 이용해서 내가 원하는 것만 뽑아낼 수 있다.  
	이러한 가공 단계를 중간 작업(intermediate operations)이라고 한다.  
	이러한 작업은 스트림을 리턴하기 때문에 여러 작업을 이어 붙여서(chaining) 작성할 수 있다.
-	배열의 원소를 가공하는데 있어 filter, map, sorted 등 이 있다.

####	Filter
-	스트림 내 요소들을 조건에 따라 하나씩 평가해서 걸러내는 작업을 한다.  
	(if문과 로직이 합쳐진 느낌)  
	인자로 받는 Predicate 는 boolean 을 리턴하는 함수형 인터페이스로 파라미터로는 평가식이 들어간다.
-	길이의 제한, 특정문자포함 등의 작업을 하고 싶을때 사용 가능하다.
```java
List<String> names = Arrays.asList("Eric", "Elena", "Java");

Stream<String> stream = 
  names.stream()
  .filter(name -> name.contains("a")); //"a"가 들어간 스트림만 리턴
  // [Elena, Java]
```

####	Map
-	스트림 내 요소들을 하나씩 특정 값으로 변환해준다.  
	이 때 값을 변환하기 위한 람다를 인자로 받는다.
-	요소들을 대, 소문자 변형 등 의 작업을 하고 싶을때 사용 가능하다.
-	스트림에 들어가 있는 값이 input 이 되어서 특정 로직을 거친 후  
	output(리턴) 이 되어 새로운 스트림에 담긴다.  
	이러한 작업을 맵핑(mapping)이라고 한다.

-	스트림 내 String 의 toUpperCase 메소드를 실행해서 대문자로 변환한 값들이 담긴 스트림을 리턴한다.
```java
List<String> names = Arrays.asList("Eric", "Elena", "Java");

Stream<String> stream = 
  names.stream()
  .map(String::toUpperCase);
// [ERIC, ELENA, JAVA]
```
-	다음처럼 요소 내 들어있는 Product 개체의 필드값(item)을 꺼내올 수도 있다.  
```java
//Product 클래스
public class Product {
	
	String item = "";
	int price = 0;
	
	public String getItem() {
		return item;
	}
	public void setItem(String item) {
		this.item = item;
	}
	public int getPrice() {
		return price;
	}
	public void setPrice(int price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return "Product [item=" + item + ", price=" + price + "]";
	}
}

List<Product> productList = new ArrayList<>();
		
IntStream.generate(() -> new Random().nextInt(100)).limit(100)
.boxed()
.forEach(el -> {
	Product product = new Product();
	product.setItem("item" + String.valueOf(el));
	product.setPrice(el);
	productList.add(product);
});

/* 각 ‘상품’을 ‘item’으로 맵핑한다. */
Stream<String> stream = 
			productList.stream()
			.map(Product::getItem);

System.out.println(stream.collect(Collectors.toList()));
```
#### flatMap

-	map 이외에도 조금 더 복잡한 flatMap 메소드도 있다.
-	파라미터로 mapper를 받고 리턴 타입이 Stream 이다.  
	즉, 새로운 스트림을 생성해서 리턴하는 람다를 파라미터로 넘겨야한다.  
	flatMap 은 중첩 구조를 한 단계 제거하고 단일 컬렉션으로 만들어주는 역할을 한다.  
	이러한 작업을 평탄화(flattening)이라고 한다.

다음과 같은 중첩된 리스트가 있다.
```java
List<List<String>> list = 
  Arrays.asList(Arrays.asList("a"), 
                Arrays.asList("b"));
// [[a], [b]]
```

-	이를 flatMap을 사용해서 중첩 구조를 제거한 후 작업할 수 있습니다.
```java
List<String> flatList = 
  list.stream()
  .flatMap(Collection::stream)
  .collect(Collectors.toList());
// [a, b]
```
-	객체에 적용하면 아래와 같이 코드를 작성할 수 있다.
-	아래 예제에서는 Student 객체를 가진 스트림에서 학생의 국영수 점수를 뽑아 새로운 스트림을 만들어 평균을 구하는 코드이다.  
	이는 map 메소드 자체만으로는 한번에 할 수 없는 기능이다.
```java
students.stream()
  .flatMapToInt(student -> 
                IntStream.of(student.getKor(), 
                             student.getEng(), 
                             student.getMath()))
  .average().ifPresent(avg -> 
                       System.out.println(Math.round(avg * 10)/10.0));
```

####	sorted

-	Sorted 방법은 다른 정렬과 마찬가지로 Comparator 를 이용한다.
-	sorted : 요소들을 정렬해주는 작업을 해준다.

-	인자 없이 그냥 호출할 경우 오름차순으로 정렬한다.
```java
IntStream.of(14, 11, 20, 39, 23)
  .sorted()
  .boxed()
  .collect(Collectors.toList());
// [11, 14, 20, 23, 39]
```
-	인자를 넘기는 경우와 비교해보자.  
	스트링 리스트에서 알파벳 순으로 정렬한 코드와 Comparator 를 넘겨서 역순으로 정렬한 코드이다.
```java
List<String> lang = 
  Arrays.asList("Java", "Scala", "Groovy", "Python", "Go", "Swift");

lang.stream()
  .sorted()
  .collect(Collectors.toList());
// [Go, Groovy, Java, Python, Scala, Swift]

lang.stream()
  .sorted(Comparator.reverseOrder())
  .collect(Collectors.toList());
// [Swift, Scala, Python, Java, Groovy, Go]
```

-	Comparator 의 compare 메소드는 두 인자를 비교해서 값을 리턴한다.
-	기본적으로 Comparator 사용법과 동일하다.  
	이를 이용해서 문자열 길이를 기준으로 정렬해보겠다.
```java
lang.stream()
  .sorted(Comparator.comparingInt(String::length))
  .collect(Collectors.toList());
// [Go, Java, Scala, Swift, Groovy, Python]

lang.stream()
  .sorted((s1, s2) -> s2.length() - s1.length())
  .collect(Collectors.toList());
// [Groovy, Python, Scala, Swift, Java, Go]
```

####	peek

-	스트림 내 요소들 각각을 대상으로 특정 연산을 수행하는 메소드로는 peek 이 있다.  
	‘peek’ 은 그냥 확인해본다는 단어 뜻처럼 특정 결과를 반환하지 않는 함수형 인터페이스 Consumer 를 인자로 받는다.  
	따라서 스트림 내 요소들 각각에 특정 작업을 수행할 뿐 결과에 영향을 미치지 않는다.  
	다음처럼 작업을 처리하는 중간에 결과를 확인해볼 때 사용할 수 있습니다.
```java
int sum = IntStream.of(1, 3, 5, 7, 9)
  .peek(System.out::println)
  .sum();
```

### 	3. 결과 만들기
-	가공한 스트림을 가지고 내가 사용할 결과값으로 만들어내는 단계이다.  
	따라서 스트림을 끝내는 최종 작업(terminal operations)이다.

####	Calculating(계산)

-	스트림 API 는 다양한 종료 작업을 제공한다.  
	최소(min), 최대(max), 합(sum), 평균(average) 등 기본형 타입으로 결과를 만들어낼 수 있다.
```java
long count = IntStream.of(1, 3, 5, 7, 9).count();
long sum = LongStream.of(1, 3, 5, 7, 9).sum();
```

-	만약 스트림이 비어 있는 경우 count 와 sum 은 0을 출력하면 된다.  
	하지만 평균(average), 최소(min), 최대(max)의 경우에는 표현할 수가 없기 때문에 Optional 을 이용해 리턴한다.
```java
OptionalInt min = IntStream.of(1, 3, 5, 7, 9).min();
OptionalInt max = IntStream.of(1, 3, 5, 7, 9).max();
```
-	스트림에서 바로 ifPresent 메소드를 이용해서 Optional 을 처리할 수 있다.
```java
DoubleStream.of(1.1, 2.2, 3.3, 4.4, 5.5)
  .average()
  .ifPresent(System.out::println);
```

####	Reduction(축약)

-	스트림은 reduce(축약)라는 메소드를 이용해서 결과를 만들어 낸다.  
	람다 예제에서 살펴봤듯이 스트림에 있는 여러 요소의 총합을 낼 수도 있다.
-	reduce 메소드는 총 세 가지의 파라미터를 받을 수 있다.
	-	identity : 계산을 위한 초기값으로 스트림이 비어서 계산할 내용이 없더라도 이 값은 리턴.
	-	accumulator : 각 요소를 처리하는 계산 로직. 각 요소가 올 때마다 중간 결과를 생성하는 로직.
	-	combiner : 병렬(parallel) 스트림에서 나눠 계산한 결과를 하나로 합치는 동작하는 로직.
	```java
	// 1개 (accumulator)
	Optional<T> reduce(BinaryOperator<T> accumulator);

	// 2개 (identity)
	T reduce(T identity, BinaryOperator<T> accumulator);

	// 3개 (combiner)
	<U> U reduce(U identity,
	BiFunction<U, ? super T, U> accumulator,
	BinaryOperator<U> combiner);
	```
	-	파라미터 1개  
		BinaryOperator<T> 는 같은 타입의 파라미터 두 개를 받아 같은 타입의 결과를 반환하는 함수형 인터페이스이다.  
		다음 예제에서는 두 값을 더하는 람다를 넘겨주고 있다.  
		따라서 결과는 6(1 + 2 + 3)이 됩니다.
		```java
		OptionalInt reduced = 
		IntStream.range(1, 4) // [1, 2, 3]
		.reduce((a, b) -> {
			return Integer.sum(a, b);
		}); //6
		```
	-	파라미터 2개  
		 여기서 10은 초기값이고, 스트림 내 값을 더해서 결과는 16(10 + 1 + 2 + 3)이 된다.  
		 여기서 람다는 메소드 참조(method reference)를 이용해서 넘길 수 있다.
		```java
		int reducedTwoParams = 
			IntStream.range(1, 4) // [1, 2, 3]
			.reduce(10, Integer::sum); // method reference
			//16
		```
	-	파라미터 3개
		-	아래 코드는 Combiner이 호출되지 않는다.
		```java
		Integer reducedParams = Stream.of(1, 2, 3)
			.reduce(10, // identity
					Integer::sum, // accumulator
					(a, b) -> {
						System.out.println("combiner was called");
						return a + b;
					});
		```
		-	Combiner 는 병렬 처리 시 각자 다른 쓰레드에서 실행한 결과를 마지막에 합치는 단계이다.  
			따라서 병렬 스트림에서만 동작한다.
		```java
		Integer reducedParallel = Arrays.asList(1, 2, 3)
			.parallelStream()
			.reduce(10,
					Integer::sum,
					(a, b) -> {
						System.out.println("combiner was called");
						return a + b;
					});
		/* 결과
			combiner was called
			combiner was called
			36
		*/
		```
		-	결과는 다음과 같이 36이 나온다.  
			먼저 accumulator 는 총 세 번 동작한다.  
			초기값 10에 각 스트림 값을 더한 세 개의 값(10 + 1 = 11, 10 + 2 = 12, 10 + 3 = 13)을 계산한다.  
			Combiner 는 identity 와 accumulator 를 가지고 여러 쓰레드에서 나눠 계산한 결과를 합치는 역할이다.  
			12 + 13 = 25, 25 + 11 = 36 이렇게 두 번 호출된다.

####	Collect

-	Collector 타입의 인자를 받아서 처리를 한다.  
	자주 사용하는 작업은 Collectors 객체에서 제공하고 있다.

```java
//Product 클래스
public class Product {
	
	String item = "";
	int price = 0;
	
	public Product(String item, int price) {
		this.item = item;
		this.price = price;
	}

	public String getItem() {
		return item;
	}
	public void setItem(String item) {
		this.item = item;
	}
	public int getPrice() {
		return price;
	}
	public void setPrice(int price) {
		this.price = price;
	}

	@Override
	public String toString() {
		return "Product [item=" + item + ", price=" + price + "]";
	}
}
```
#####	Collectors.toList()

-	스트림에서 작업한 결과를 담은 리스트로 반환한다.
```java
//List 데이터 생성
List<Product> productList = 
  Arrays.asList(new Product("potatoes", 1000),
                new Product("orange", 1500),
                new Product("lemon", 2000),
                new Product("bread", 2500),
                new Product("sugar", 3000));
```
```java
List<String> collectorCollection =
  productList.stream()
    .map(Product::getItem)
    .collect(Collectors.toList());
// [potatoes, orange, lemon, bread, sugar]
```
#####	Collectors.joining()

-	스트림에서 작업한 결과를 하나의 스트링으로 이어 붙일 수 있다.
```java
String listToString = 
 productList.stream()
  .map(Product::getItem)
  .collect(Collectors.joining());
// potatoesorangelemonbreadsugar
```
-	Collectors.joining 은 세 개의 파라미터를 받을 수 있다.  
	이를 이용하면 간단하게 스트링을 조합할 수 있습니다.
	-	delimiter : 각 요소 중간에 들어가 요소를 구분시켜주는 구분자
	-	prefix : 결과 맨 앞에 붙는 문자
	-	suffix : 결과 맨 뒤에 붙는 문자
```java
String listToString = 
 productList.stream()
  .map(Product::getItem)
  .collect(Collectors.joining(", ", "<", ">"));
// <potatoes, orange, lemon, bread, sugar>
```
#####	Collectors.averageingInt()

-	숫자 값(Integer value )의 평균(arithmetic mean)을 낸다.
```java
Double averagePrice = 
 productList.stream()
  .collect(Collectors.averagingInt(Product::getPrice));
// 2000.0
```
#####	Collectors.summingInt()

-	숫자값의 합(sum)을 낸다.
```java
Integer summingAmount = 
 productList.stream()
  .collect(Collectors.summingInt(Product::getPrice));
// 10000
```

-	IntStream 으로 바꿔주는 mapToInt 메소드를 사용해서 좀 더 간단하게 표현할 수 있다.
```java
Integer summingAmount = 
  productList.stream()
  .mapToInt(Product::getPrice)
  .sum();
  // 10000
```
#####	Collectors.summarizingInt()

-	만약 합계와 평균 모두 필요하다면 스트림을 두 번 생성해야 할까? 이런 정보를 한번에 얻을 수 있는 방법으로 summarizingInt 메소드가 있다.
```java
IntSummaryStatistics statistics = 
 productList.stream()
  .collect(Collectors.summarizingInt(Product::getPrice));
  //IntSummaryStatistics{count=5, sum=10000, min=1000, average=2000.000000, max=3000}
```
	-	개수 getCount()
	-	합계 getSum()
	-	평균 getAverage()
	-	최소 getMin()
	-	최대 getMax()  
	이를 이용하면 collect 전에 이런 통계 작업을 위한 map 을 호출할 필요가 없게 된다.  
	위에서 살펴본 averaging, summing, summarizing 메소드는 각 기본 타입(int, long, double)별로 제공된다.
#####	Collectors.groupingBy()

-	특정 조건으로 요소들을 그룹지을 수 있다.  
	가격을 기준으로 그룹핑해보겠다.  
	여기서 받는 파라미터는 함수형 인터페이스 Function 입니다.
```java
List<Product> productList = 
  Arrays.asList(new Product("potatoes", 1000),
                new Product("orange1", 1500),
                new Product("orange2", 1500),
                new Product("lemon", 2000),
                new Product("bread", 2500),
                new Product("sugar", 3000));

Map<Integer, List<Product>> collectorMapOfLists =
 productList.stream()
  .collect(Collectors.groupingBy(Product::getPrice));
```

-	결과는 Map 타입으로 나오는데, 같은 가격이면 리스트로 묶어서 보여준다.
```java
{2000=[Product [item=lemon, price=2000]], 
2500=[Product [item=bread, price=2500]], 
3000=[Product [item=sugar, price=3000]], 
1000=[Product [item=potatoes, price=1000]], 
1500=[Product [item=orange1, price=1500], Product [item=orange2, price=1500]]}

```
#####	Collectors.partitioningBy()

-	위의 groupingBy 함수형 인터페이스 Function 을 이용해서 특정 값을 기준으로 스트림 내 요소들을 묶었다면, partitioningBy 은 함수형 인터페이스 Predicate 를 받습니다.  
	Predicate 는 파리미터를 받아서 boolean 값을 리턴합니다.
```java
Map<Boolean, List<Product>> mapPartitioned = 
  productList.stream()
  .collect(Collectors.partitioningBy(el -> el.getPrice() > 1500));
```

-	따라서 평가를 하는 함수를 통해서 스트림 내 요소들을 true 와 false 두 가지로 나눌 수 있다.
```java
{false=[Product [item=potatoes, price=1000], Product [item=orange1, price=1500], Product [item=orange2, price=1500]], 
true=[Product [item=lemon, price=2000], Product [item=bread, price=2500], Product [item=sugar, price=3000]]}
```
#####	Collectors.collectingAndThen()

-	특정 타입으로 결과를 collect 한 이후에 추가 작업이 필요한 경우에 사용할 수 있다.  
	이 메소드의 시그니쳐는 다음과 같습니다.  
	finisher 가 추가된 모양인데, 이 피니셔는 collect 를 한 후에 실행할 작업을 의미한다.
	```java
	public static<T,A,R,RR> Collector<T,A,RR> collectingAndThen(
		Collector<T,A,R> downstream,
		Function<R,RR> finisher) { ... }
	```
-	collect 한 후 리턴된 클래스의 함수를 2번째 파라미터에서 사용하면 된다.
```java
//Collectors.toSet 을 이용해서 결과를 Set 으로 collect 한 후 수정불가한 Set 으로 변환하는 작업을 추가로 실행하는 코드이다.
Set<Product> unmodifiableSet = 
 productList.stream()
  .collect(Collectors.collectingAndThen(Collectors.toSet(),
                                        Collections::unmodifiableSet));

//collect하여 Map으로 리턴된 결과를 keySet 함수를 사용하여 key 값만 가져오는 코드이다.
Set<Integer> collect = productList.stream()
		.collect(Collectors
				.collectingAndThen(Collectors.groupingBy(Product::getPrice), Map::keySet));
		System.out.println(collect);
```
#####	Collector.of()

-	이 외에 필요한 로직이 있다면 직접 collector 를 만들 수도 있다.  
	accumulator 와 combiner 는 reduce 에서 살펴본 내용과 동일하다.
```java
public static<T, R> Collector<T, R, R> of(
  Supplier<R> supplier, // new collector 생성
  BiConsumer<R, T> accumulator, // 두 값을 가지고 계산
  BinaryOperator<R> combiner, // 계산한 결과를 수집하는 함수.
  Characteristics... characteristics) { ... }
```
-	다음 코드에서는 Collector 를 하나 생성한다.  
	컬렉터를 생성하는 Supplier 에 LinkedList 의 생성자를 넘겨준다.  
	그리고 accumulator 에는 리스트에 추가하는 add 메소드를 넘겨주고 있다.  
	따라서 이 컬렉터는 스트림의 각 요소에 대해서 LinkedList 를 만들고 요소를 추가하게 된다.  
	마지막으로 combiner 를 이용해 결과를 조합하는데, 생성된 리스트들을 하나의 리스트로 합치고 있다.
```java
Collector<Product, ?, LinkedList<Product>> toLinkedList = 
  Collector.of(LinkedList::new, 
               LinkedList::add, 
               (first, second) -> {
                 first.addAll(second);
                 return first;
               });
```
-	따라서 다음과 같이 collect 메소드에 우리가 만든 커스텀 Collector를 넘겨줄 수 있고, 결과가 담긴 LinkedList 가 반환된다.
```java
LinkedList<Product> linkedListOfPersons = 
  productList.stream()
  .collect(toLinkedList);
```
####	Matching

-	매칭은 조건식 람다 Predicate 를 받아서 해당 조건을 만족하는 요소가 있는지 체크한 결과를 리턴한다.  
	다음과 같은 세 가지 메소드가 있다.
	-	anyMatch : 하나라도 조건을 만족하는 요소가 있는지
	-	allMatch : 모두 조건을 만족하는지
	-	noneMatch : 모두 조건을 만족하지 않는지
```java
List<String> names = Arrays.asList("Eric", "Elena", "Java");

boolean anyMatch = names.stream()
  .anyMatch(name -> name.contains("a")); //true

boolean allMatch = names.stream()
  .allMatch(name -> name.length() > 3); //true

boolean noneMatch = names.stream()
  .noneMatch(name -> name.endsWith("s")); //true
```
####	Iterating

-	foreach 는 요소를 돌면서 실행되는 최종 작업이다.  
	보통 System.out.println 메소드를 넘겨서 결과를 출력할 때 사용하곤 한다.  
	앞서 살펴본 peek 과는 중간 작업과 최종 작업의 차이가 있다.
```java
names.stream().forEach(System.out::println);
```

# Part2 : 스트림 고급

## 개관

-	동작 순서
-	성능 향상
-	스트림 재사용
-	지연 처리(Lazy Invocation)
-	Null-safe 스트림 생성하기
-	줄여쓰기(Simplified)

##	동작 순서

-	다음 스트림에서는 최종 작업인 findFirst 메소드를 호출한다.
```java
List<String> list = Arrays.asList("b", "a", "c");

list.stream()
  .filter(el -> {
    System.out.println("filter() was called.");
    return el.contains("a");
  })
  .map(el -> {
    System.out.println("map() was called.");
    return el.toUpperCase();
  })
  .findFirst();
```
-	요소는 3개인데 결과는 다음처럼 filter 두 번, map 이 한 번 출력됩니다.
```java
filter() was called.
filter() was called.
map() was called.
```
-	여기서 스트림이 동작하는 순서를 알아낼 수 있다.  
	모든 요소가 첫 번째 중간 연산을 수행하고 남은 결과가 다음 연산으로 넘어가는 것이 아니라, 한 요소가 모든 파이프라인을 거쳐서 결과를 만들어내고, 다음 요소로 넘어가는 순서이다.
## 성능 향상
-	위에서 살펴봤듯이 스트림은 한 요소씩 수직적으로(vertically) 실행된다.  
	여기에 스트림의 성능을 개선할 수 있는 힌트가 숨어있다.  
	요소들의 범위를 줄이는 작업을 먼저 실행하는 것이 불필요한 연산을 막을 수 있어서 성능을 향상시킬 수 있다.
-	skip, filter, distinct 를 앞쪽 파이프라인에 연결해서 최대한 요소의 수를 줄이고 스트림을 사용한다.

##	스트림 재사용

-	종료 작업을 하지 않는 한 하나의 인스턴스로서 계속해서 사용이 가능하다.  
	하지만 종료 작업을 하는 순간 스트림이 닫히기 때문에 재사용은 할 수 없다.  
	스트림은 저장된 데이터를 꺼내서 처리하는 용도이지 데이터를 저장하려는 목적으로 설계되지 않았기 때문이다.
-	아래 예제에서 findFirst 메소드를 실행하면서 스트림이 닫히기 때문에 findAny 하는 순간 런타임 예외(runtime exception)이 발생한다.  
	컴파일러가 캐치할 수 없기 때문에 Stream 이 닫힌 후에 사용되지 않는지 주의해야 한다.
```java
Stream<String> stream = 
  Stream.of("Eric", "Elena", "Java")
  .filter(name -> name.contains("a"));

Optional<String> firstElement = stream.findFirst();
Optional<String> anyElement = stream.findAny(); //IllegalStateException: stream has already been operated upon or closed
```
-	위 코드는 아래 코드처럼 바꿀 수 있다.  
	데이터를 List 에 저장하고 필요할 때마다 스트림을 생성해 사용한다.
```java
List<String> names = 
  Stream.of("Eric", "Elena", "Java")
  .filter(name -> name.contains("a"))
  .collect(Collectors.toList());

Optional<String> firstElement = names.stream().findFirst();
Optional<String> anyElement = names.stream().findAny();
```

##	지연 처리(Lazy Invocation)

-	스트림에서 최종 결과는 최종 작업이 이루어질 때 계산된다.  
	호출 횟수를 카운트하는 예제이다.
```java
private long counter;
private void wasCalled() {
  counter++;
}
```
-	다음 예제에서 리스트의 요소가 3개이기 때문에 총 세 번 호출되어 결과가 3이 출력될 것으로 예상된다.  
	하지만 출력값은 0이다.
```java
List<String> list = Arrays.asList("Eric", "Elena", "Java");
counter = 0;
Stream<String> stream = list.stream()
  .filter(el -> {
    wasCalled();
    return el.contains("a");
  });
System.out.println(counter); // 0 ??
```
-	왜냐하면 최종 작업이 실행되지 않아서 실제로 스트림의 연산이 실행되지 않았기 때문이다.  
	다음 예제처럼 최종 작업인 collect 메소드를 호출한 결과 3이 출력된다.
```java
list.stream().filter(el -> {
  wasCalled();
  return el.contains("a");
}).collect(Collectors.toList());
System.out.println(counter); // 3
```
##	Null-safe 스트림 생성하기

-	NullPointerException 은 개발 시 흔히 발생하는 예외이다.  
	Optional 을 이용해서 null에 안전한(Null-safe) 스트림을 생성해보겠습니다.
```java
public <T> Stream<T> collectionToStream(Collection<T> collection) {
    return Optional
      .ofNullable(collection)
      .map(Collection::stream)
      .orElseGet(Stream::empty);
  } 
```
-	위 코드는 파라미터로 받은 컬렉션 객체를 이용해 옵셔널 객체를 만들고 스트림을 생성후 리턴하는 메소드이다.  
	그리고 만약 컬렉션이 비어있는 경우라면 빈 스트림을 리턴하도록 한다.

-	제네릭을 이용해 어떤 타입이든 받을 수 있다.
```java
List<Integer> intList = Arrays.asList(1, 2, 3);
List<String> strList = Arrays.asList("a", "b", "c");

Stream<Integer> intStream = 
  collectionToStream(intList); // [1, 2, 3]
Stream<String> strStream = 
  collectionToStream(strList); // [a, b, c]
```
-	이제 null 로 테스트를 해보자.  
	다음과 같이 리스트에 null 이 있다면 NPE 가 날 수 밖에 없는 상황이다.  
	외부에서 인자로 받은 리스트로 작업을 하는 경우에 일어날 수 있는 상황이다.
```java
List<String> nullList = null;

nullList.stream()
  .filter(str -> str.contains("a"))
  .map(String::length)
  .forEach(System.out::println); // NPE!
```
-	하지만 위에서 만든 collectionToStream 메소드를 이용하면 NPE 가 발생하는 대신 빈 스트림으로 작업을 마칠 수 있다.
```java
collectionToStream(nullList)
  .filter(str -> str.contains("a"))
  .map(String::length)
  .forEach(System.out::println); // []
```
##	줄여쓰기(Simplified)

-	스트림 사용 시 다음과 같은 경우에 같은 내용을 좀 더 간결하게 줄여쓸 수 있다.  
	IntelliJ 를 사용하면 다음과 같은 경우에 줄여쓸 것을 제안해준다.
```java
collection.stream().forEach() 
  → collection.forEach()
  
collection.stream().toArray() 
  → collection.toArray()

Arrays.asList().stream() 
  → Arrays.stream() or Stream.of()

Collections.emptyList().stream() 
  → Stream.empty()

stream.filter().findFirst().isPresent() 
  → stream.anyMatch()

stream.collect(counting()) 
  → stream.count()

stream.collect(maxBy()) 
  → stream.max()

stream.collect(mapping()) 
  → stream.map().collect()

stream.collect(reducing()) 
  → stream.reduce()

stream.collect(summingInt()) 
  → stream.mapToInt().sum()

stream.map(x -> {...; return x;}) 
  → stream.peek(x -> ...)

!stream.anyMatch() 
  → stream.noneMatch()

!stream.anyMatch(x -> !(...)) 
  → stream.allMatch()

stream.map().anyMatch(Boolean::booleanValue) 
  → stream.anyMatch()

IntStream.range(expr1, expr2).mapToObj(x -> array[x]) 
  → Arrays.stream(array, expr1, expr2)

Collection.nCopies(count, ...) 
  → Stream.generate().limit(count)

stream.sorted(comparator).findFirst() 
  → Stream.min(comparator)
```
###	!!!주의!!!
-	특정 케이스에서 조금 다르게 동작할 수 있다.
-	예를 들면 다음의 경우 stream 을 생략할 수 있지만,
```java
collection.stream().forEach() 
  → collection.forEach()
```
-	다음 경우에서는 동기화(synchronized)는 차이가 있다.
```java
// not synchronized
Collections.synchronizedList(...).stream().forEach()
  
// synchronized
Collections.synchronizedList(...).forEach()
```
-	다른 예제는 다음과 같이 collect 를 생략하고 바로 max 메소드를 호출하는 경우이다.
```java
stream.collect(maxBy()) 
  → stream.max()
```
-	하지만 스트림이 비어서 값을 계산할 수 없을 때의 동작은 다르다.  
	전자는 Optional 객체를 리턴하지만,  
	후자는 NullPointerExcpetion 이 발생할 가능성이 있습니다.
```java
collect(Collectors.maxBy()) // Optional
Stream.max() // NPE 발생 가능
```

# 참고 링크
[for문 내 if문 처리](https://stackoverflow.com/questions/23308193/break-or-return-from-java-8-stream-foreach)
[stream을 이용한 map 사용](https://uchupura.tistory.com/108)
[스트림 설명](https://futurecreator.github.io/2018/08/26/java-8-streams/)
[자바 stream](https://dpdpwl.tistory.com/81)
[자바 stream 생성하기](https://beomseok95.tistory.com/217)