# Stream

<br/>

## 🍕 개요
---

Java8이 나오게 되면서 Stream API이란 개념이 도입되었습니다. 많은 사람들이 Java I/O에서 InputStream 과 OutputStream과 헷갈려 하였는데 이 두개에서의 스트림과는 전혀 다른 것입니다. Java8에서 나온 Stream은 함수형 프로그래밍을 자바로 가져오는데 큰 역할을 한 Monad입니다.
함수형 프로그래밍에서 모나드는 일련의 단계로 정의된 연산을 나타내는 구조입니다. 모나드 구조가 있는 유형은 "연산을 연결하거나 해당 유형의 함수를 함께 중첩하는 것"을 정의 합니다.

<br/>
<br/>

- *스트림은 데이터 처리 연산을 지원하도록 소스에서 추출된 연속된 값 요소*
- *컬렉션의 요소를 하나씩 참조해 람다식으로 처리할 수 있는 반복자*

**-> 스트림은 데이터 컬렉션 반복을 멋지게 처리하는 기능이다.**

<br/>

> 📌 스트림 정의 
>
> '***데이터 처리 연산**을 지원하도록 **소스**에서 추출된 **연속된 요소***'로 정의할 수 있다.


- **연속된 요소** : 컬렉션과 마찬가지로 스트림은 특정 요소 형식으로 이루어진 연속된 값 집합의 인터페이스를 제공한다. 
  - 그러나 컬렉션이 시간과 공간의 복잡성과 관련된 요소 저장 및 접근연산이 주를 이룬다면, 
  - 반면 스트림은 filter, sorted, map처럼 표현 계산식이 주를 이룬다. 

- **소스** : 스트림은 컬렉션, 배열, I/O자원 등의 데이터 제공 소스로부터 데이터를 소비한다.

- **데이터 처리 연산** : 함수형 프로그래밍 언어에서 일반적으로 지원하는 연산과 데이터베이스와 비슷한 연산을 지원한다.( `filter, map, reduce, find, match, sort` )

<br/>

**특징**

- 선언형 : 더 간결하고 가독성 향상
  - -> 데이터 처리 임시 구현 코드 대신 질의로 표현
- 조립가능 : 유연성 향상
  - 고수준 빌딩 블록: filter, sorted, map, collect 등
  - 특정 스레딩 모델에 제한되지 않고 자유롭게 어떤 상황에서 사용 가능
- 병렬화 : 성능 향상
  - 멀티 스레드 코드를 구현하지 않아도 데이터를 투명하게 병렬로 처리 가능

<br/>

**대표적인 스트림 연산자**

- `filter` : 람다를 인수로 받아 스트림에서 특정 요소를 제외시킨다.
- `map` : 람다를 이용해서 한요소를 다른 요소로 변환하거나 정보를 추출한다.
- `limit` : 정해진 개수 이상의 요소가 스트림에 저장되지 못하게 스트림 크기를 축소 한다.
- `collect` : 스트림을 다른 형식으로 변환한다.

<br/>
<br/>
<br/>

## 🍕 Pre Java 8 VS Post Java 8
---

> 스트림의 등장으로 연산에 필요한 매개변수를 사용하지 않게 되었다.
> 
> 스트림을 쓰기 전에는 **How** 중심인 `외부반복`을 사용.
> > 스트림 사용 후 객체에 지시만 하면 되는  **What** 중심의 코드가 되었다.
> >
> > `내부 반복`을 쓰게되면서 직관적인 코드를 짤 수 있음 

<br/>

- 🍺 외부 반복 : 사용자가 for-each 등을 사용해서 직접 요소를 반복하는 것을 말한다.
  - 명시적으로 컬렉션 항목을 하나씩 가져와서 처리함
  - 병렬성을 스스로 관리해야 한다.

<br/>

- 🍺 내부 반복 : 반복자를 이용해서 명시적으로 반복하는 컬렉션과 달리, 스트림은 내부 반복을 지원한다.
  - 작업을 투명하게 병렬로 처리할 수 있다.
  - 더 최적화된 다양한 순서로 처리할 수 있다.
  - filter 나 map 같이 반복을 숨겨주는 연산 리스트가 미리 정의되어 있어야 한다.
  - 반복을 숨겨주는 연산은 대부분 람다 표현식으로 인수를 받는다. 동작 파라미터화를 사용할 수 있다.

