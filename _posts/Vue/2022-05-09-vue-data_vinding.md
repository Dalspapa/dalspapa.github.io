## 데이터 바인딩이란?

두 데이터 혹은 정보의 소스를 일치시키는 기법으로, 화면에 보이는 데이터와 브라우저 메모리에 있는 데이터(여러개의 자바스크립트 객체)를 일치시키는 것을 말한다.  
예를 들어, MVC 모델에서 model과 view를 서로 묶어 model과 view의 "자동 동기화" 시키기 라고 이해할 수 있다.

### 양방향 데이터 바인딩

-   장점 : 코드의 사용면에서 코드량을 크게 줄여줌
-   단점 : 변화에 따라 DOM 객체 전체를 렌더링해주거나 데이터를 바꿔주므로, 성능이 감소되는 경우가 있음

`컨트롤러`에서  `model`이 변경됨 ->  `view`변경됨  
`view`에서  `scope model`이 변경됨 ->  `컨트롤러`에서  `model`이 변경됨

-   이렇게  `컨트롤러`와  `뷰`  양쪽의 데이터 일치가 모두 가능한 것이 양방향 데이터 바인딩이다. 데이터의 변화를 감지해 템플릿과 결합해 화면을 갱신, 화면의 입력에 따라 데이터를 갱신하는 것이다. (HTML -> JS, JS -> HTML 양쪽 모두 가능)
-   양방향 데이터 바인딩은 데이터의 변경을 프레임워크에서 감지하고 있다가, 데이터가 변경되는 시점에 DOM 객체에 렌더링을 해주거나 페이지 내에서 모델의 변경을 감지해 JS 실행부에서 변경한다. 입력된 값이나 변경된 값에 따라 내용이 바로 바뀌기 때문에 따로 체크해주지 않아도 된다.
-   양방향 데이터 바인딩은 웹 애플리케이션의 복잡도가 증가하면 증가할수록 빛을 발한다. 수많은 코드의 양을 줄여줄 뿐만 아니라 유지보수나 코드를 관리하기 매우 쉽게 해주기 때문이다.

예를 들어 vue.js 에서는

-   V-model과 V-on을 통해 양방향 데이터 바인딩을 한다.
-   v-model이 DOM 연관된 내용을 잡아내고, vue가 바라보는 대상의 속성과 연결됨.
-   v-on은 이벤트를 잡아내는 데 사용한다.
-  **v-model**은 **Vue.js** 에서 **양방향 바인딩**을 제공한다. keyup 이벤트와 이벤트 함수 없이 바로 사용자가 입력한 값을 화면에 반영할 수 있다.

### 단방향 데이터 바인딩

-   장점 : 데이터 변화에 따른 성능 저하 없이 DOM 객체 갱신 가능,  
    데이터 흐름이 단방향(부모->하위 컴포넌트)이라, 코드를 이해하기 쉽고 데이터 추적과 디버깅이 쉬움
-   단점: 변화를 감지하고 화면을 업데이트 하는 코드를 매번 작성해야 함

-   대표적으로  `React`가 단방향 데이터 바인딩을 한다.
-   단방향 데이터 바인딩은 데이터와 템플릿을 결합해 화면을 생성하는 것이다. (JS -> HTML만 가능)
-   사용자의 입력에 따라 데이터를 갱신하고 화면을 업데이트 해야 하므로 단방향 데이터 바인딩으로 구성하면, 데이터의 변화를 감지하고 화면을 업데이트 하는 코드를 매번 작성해주어야 한다.
-   리액트는 자바스크립트 기반으로, 부모 뷰 -> 자식 뷰 바뀐 내용을 직접 전달한다.
-   Vue.js에서 단방향 바인딩 대표적인 지시어
	- v-on(@) : UI에서 데이터 모델(viewModel)을 업데이트 하거나 출력할 때 사용.
	- v-bind(:) : 데이터 모델(viewModel)에서 업데이트 된 상태를 UI에 반영.
	- {{ }} 머스태쉬 태그 

### 데이터 바인딩 - 변화 감지

사실 모델이 변화할 가능성이 있는 경우는 그다지 많지 않다.  
아래와 같은 비동기 처리가 수행될 때 컴포넌트 클래스의 데이터가 변경될 수 있다. 변화 감지는 모델이 변화할 수 있는 이러한 상황들을 감시한다.

-   DOM 이벤트(click, key press, mouse move 등)
-   Timer 함수(setTimeout, setInterval)의 tick 이벤트
-   Ajax 통신 / Promise