# 뷰의 템플릿 문법
_뷰로 화면을 조작하기 위해 제공되는 문법. 크게 **데이터 바인딩**과 **디렉티브**로 나뉜다._

<br/>

## Data Binding
_콧수염 문법인 “{{ }}”를 활용하여 인스턴스의 data, computed, props 속성을 연결할 수 있다. 그리고 간단한 자바스크립트 표현식도 화면에 표시할 수 있다._

```html
<div>{{ str }}</div>
<div>{{ number + 1 }}</div>
<div>{{ message.split('').reverse().join('') }}</div>
```

```js
    <div id="app">

        <p v-bind:id="uuid" v-bind:class="name">{{ num }}</p> 

        <!-- 단지 화면에서 표현되는 텍스트값 뿐만 아니라, 전체적인 돔에 대한 정보들까지 리엑티비티하게 바로바로 다시 반영해서 그 돔을 변경해 줌. -->
		<!-- 예전에는 돔을 쿼리셀렉터 같은 것으로 일일히 다 쫓아가서 그 안의 내용들을 바꿔주는 코드를 넣었어야 했음.  -->

        <!-- 실질적으로 아래코드처럼 표현됨. -->

        <!-- <p id="abc1234">{{ num }}</p> -->

        <p>{{ doubleNum }}</p>

        <div v-if="loading">

            Loading...

        </div>

        <div v-else>

            test user has been logged in

        </div>

        <div v-show="loading">

            Loading...

        </div>

        <!-- show는 style="display: none;" 으로 육안상에서만 보이지 않게 해줌. if는 false일때 dom을 삭제함. -->

        <input type="text" v-model="message">

        <p>{{ message }}</p>

        <!-- v-model 이용해 사용자 입력 값을 바로 노출 시킬 수 있음. -->

    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>

        new Vue({

            el: '#app',

            data: {

                num: 10,

                uuid: 'abc1234',

                name: 'text-blue',

                loading: true,

                message: ''

            },

            computed: { //컴피티드 속성(계산된 속성). 루트 데이터의 값 제어 가능.

                doubleNum: function() {

                    return this.num * 2;

                }

            }

        })

    </script>
```

<br/>

## Directive
HTML 태그의 속성에 `v-` 접두사가 붙은 특별한 속성으로 화면의 DOM 조작을 쉽게할 수 있는 문법들을 제공한다.

```html
<!-- seen의 진위 값에 따라 p 태그가 화면에 표시 또는 미표시 -->
<p v-if="seen">Now you see me</p>
<!-- 화면에 a 태그를 표시하는 시점에 뷰 인스턴스의 url 값을 href에 대입 -->
<a v-bind:href="url"></a>
<!-- 버튼에 클릭 이벤트가 발생했을 때 doSomething이라는 메서드를 실행 -->
<button v-on:click="doSomething"></button>
```

### methods  /  v-on 

```js
    <div id="app">

        <button v-on:click="logText">click me</button>

        <input type="text" v-on:keyup.enter="logText"> <!-- .enter : 이벤트 모디파이어 엔터 쳐야 실행 됨. -->

        <button>add</button>

    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <script>

        new Vue({

            el: '#app',

            methods: { //일반적으로 비즈니스 로직을 다루거나 이벤트를 처리하고 화면을 조작하는 로직들은 여러개.

                logText: function() {

                    console.log('clicked');

                }

            }

        })

    </script>
```
<br/>

### whatch

```js
  <div id="app">

    {{ num }}

    <button v-on:click="addNum">increase</button>

  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

  <script>

    new Vue({

      el: '#app',

      data: {

        num: 10

      },

      watch: { // 데이터의 변화에 따라 특정 로직을 수행할 수 있음.

        num: function() {

          this.logText();

        }

      },

      methods: {

        addNum: function() {

          this.num = this.num + 1;

        },

        logText: function() {

          console.log('changed');

        }

      }

    })

  </script>
```

<br/>

> **❕ TIP**
>  서비스를 구현하기 위해 필요한 모든 속성과 기능들은 뷰에서 제공하고 있다고 인식. 
>  vuejs.org 의 검색 기능 적극 활용. / Learn 탭에서 Guide, API 항목 확인.
>  vue는 문서화가 잘 되어 있음. 서비스 구현시 시간이 부족하기 때문에 문서화가 잘 된 라이브러리를 선택하는 것이 중요함.
<br/>