<br/>

```java
List<String> highCaloriesDishes = new ArrayList<>();
Iterator<String> iterator = menu.iterator();
while (iterator.hasNext()) {
	Dish dish = iterator.next();
	if (dish.getCalories() > 300) {
		highCaloricDishes.add(d.getName());
	}
}

// Stream사용 리펙토링
List<String> highCaloriesDishes = menu.stream()
			.filter(dish -> dish.getCalories() > 300)
			.map(Dish::getName)
			.collect(toList());
```

<br/>

### 💻 BEFORE JAVA 8

```java
// 연복 1억이 넘는 직장인의 평균을 구하는 코드

int sum = 0;
int count = 0;
for (Employee emp : emps) {
  if (emp.getSalary() > 100) {
    sum += emp.getSalary();
    count++;
  }
}
double average = (double) sum / count;
```

<br/>

### 💻 AFTER JAVA 8

```java
// 연복 1억이 넘는 직장인의 평균을 구하는 코드 (Stream API 사용)

double average = emps.stream()
  .filter(emp -> emp.getSalary() > 100_000_000)
  .mapToInt(Employee::getSalary)
  .average()
  .orElse(0)
  ;
```

<br/>
<br/>
<br/>

## 🍕 스트림과 컬렉션
---

*자바의 기존 컬렉션과 새로운 스트림은 순차적으로 값에 접근한다.*

> DVD와 인터넷 스트리밍을 예로 비교
> 
>> DVD는 이미 영화가 저장되어서 판매된다. 이는 컬렉션에 비유할 수 있다.
>>
>> 반면 인터넷 스트리밍은 사용자가 시청하는 부분의 몇 프레임을 미리 내려받는다.
>>> 때문에 대부분의 값을 처리하지 않은 상태에서 미리 내려받은 프레임부터 재생이 가능하다. 이를 스트림으로 비유할 수 있다.

<br/>

**🍺 컬렉션 = DVD**

- 자료구조가 포함하는 모든 값을 메모리에 저장한다.
- 컬렉션의 모든 요소는 컬렉션에 추가하기 전에 계산되어야 한다.
- 생산자 중심 → 팔기도 전에 창고를 가득 채움.
- 만약 소수를 저장하는 컬렉션을 만들 시에, 끝도 없이 모든 소수를 포함하려 할 것이므로 무한루프를 돌게 된다.
- 영화의 모든 프레임들이 미리 저장되어있는 DVD
- **적극적 생성** → 모든 값을 계산할 때까지 기다린다.

<br/>

**🍺 스트림 = 인터넷 스트리밍**

- 요청할 때만 요소를 계산한다. 
- 고정된 자료구조. → 스트림에 요소를 추가하거나 제거할 수 없다.
- 사용자가 요청하는 값만 스트림에서 추출한다.
- 생성자와 소비자의 관계를 형성한다.
- **게으른 생성** → 필요할 때만 값을 계산한다.

> 자료구조가 포함하는 모든 값을 메소드에 포함하는 컬렉션관 다르게
> 
> 스트림은 요청할 때만 요소를 계산하는 고정된 자료구조를 가진다.
>> 스트림은 (특정 연산자를 사용할 때) 여러 개의 조건이 중첩된 상환에서 값이 결정나면 불필요한 연산을 진행하지 않고 조건문을 빠져나와 실행 속도를 높인다.

<br/>
<br/>
<br/>

## 🍕 스트림 연산 
---

*각 연산자끼리는 점을 찍어서 이어주는데, 이 방식이 파이프끼리 잇는 것과 닮았다고 해서 **파이프라이닝** 이라 부르기도 한다.*

- 📌 **파이프 라이닝** : 대부분의 스트림 연산은 스트림 연산끼리 연결해서 커다란 파이프라인을 구성할 수 있도록 스트림 자신을 반환한다.
  -  게으름(laziness), 쇼트서킷(short-circuiting) 같은 최적화도 얻을 수 있다.

<br/>
<br/>

