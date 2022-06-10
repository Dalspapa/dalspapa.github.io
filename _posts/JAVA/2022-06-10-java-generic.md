# Generic

*데이터 형식에 의존하지 않고, 하나의 값이 여러 다른 데이터 타입들을 가질 수 있도록 하는 방법*

> 제네릭(Generic)은 클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것을 의미한다. 한마디로 특정(Specific) 타입을 미리 지정해주는 것이 아닌 필요에 의해 지정할 수 있도록 하는 일반(Generic) 타입이라는 것이다.
> > 정확히 말하자면 지정된다는 것 보다는 타입의 경계를 지정하고, 컴파일 때 해당 타입으로 캐스팅하여 매개변수화 된 유형을 삭제하는 것.

<br/>

## 장점
---
1. 제네릭을 사용하면 잘못된 타입이 들어올 수 있는 것을 컴파일 단계에서 방지할 수 있다.
2. 클래스 외부에서 타입을 지정해주기 때문에 따로 타입을 체크하고 변환해줄 필요가 없다. 즉, 관리하기가 편하다.
3. 비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.

<br/>

**`<T>`** : Type

**`<E>`** : Element

**`<K>`** : Key

**`<V>`** : Value

**`<N>`** : Number

<br/>
<br/>

## ⌨ 사용방법

<br/>

### 🍟 클래스 및 인터페이스 선언
---

```java
public class ClassName <T> { ... }
public Interface InterfaceName <T> { ... }

// 제네릭 타입 두 개 지정 가능. 
public class ClassName <T, K> { ... }
public Interface InterfaceName <T, K> { ... }
 
// HashMap의 경우 아래와 같이 선언되어있을 것이다.
public class HashMap <K, V> { ... }
```
> T 타입은 해당 블럭 { ... } 안에서까지 유효하다.

<br/>

```java
public class ClassName <T, K> { ... }

// 사용자가 정의한 클래스
public class Student { ... }
 
public class Main {
	public static void main(String[] args) {
    // T는 String, K는 Integer
		ClassName<String, Integer> a = new ClassName<String, Integer>();

    // 레퍼런스타입이므로 가능
    ClassName<Student> a = new ClassName<Student>();
	}
}
```

> 주의해야 할 점은 타입 파라미터로 명시할 수 있는 것은 참조 타입(**Reference Type**)밖에 올 수 없다. 
> > `int, double, char` 같은 **primitive type**은 올 수 없다
> >
> > `Integer, Double` 같은 **Wrapper Type**으로 사용.

<br/>
<br/>

### 🍟 제네릭 클래스
---

**`제네릭 1개`**

```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드
		return element;
	}
	
}
 
class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		
	}
}
```

<br/>

> ClassName이란 객체를 생성할 때 <> 안에 타입 파라미터(Type parameter)를 지정
> > `a객체의 ClassName의 E 제네릭 타입`은 **String**으로 모두 변환
> >
> > `b객체의 ClassName의 E 제네릭 타입`은 **Integer**으로 모두 변환

<br/>

```
# CONSOLE

a data : 10
a E Type : java.lang.String

b data : 10 
b E Type : java.lang.Intager
```

<br/>

**`제네릭 2개`**

```java
// 제네릭 클래스 
class ClassName<K, V> {	
	private K first;	// K 타입(제네릭)
	private V second;	// V 타입(제네릭) 
	
	void set(K first, V second) {
		this.first = first;
		this.second = second;
	}
	
	K getFirst() {
		return first;
	}
	
	V getSecond() {
		return second;
	}
}
 
// 메인 클래스 
class Main {
	public static void main(String[] args) {
		
		ClassName<String, Integer> a = new ClassName<String, Integer>();
		
		a.set("10", 10);
 
 
		System.out.println("  fisrt data : " + a.getFirst());
		// 반환된 변수의 타입 출력 
		System.out.println("  K Type : " + a.getFirst().getClass().getName());
		
		System.out.println("  second data : " + a.getSecond());
		// 반환된 변수의 타입 출력 
		System.out.println("  V Type : " + a.getSecond().getClass().getName());
	}
}
```

<br/>

```
# CONSOLE

first data : 10 
K Type : java.lang.String

second data : 10 
V Type : java.lang.Intager
```

<br/>
<br/>

### 🍟 제네릭 메소드
----

```java
public <T> T genericMethod(T o) {	// 제네릭 메소드
		...
}
 
[접근 제어자] <제네릭타입> [반환타입] [메소드명]([제네릭타입] [파라미터]) {
	// 텍스트
}
```

<br/>

> 클래스와는 다르게 반환타입 이전에 <> 제네릭 타입 선언

<br/>

`제네릭클래스에 제네릭메소드 적용`