> **📌vscode단축키**
> Ctrl + L : 한 줄 선택
> Shift + Alt + ↓ : 해당 줄 아래로 복사
> Ctrl + Enter : 커서 어디에 있든지 다음줄로 엔터.
> log + Enter : console.log 코드 자동완성.
> Ctrl + Shift + ` : 터미널 열기

<br/>
<br/>

## watch 속성 VS computed 속성
_watch보다는 computed가 대부분의 케이스에 적합. (공식문서)_ 
- computed가 캐싱이나 내부적 튜닝이 더 많이 되어있음.
- 간단한 텍스트 연산 시 computed 추천.
- 뷰의 validation 라이브러리 내부적으로 computed로 구현되어 있음. 
- watch는 코드가 지저분해짐.
- watch는 매번 실행되기 부담스러운 무거운 로직에 사용. 특히 데이터요청에 적합.
<br/>

```js
  <div id="app">

    {{ num }}

  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

  <script>

    new Vue({

      el: '#app',

      data: {

        num: 10

      },

      computed: { // 단순한 값에 대한 계산. validation 라이브러리 내부적으로 computed로 구현되어 있음. 간단한 텍스트 연산.

        doubleNum: function() {

          return this.num * 2;

        }

      },

      watch: { // 매번 실행되기 부담스러운 무거운 로직에 사용. 특히 데이터요청에 적합.

        num: function(newValue, oldValue) {

          this.fetchUserByNumber(newValue);

        }

      },

      methods: {

        fetchUserByNumber: function(num) {

          // console.log(num);

          axios.get(num);

        }

      }

    });

  </script>
```
<br/>

## computed 속성을 이용한 클래스 코드 작성

```js
  <style>

 .warning {

 color: red;

  }

  </style>

</head>

<body>

  <div id="app">

    <!-- <p v-bind:class="{ warning: isError }">Hello</p> -->

    <!-- 템플릿 표현식으로 계산 x 스크립트 단으로 내려서 사용. -->

    <p v-bind:class="errorTextColor">Hello</p>

  </div>

  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

  <script>

    new Vue({

      el: '#app',

      data: {

        // cname: 'blue-text',

        isError: false

      },

      computed: {

        errorTextColor: function() {

          // if (isError) {

          //   return 'warning'

          // } else {

          //   return null;

          // }

          return this.isError ? 'warning' : null;

          // 컴피티드 데이터 속성 접근 시 this 부착.

        }

      }

    });

  </script>

</body>
```
<br/>

## Vue CLI
### 설치방법
> https://cli.vuejs.org/  -> Installation 탭에서 
>```
>npm install -g @vue/cli
>```
>VSCode 터미널 이용해 설치.

```
node -v
npm -v
```
버전 확인 후 명령어 이용해 설치. 

파일 권한이 없어서 설치 불가능 할 경우 앞에 sudo 부착.
```
sudo npm install -g @vue/cli
```

### Where does npm install packages?
On Unix systems they are normally placed in  `/usr/local/lib/node`  or  `/usr/local/lib/node_modules`  when installed globally. If you set the  `NODE_PATH`  environment variable to this path, the modules can be found by node.

Windows XP -  `%USERPROFILE%\AppData\npm\node_modules`  
Windows 7, 8 and 10 -  `%USERPROFILE%\AppData\Roaming\npm\node_modules`

<br/>

### Vue CLI 버전별 차이점
**[Vue CLI 2.x]**
- vue init '프로젝트 템플릿 유형' '프로젝트 폴더 위치'
- vue init webpack-simple '프로젝트 폴더 위치'

**[Vue CLI 3.x]**
- `vue create '프로젝트 폴더 위치'` : 프로젝트 폴더 생성
- `vue.cmd create vue-cli`
	- 최신 버전의 뷰는 vue 명령어를 사용하지 않고 vue.cmd 명령어를 사용한다.
- `Default ( [Vue 2] babel, eslint)` 선택.
- `cd vue-cli` : vue-cli 폴더로 이동.
- `npm run serve` : 서버 실행.