**📌 쇼트서킷(shortcircuiting)**
> 연산자의 앞 조건식의 결과에 따라 뒤 조건식의 실행 여부를 결정한다.
>
> 이미 결정난 값에 대한 불필요한 연산을 하지 않음으로 실행 속도를 높이는 기능
> > 조건문에서 여러 개의 조건을 중첩할 때, && 연산자와 II 연산자는 참 거짓이 확정되면 뒤의 조건은 검사하지 않는다.

```
💡 조건1 && 조건2 일 경우

조건1이 false라면 조건2를 실행하지 않고 생략한다.
(조건1이 false라면 조건1 && 조건2는 항상 false이기 때문)

-> 거짓일 확률이 높은 조건 / 우선적으로 확인해야 할 조건을 앞에 놓는다.


💡 조건1 || 조건2 일 경우

조건1이 true라면 조건2를 실행하지 않고 생략한다.
(조건1이 true라면 조건1 || 조건2는 항상 true이기 때문)

-> 참일 확률이 높은 조건부터 앞에 놓아야 한다.
```

<br/>
<br/>

- 📌 **스트림은 딱 한 번만 탐색할 수 있다.**
  - 탐색된 스트림의 요소는 소비된다.
  - 때문에 한 번 탐색한 요소를 다시 탐색하려면 초기 데이터 소스에서 새로운 스트림을 생성해야 한다.
  - 그러려면 컬렉션처럼 반복 사용할 수 있는 데이터 소스여야 한다.
  - 데이터 소스가 I/O 라면 소스를 반복 사용할 수 없기 때문에 새로운 스트림을 생성할 수 없다.

```java
List<String> title = Arrays.asList("java8", "In", "Action");
Stream<String> s = title.stream();

s.forEach(System.out::println);
//각 단어 출력 

s.forEach(System.out::println);
// java.lang.IllegalStateException: 스트림이 이미 소비되었거나 닫힘.
```

<br/>
<br/>

### 🍺 1. 스트림 생성
---

- **`.stream()`** 

*컬렉션을 스트림으로 만들어주는 연산자*

<br/>
<br/>

### 🍺 2. 중간 연산 (Intermediate Operations)
---

*데이터를 처리하는 중간 연산자*

*서로 연결되어 `파이프라인`을 형성*
 - 중간 연산의 결과는 스트림을 반환(Return) 해주기 때문에 Operation을 지속적으로 이어 붙일 수 있다.(Chaining)

<br/>

*크게 4가지 행위로 나눌 수 있다.*

- Filtering
- Mapping
- Sorting
- Iterating

<br/>

> 📌 **루프퓨전**
> 
> > filter, map과 같이 서로 다른 연산이 한과정으로 병합 되는 기법.

- SORTED 연산자 사용 시 루프 퓨전
  - **`fiiter` -> `filter` -> `sorted` -> `map` -> `sorted` -> `map`**

*💡 sorted는 중간연산자 이면서 특이하게도 최종연산자처럼 이전 연산자들이 실행되도록 한다.*

<br/>

|   연산   |   형식    |  반환 형식  |   연산의 인수   | 함수 디스크립터 |
| :------: | :-------: | :---------: | :-------------: | :-------------: |
|  filter  | 중간 연산 | `Stream<T>` | `Predicate<T>`  |    `boolean`    |
|   map    | 중간 연산 | `Stream<T>` | `Function<T,R>` |    `T -> R`     |
|  limit   | 중간 연산 | `Stream<T>` |                 |                 |
|  sorted  | 중간 연산 | `Stream<T>` | `Comparator<T>` | `(T, T) -> int` |
| distinct | 중간 연산 | `Stream<T>` |                 |                 |

<br/>
<br/>

### 🍺 3. 최종 연산 (terminal operation)
---

- **`.collect()`**

*연산을 정리하고 결과를 도출하는 최종 연산자*

*파이프라인을 실행한 다음 닫는다.*

*보통 최종 연산에 의해 List, Integer, void 등 스트림 이외의 결과가 반환된다.*

*행위*

- Calculating
- Reduction
- Collecting
- Matching
- Iterating

<br/>

