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


