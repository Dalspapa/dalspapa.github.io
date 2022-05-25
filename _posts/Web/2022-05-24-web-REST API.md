# 🔎 REST API란?

*Representational Transfer의 약어.*

**Restful** : 자원을 표현(http를 통해 자원들을 식별)할 때, uri를 crud규칙에 맞게 구현하는 것.

<br/> 

## 🤷‍♂️ 왜 쓰게 되었는가?
---

- 웹사이트를 만들 때 웹에서만 돌아가게 만들면 사용성이 제한 됨.

- 웹을 사용하는 디바이스(클라이언트)가 다양해짐에 따라 그 요구에 맞게 **백엔드 로직을 하나로 통합**하여 모든 클라이언트 단에 붙이기 위해 고안 됨.

- REST라는 개념을 통해 REST API로 백엔드를 구축하게 되면 다양한 클라이언트와의 통신이 가능.

<br/>

## 기존 http URI 구성
---

- GET : 백엔드에서 Data를 가져올 때 
  - ex.) 게시판목록, 특정 게시글내용, 회원정보 등
- POST : 말그대로 POST한다, 등록할 때 사용
  - ex.) 회원정보를 DB에 insert,update,delete 
 
<br/>

## 😎 REST-ful한 URI
---

- **GET** ▶ select 조회
- **POST** ▶ Insert 입력
- **PUT&PATCH** ▶ Update 수정
- **DELETE** ▶ Delete 삭제

> http method방식을 다양화하여 처리하게되면 같은 uri로 다른 행동을 하게 만들수 있게 됨.

``` 
GET /movies ▶ 영화의 전체 목록들을 조회
GET /movies/:id ▶ 특정 영화만을 조회
POST /movies ▶ 신규 영화를 등록
PUT /movies ▶ 목록에 등록된 영화를 수정
DELETE /movies ▶ 목록으로부터 삭제
```

*같은 uri를 사용하되 전달 방식에 따라 다른처리를 할수있도록 만듭니다.*

<br/>

> URI (Uniform Resource Identifier)
> 
> ▶ 서버의 자원을 식별할수 있는 유일한 식별자

<br/>
<br/>

## REST API의 구체적인 개념
---

▶ *HTTP uri로 자원을 명시하며, HTTP의 메서드를 활용하여 해당 자원에 대한 CRUD처리 적용*

<br/>

### REST API의 CRUD method 처리방식
---

```
Create ▶ POST
Read ▶ GET
Update ▶ PUT
Delete ▶ DELETE
```

<br/>

### 🍺 REST API의 장점과 단점
---

장점

- Http 프로토콜이 제공하는 uri나 요청방식 사용을 그대로 사용하므로 별도의 인프라를 구축할 필요가 없습니다.
- Http 프로토콜의 장점을 가져갈 수 있으며, http프로토콜을 사용하는 모든 플랫폼에서 사용이 가능합니다.
- 서버와 클라이언트 역할을 명확하게 분리하면서, 백앤드 서버는 데이터를 관리만을, 프론트엔드 클라이언트는 자원들을 표현 합니다. 이러한 REST방식 때문에 통신처리를 프론트엔드에서 하기때문에 백엔드는 데이터베이스 관리만 하게되어 확실히 백엔드 파트가 많이 줄게되었습니다.
- 백엔드가 분리가되어 공통적으로 처리되도록 되어있어 모바일,웹,pc 등 디자인에서 생길수 있는 문제를 최소화 시켜줍니다.


단점

- 명확한 표준이 존재하지 않습니다.
- 구형 브라라우저 에서의 사용에 제약이 발생합니다.
스프링에서는 구형에서도 사용할수 있도록 하는 처리방식이 있습니다.

<br/>
 
### Rest API가 필요한 이유
---

- 애플리케이션을 백엔드서버와 프론트앤드서버로 분리해서 여러 다양한 클라이언트에 적용될수 있게 만듭니다.
- Android, Ios, 크롬, 사파리 등 다양한 클라이언트가 등장하고 있습니다.
- 이러한 다양한 클라이언트에서 통신을 할수있도록 표준화된 규격이 필요하며 이러한 규격은 Rest api가 됩니다.
스프링 4부터 Rest api를 구축할 수 있도록 아주 편리한 어노테이션과 메서드들을 제공하고 있습니다.

**Restful 하다**
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드것을 의미합니다.

**Restful 하지 못하다**
- CRUD 기능을 모두 POST로만 처리하는 API를 말합니다.

> ❗  보안 관련해서는 취약점 항목으로 작용할 수 있다.
> 
> > uri 에서 특정 동작을 넣어두면 안됨. (DB  로직을 uri에 내비치면 안됨)

<br/>
<br/>

## 👌 정리
--- 

REST는 ‘Representational State Transfer'의 약어로 하나의 URI는 하나의 고유한 리소스를 대표하도록 설계된다는 개념이다.   

최근에는 서버에 접근하는 기기의 종류가 다양해 지면서 다양한 기기에서 공통으로 데이터를 처리할 수 있는 규칙을 만들려고 하는데 이러한 시도가 REST 방식이다.

<br/>

REST API는 외부에서 위와 같은 방식으로 특정 URI를 통해서 사용자가 원하는 정보를 제공하는 방식이다.
 
최근에는 오픈 API에서 많이 사용되면서 REST방식으로 제공 되는 외부 연결 URI를 REST API라고 하고, REST 방식의 서비스 제공이 가능한 것을 ‘Restful' 하다고 표현한다.

<br/>