|  연산   |   형식    |                              목적                               |
| :-----: | :-------: | :-------------------------------------------------------------: |
| forEach | 최종 연산 | 스트림의 각 요소를 소비하면서 람다를 적용한다. void를 반환한다. |
|  count  | 최종 연산 |         스트림의 요소 개수를 반환한다. long을 반환한다.         |
| collect | 최종 연산 |   스트림을 리듀스해서 리스트,맵,정수 형식의 컬렉션을 만든다.    |

<br/>
<br/>
<br/>

# 🍕 스트림 활용

<br/>

## 🍺 필터링
---

*스트림의 요소를 필터를 통해 취사 선택할 수 있다.*

<br/>

### Predicate로 필터링

> 🔥 **`filter(Predicate<> predicate)`**
> > `T -> boolean` 형식의 `Predicate` 객체를 이용해서 필터링할 조건을 걸어준다.
> >
> > 람다 및 메서드 참조로 이용 가능

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
        .filter(i -> i < 3) // Predicate를 이용한 람다식
        .forEach(System.out::println);
        // 결과 : 1, 2 
```

<br/>

### 고유 요소 필터링

> 🔥 **`distinct()`**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 1, 2, 4);

numbers.stream()
        .distinct() // 스트림 내의 중복 값을 필터링 
        .forEach(System.out::println);
        // 결과 : 1, 2, 3, 4 
```

<br/>
<br/>

## 🍺 스트림 슬라이싱
---

<br/>

### Predicate를 이용한 슬라이싱

> 🔥 **`takeWhile(Predicate<> predicate)`**
> > predicate를 적용해서 필터링 하되 false가 되는 순간 반복을 멈춘다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
        .takeWhile(i -> i < 3)
        .forEach(System.out::println);
        // 결과 : 1, 2
```

> 🔥 **`dropWhile(Predicate<> predicate)`**
> > predicate가 처음으로 false가 되는 지점까지 발견된 요소를 버린다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 1 ,2);

numbers.stream()
        .dropWhile(i -> i < 3)
        .forEach(System.out::println);
        // 결과 : 3, 4, 5, 1, 2
```

<br/>

### 스트림 축소 및 요소 건너뛰기

> 🔥 **`limit(long maxSize)`**
> > 주어진 값 이하의 크기를 갖는 새로운 스트림을 반환
> 
> > maxSize 만큼 앞에서 요소를 반환한다.

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
        .limit(3)
        .forEach(System.out::println);
        // 결과 : 1, 2, 3
```

> 🔥 **`skip(long n)`**
> > 처음 n개 요소를 제외한 스트림을 반환

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

numbers.stream()
        .skip(3)
        .forEach(System.out::println);
        // 결과 : 4, 5
```

<br/>
<br/>

## 🍺 매핑
---

<br/>

### 스트림 각 요소에 함수 적용

> 🔥 **`map(Funtion<> mapper)`**
> > 함수를 인수로 받아 각 요소에 함수를 적용하고 그 결과가 새로운 요소로 매핑된다.

```java
List<String> words = Arrays.asList("Stream", "Java", "Map");

words.stream()
        .map(String::length) // String의 length 메서드를 메소드 참조로 이용
        .forEach(System.out::println);
        // 결과 : 6, 4, 3
```

<br/>

### 스트림 평면화

> 🔥 **`flatMap(Function<> mapper)`**
> > 스트림의 형태가 배열과 같을 때, 모든 원소를 단일 원소 스트림으로 반환 가능

```java
String[] array = {"Hi", "Hello"};

Arrays.stream(array)
        .map(word -> word.split("")) // 각 단어를 개별 문자를 포함하는 배열로 변환
        .flatMap(Arrays::stream) // 생성된 스트림을 하나의 스트림으로 평면화
        .forEach(System.out::println);
        // 결과 :  H,i,H,e,l,l,o
```

<br/>
<br/>

## 🍺 검색과 매칭
---

<br/>

> 🔥 **`anyMatch(Predicate<> predicate)`**
> > predicate가 주어진 스트림에서 적어도 한 요소와 일치하는지 확인, boolean값 반환

<br/>

> 🔥 **`allMatch(Predicate<> predicate)`**
> > predicate가 주어진 스트림에서 모든 요소와 일치하는지 확인, boolean값 반환