```java
// 제네릭 클래스
class ClassName<E> {
	
	private E element;	// 제네릭 타입 변수
	
	void set(E element) {	// 제네릭 파라미터 메소드
		this.element = element;
	}
	
	E get() {	// 제네릭 타입 반환 메소드 
		return element;
	}
	
	<T> T genericMethod(T o) {	// 제네릭 메소드
		return o;
	}
 
	
}
 
public class Main {
	public static void main(String[] args) {
		
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
		
		a.set("10");
		b.set(10);
	
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력 
		System.out.println("a E Type : " + a.get().getClass().getName());
		
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력 
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
		
		// 제네릭 메소드 Integer
		System.out.println("<T> returnType : " + a.genericMethod(3).getClass().getName());
		
		// 제네릭 메소드 String
		System.out.println("<T> returnType : " + a.genericMethod("ABCD").getClass().getName());
		
		// 제네릭 메소드 ClassName b
		System.out.println("<T> returnType : " + a.genericMethod(b).getClass().getName());
	}
}
```

<br/>

> ClassName이란 객체를 생성할 때 <> 안에 타입 파라미터(Type parameter)를 지정
> > a객체의 ClassName의 E 제네릭 타입은 String으로 모두 변환
> >
> > b객체의 ClassName의 E 제네릭 타입은 Integer으로 모두 변환
> >
> > genericMethod()는 파라미터 타입에 따라 T 타입이 결정

<br/>

```
# CONSOLE
a data : 10
a E Type : java.lang.String

b data : 10
b E Type : java.lang.Integer

<T> returnType : java.lang.Integer
<T> returnType : java.lang.String
<T> returnType : ClassName
```

> *클래스에서 지정한 제네릭유형과 별도로 메소드에서 독립적으로 제네릭 유형을 선언 가능*

<br/>

> ❓ WHY
> 
> `static method` 선언시 필요
> 
> > 스태틱 메소드 객체 생성 전에 이미 메모리에 올라가기 때문에 타입을 지정할 방법이 없다.
> > > ***제네릭이 사용되는 메소드를 정적메소드로 두고 싶은 경우 제네릭 클래스와 별도로 독립적인 제네릭이 사용되어야 한다***

<br/>

`static generic method`

```java
class ClassName<E> {
 
	private E element; // 제네릭 타입 변수
 
	void set(E element) { // 제네릭 파라미터 메소드
		this.element = element;
	}
 
	E get() { // 제네릭 타입 반환 메소드
		return element;
	}
 
	// 아래 메소드의 E타입은 제네릭 클래스의 E타입과 다른 독립적인 타입이다.
	static <E> E genericMethod1(E o) { // 제네릭 메소드
		return o;
	}
 
	static <T> T genericMethod2(T o) { // 제네릭 메소드
		return o;
	}
 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<String> a = new ClassName<String>();
		ClassName<Integer> b = new ClassName<Integer>();
 
		a.set("10");
		b.set(10);
 
		System.out.println("a data : " + a.get());
		// 반환된 변수의 타입 출력
		System.out.println("a E Type : " + a.get().getClass().getName());
 
		System.out.println();
		System.out.println("b data : " + b.get());
		// 반환된 변수의 타입 출력
		System.out.println("b E Type : " + b.get().getClass().getName());
		System.out.println();
 
		// 제네릭 메소드1 Integer
		System.out.println("<E> returnType : " + ClassName.genericMethod1(3).getClass().getName());
 
		// 제네릭 메소드1 String
		System.out.println("<E> returnType : " + ClassName.genericMethod1("ABCD").getClass().getName());
 
		// 제네릭 메소드2 ClassName a
		System.out.println("<T> returnType : " + ClassName.genericMethod1(a).getClass().getName());
 
		// 제네릭 메소드2 Double
		System.out.println("<T> returnType : " + ClassName.genericMethod1(3.0).getClass().getName());
	}
}
```

<br/>

```
# CONSOLE

a data : 10 
a E Type : java.lang.String

b data : 10
b E Type : java.lang.Integer

<E> returnType : java.lang.Integer
<E> returnType : java.lang.String 
<T> returnType : ClassName
<T> returnType : java.lang.Double
```

<br/>
<br/>
<br/>

## 제한된 Generic과 와일드 카드
---

```
<K extends T>	// T와 T의 자손 타입만 가능 (K는 들어오는 타입으로 지정 됨)
<K super T>	// T와 T의 부모(조상) 타입만 가능 (K는 들어오는 타입으로 지정 됨)
 
<? extends T>	// T와 T의 자손 타입만 가능
<? super T>	// T와 T의 부모(조상) 타입만 가능
<?>		// 모든 타입 가능. <? extends Object>랑 같은 의미
```