스프링 3.0버전부터 @ResponseBody애노테이션을 지원하면서 본격적으로 REST방식의 처리를 지원하였고, 4.0부터는 @RestController가 본격적으로 소개되었다. 

스프링 4.0버전부터 지원되는 ‘@RestController'애노테이션의 경우 기존의 특정한 JSP REST 와 같은 뷰를 만들어 내는 것이 목적이 아닌 방식의 데이터 처리를 위해서 사용하는 애노테이션이다.
 
스프링 3.0버전까지는 컨트롤러는 주로 @Controller애노테이션만을 사용하였고, 화면 처리는 jsp가 아닌 데이터 자체를 서비스 하려면 해당 메서드나 리턴타입이  ‘@ResponseBody' 애노테이션을 추가하는 것으로 작성되었다.

기능적인 면에서는 크게 이전 3.0버전과 달라진 점은 없지만, 컨트롤러 자체의 용도를 지정한다는 점에서 변화가 있다고 볼수 있다.
 
<br/>
<br/>
<br/>

# JSON ( Java Script Object Notation) 
### *자바스크립트 객체 표기법*
 
<br/>

## JSON 형태의 데이터란?
---

### 백엔드

스프링으로 구축된 was서버, Oracle DB서버가 있다.

<br/> 

### 프론트엔드

클라이언트 (Web Browser - chrome)를 통해서 was서버와 통신을 한다.

Http프로토콜을 사용하여 request,response를 통해 백엔드의 was와 통신.

<br/>

> REST API에서는 백엔드를 웹 전용만의 프로그램을 만들지 않습니다.

<br/>
<br/>

## 🌏 클라이언트 해독 및 통신 서버
---

| 클라이언트 | ↔ ||서버||
|:---------:|:--:|--|:--:|--|
| WebBrowser (HTML,css,javsscript) | 
| Android Phone (JAVA,Kotlin,groovy) |JSON | JAVA | (↔) <br/>jdbc | SQL |
| I Phone (Swift,Objective C) |


다양한 방식의 클라이언트가 하나의 서버와 통신이 가능해 지기 위해서는 여러 언어의 동일한 규격, 언어적 표준을 맞춰야 한다는 것입니다.

이러한 언어적 표준을 맞춘것이 바로 JSON 형태의 데이터입니다.

기존에는 언어적 표준으로 "문자열".xml 이라는 형식으로 통신을 했는데 이러한 형식으로는 가독성,표현성 등 단점들이 많았기 때문에 최근에는 JSON이라는 표기법이 대체하고있습니다.

<br/>

JSON은 javaScript로 이루어진 데이터가 아니라 자바스크립트 객체를 표기해주는 데이터 형태입니다.

하필 왜 javaScript일까요? 가장 간단하기 때문입니다.

다양한 클라이언트의 각기 다른 언어들을 JSON 형태로 맞춰서 서버와 통신하게 됩니다.

서버에서는 JSON형태로 받은 데이터들을 스프링에 맞는 자바언어로 다시 번역하여 통신을 수행합니다.

클라이언트와 서버의 각각 서로 다른 데이터 언어들을 사용하여 서로 통신할때 중간에서 JSON형태의 하나의 언어로 바꾸어 통역 역할을 해줍니다.

<br/> 
<br/> 

### 📌 JSON형태 
---

**[ Array or LIST ]**

| 서버 언어 형태 Java |	통신 언어 JSON |
|--|--|
| Array or LIST | [ " " ,  " " ,  " " , " " ] |

<br/> 

**[ Object or Map ]**

| 서버 언어 형태 Java |	통신 언어 JSON |
|--|--|
| Object or Map | { <br/> &nbsp; &nbsp; "key1":"value1", <br/> &nbsp; &nbsp; "key2":"value2" <br/> } |

```java
class User {
    String name = "홍길동";
    int age = "20";
}
```

```js
{
    "name":"홍길동",
    "age":"20"
}
```
 
<br/>

***객체형태를 담고있는 List***

**[ `List<generic>` ]**

| 서버 언어 형태 Java |	통신 언어 JSON |
|--|--|
| `List<generic>`	| [ <br/> &nbsp; &nbsp; {"key1-1":"value1-1" , "key1-2":"value1-2"} , <br/> &nbsp; &nbsp; {"key2-1":"value2-1" , "key2-2":"value2-2"} , <br/> &nbsp; &nbsp; {"key3-1":"value3-1" , "key3-2":"value3-2"} <br/> ]

```js
[
  {"name":"강감찬" , "age":"15"} , 
  {"name":"홍길동" , "age":"20"} , 
  {"name":"대조영" , "age":"30"}
]
```

> 객체의 필드가 key가 되고 필드의 저장된 값이 키에 매칭되는 value가 되며 마찬가지로 Map에서도 Key,value를 각각 같은 방식으로 표현해 준다.

<br/>

> 클라이언트의 언어가 만약 자바라면 서버로 통신을할때 위와 같이 jSON형태로 바꿔서 보내게 된다.
> 
> 서버에서는 이런 JSON형태의 데이터를 다시 서버의 언어로 바꾼 후 DB와 통신

<br/>

REST API구축은 기본이며 REST API를 프론트엔드 쪽으로 쐈을 때, javascript로 적재적소를 뽑아내어 html에 꽂아넣는것 즉, 값을 ${EL}로 받지 않고 JSON형태의 데이터로 만든다음 javascript를 통해 꽂아 넣는 것.

<br/>

> **@RestController**를 사용하면 @ResponseBody어노테이션을 생략할 수 있게된다.
> 
> > F3을누르면 @Controller @ResponseBody를 상속받는다고 지정되있다.