<br/>

> 🔥 **`noneMatch(Predicate<> predicate)`**
> > predicate가 주어진 스트림에서 모든 요소와 일치하지 않는지 확인, boolean값 반환

<br/>

> 🔥 **`findAny()`**
> > 현재 스트림에서 임의의 요소를 반환

<br/>

> 🔥 **`findFirst()`**
> > 스트림에서 첫번째 요소를 반환

<br/>

```
스트림을 직렬로 처리할 때
findAny와 findFirst는 동일한 요소를 리턴 (둘의 차이점 x)

병렬로 처리할 때
findFirst : 무조건 가장 앞에 있는 요소 리턴 
findAny :  멀티 스레드에서 스트림을 처리할 때 가장 먼저 찾은 요소 리턴 
```

<br/>
<br/>

## 🍺 리듀싱
---

*모든 스트림 요소를 처리해서 값으로 도출하는 리듀싱 연산 (= fold)*

<br/>

### 요소의 합

> 🔥 **`reduce(초기값, BinaryOperator<T> accumulator)`**
> > 초깃값이 없는 경우 Optional 객체를 반환

```java
Optional<Integer> sum1 = Arrays.stream(array)
        .reduce(Integer::sum);
System.out.println(sum1); // Optional[15]

Integer sum2 = Arrays.stream(array)
        .reduce(1, (a, b) -> a + b);
System.out.println(sum2); // 16
```

<br/>

### 최대 값과 최소 값

> 🔥 **`min()`**
>
> 🔥 **`max()`**

```java
Integer[] array = {1,2,3,4,5};

Optional<Integer> max = Arrays.stream(array)
        .reduce(Integer::max);

Optional<Integer> min = Arrays.stream(array)
        .reduce(Integer::min);

System.out.println(max); // 5
System.out.println(min); // 1
```

<br/>
<br/>
<br/>

## 💻 사용 예시

<br/>

### 🍺 **`flatMap`**
---

```java 
List<Fish> manyFish = fishes.stream()
  .map(Net::getFishes)
  .flatMap(List::stream)
  .collect(Collectors.toList())
  ;
```

- 리스트나 컬렉션이 중첩되었을 떄 사용
- ex) 리스트가 모여있는 리스트를 하나의 리스트로 만들고 싶을 때 
- `List<List<Fish>>`
  1. Stream을 사용해서 리스트 피쉬를 stream 리스트피쉬로 만든다. 
  2. `flatMap(List::stream)` 을 사용하여 중첩되어 묶여 있는 피쉬를 풀어놓는다.
      - 스트림은 흐르는 강물이라는 뜻을 갖고 있기도 함. 
  3. Collectors.toList()로 한 번 묶어줘서 하나의 리스트로 만든다.

<br/>
<br/>

### 🍺 **`reduce`**
---

`reduce(10, (acc, x) -> acc + x)`

`.reduce([초기화(초기값)], [수행할 연산식])`

- 리듀스는 요소를 하나씩 가져와서 더해감
- 스트림의 요소는 소모된다. 리듀스는 각 요소를 소모해가면서 연산을 처리
- 초기값 작성하지 않으면 `Optional`이 반환된다.

<br/>
<br/>
<br/>

## 스트림 순차처리 / 병렬처리
---

**순차처리 `.stream()`**

```java
List<String> lowCaloricDishesName = menu.stream()
                                      .filter( d -> d.getCalories() < 400 ) //400칼로리 이하의 요리 선택
                                      .sorted(comparing(Dish::getCalories)) // 칼로리로 요리 정렬
                                      .map(Dish::getName) //요리명 추출
                                      .collect(toList()); //모든 요리명을 리스트에 저장
```

<br/>

**병렬처리 `parallelStream()`** 

```java
List<String> lowCaloricDishesName = menu.parallelStream()
                                      .filter( d -> d.getCalories() < 400 ) //400칼로리 이하의 요리 선택
                                      .sorted(comparing(Dish::getCalories)) // 칼로리로 요리 정렬
                                      .map(Dish::getName) //요리명 추출
                                      .collect(toList()); //모든 요리명을 리스트에 저장
```