**`extends T`** : 상한 경계

**`? super T`** : 하한 경계

**`<?>`** : 와일드 카드(Wild card)

```
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 K는
 * 지정된 타입으로 변환이 된다.
 */
<K extends Number>
 
 
/*
 * Number와 이를 상속하는 Integer, Short, Double, Long 등의
 * 타입이 지정될 수 있으며, 객체 혹은 메소드를 호출 할 경우 지정 되는 타입이 없어
 * 타입 참조를 할 수는 없다.
 */
<? extends T>	// T와 T의 자손 타입만 가능
```

> 특정 타입의 데이터를 조작하고자 할 경우에는 K 같이 특정 제네릭 인수로 지정을 해야 한다.

<br/>

### extends
---

```
<T extends B>	// B와 C타입만 올 수 있음
<T extends E>	// E타입만 올 수 있음
<T extends A>	// A, B, C, D, E 타입이 올 수 있음
 
<? extends B>	// B와 C타입만 올 수 있음
<? extends E>	// E타입만 올 수 있음
<? extends A>	// A, B, C, D, E 타입이 올 수 있음
```

> 제네릭 클래스에서 수를 표현하는 클래스만 받고 싶은 경우
> > 대표적인 Integer, Long, Byte, Double, Float, Short 같은 래퍼 클래스들은 Number 클래스를 상속 
> > > `public class ClassName <K extends Number> { ... }`

<br/>

```java
public class ClassName <K extends Number> { 
	... 
}
 
public class Main {
	public static void main(String[] args) {
 
		ClassName<Double> a1 = new ClassName<Double>();	// OK!
 
		ClassName<String> a2 = new ClassName<String>();	// error!
	}
}
```

<br/>
<br/>

### super
---

```
<K super B>	// B와 A타입만 올 수 있음
<K super E>	// E, D, A타입만 올 수 있음
<K super A>	// A타입만 올 수 있음
 
<? super B>	// B와 A타입만 올 수 있음
<? super E>	// E, D, A타입만 올 수 있음
<? super A>	// A타입만 올 수 있음
```

> 해당 객체가 업캐스팅(Up Casting)이 될 필요가 있을 때 사용


예로들어 '과일'이라는 클래스가 있고 이 클래스를 각각 상속받는 '사과'클래스와 '딸기'클래스가 있다고 가정해보자.

이 때 각각의 사과와 딸기는 종류가 다르지만, 둘 다 '과일'로 보고 자료를 조작해야 할 수도 있다. (예로들면 과일 목록을 뽑는다거나 등등..) 그럴 때 '사과'를 '과일'로 캐스팅 해야 하는데, 과일이 상위 타입이므로 업캐스팅을 해야한다. 이럴 때 쓸 수 있는 것이 바로 super라는 것이다.

<br/>
<br/>

### 제네릭 타입에 대한 객체비교
---

```java
public class ClassName <E extends Comparable<? super E> { ... }
```

> `PriorityQueue(우선순위 큐), TreeSet, TreeMap` 같이 **값을 정렬하는 클래스**에서 사용
> 
>  **특정 제네릭에 대한 자기 참조 비교**를 하고싶을 경우 대부분 공통적으로 위와 같은 형식을 취함

<br/>

```java
public class SaltClass <E extends Comparable<E>> { ... }	// Error가능성 있음
public class SaltClass <E extends Comparable<? super E> { ... }	// 안전성이 높음
 
public class Person {...}
 
public class Student extends Person implements Comparable<Person> {
	@Override
	public int compareTo(Person o) { ... };
}
 
public class Main {
	public static void main(String[] args) {
		SaltClass<Student> a = new SaltClass<Student>();
	}
}
```

> Person을 상속받고 Comparable 구현부인 comparTo에서 Person 타입으로 업캐스팅(Up-Casting) 한다면 어떻게 될까?
>> 만약 `<E extends Comparable<E>`>라면 `SaltClass<Student> a` 객체가 타입 파라미터로 Student를 주지만, Comparable에서는 그보다 상위 타입인 Person으로 비교하기 때문에 `Comparable<E>`의 E인 Student보다 상위 타입 객체이기 때문에 제대로 정렬이 안되거나 에러가 날 수 있다.
>>> 그렇기 때문에 E 객체의 상위 타입, 즉 <? super E> 을 해줌으로써 위와같은 불상사를 방지할 수가 있는 것이다.
>>>> `E 자기 자신 및 조상 타입과 비교할 수 있는 E`

<br/>
<br/>

### `<?>` 와일드카드
---

*`와일드 카드 <?> = <? extends Object>`*

데이터가 아닌 '기능'의 사용에만 관심이 있는 경우 사용.