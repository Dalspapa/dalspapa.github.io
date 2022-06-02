# Async & Await를 이용한 비동기 처리

*async와 await는 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법입니다. 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와줍니다.*

<br/>

## 🍕 자바스크립트 비동기 처리 패턴의 발전 과정
---

<br/>

### 🍺기존 JS 비동기 처리

```js
$.get('domain.com/id', function(id) {
  if (id === 'john') {
    $.get('domain.com/products', function(products) {
      console.log(products);
    });
  }
});
```

<br/>

### 🍺 Promise 이용 비동기 처리

```js
function getId() {
  return new Promise(function(resolve, reject) {
    $.get('domain.com/id', function(id) {
      resolve(id);
    })
  })
}

getId()
  .then(function(id) {
    if (id === 'john') {
      $.get('domain.com/products', function(products) {
        return new Promise(...)
      });
    }
  })
  .then(function(products) {
        console.log(products);
  })
  .catch();
```
 
<br/>

### 🍺 더 명시적인 Promise 처리

```js
function getId() {
  return new Promise(function(resolve, reject) {
    $.get('domain.com/id', function(id) {
      resolve(id);
    })
  })
}

function getProduct(id) {
  // ...
}

function logProduct() {
  // ...
}

getId()
  .then(getProduct)
  .then(logProduct)
  .catch();
```

<br/>

### 🍺 async & await 방식의 비동기 처리

```js
var id = $.get('domain.com/id');
if (id === 'john') {
  var products = $.get('domain.com/products');
}
console.log(products);
```

<br/>
<br/>
<br/>

## 🍕 async & await 기본 문법
---

```js
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

> 함수의 앞에 `async` 라는 예약어를 붙인다. 그리고 나서 함수의 내부 로직 중 HTTP 통신을 하는 비동기 처리 코드 앞에 `await`를 붙인다. 
> > 주의해야 할 점 : 비동기 처리 메서드가 꼭 **프로미스 객체를 반환**해야 `await`가 의도한 대로 동작한다.
> >
> >  일반적으로 `await`의 대상이 되는 비동기 처리 코드는 Axios 등 프로미스를 반환하는 API 호출 함수입니다.

<br/>

### 🍺 간단한 예제
```js
function fetchItems() {
  return new Promise(function(resolve, reject) {
    var items = [1,2,3];
    resolve(items) // 프로미스 객체 반환
  });
}

async function logItems() {
  var resultItems = await fetchItems();
  console.log(resultItems); // [1,2,3]
}
```

<br/>
<br/>

## 🍕 기존 방식과의 비교 코드
---

<br/>

### 🍺  프로미스 기반 로그인 비동기처리

```js
loginUser() {
  axios.get('https://jsonplaceholder.typicode.com/users/1')
    .then(response => {
      if (response.data.id === 1) {
        console.log('사용자가 인증되었습니다.');
        axios.get('https://jsonplaceholder.typicode.com/todos')
          .then(response => {
            this.items = response.data;
          });
      }
    })
    .catch(error => console.log(error));
}
```

<br/>

### 🍺 async $ await 적용

```js
async loginUser1() {
  var resonse = await axios.get('https://jsonplaceholder.typicode.com/users/1');
  if (response.data.id === 1) {
    console.log('사용자가 인증되었습니다.');
    var list = await axios.get('https://jsonplaceholder.typicode.com/todos');
    this.items = list.data;
  }
}
```

<br/>
<br/>

## 🍕 async await 에러처리 방법
---

```js
import { handleException } from './utils/handler.js';
```

```js
async loginUser1() {
  try {
    var resonse = await axios.get('https://jsonplaceholder.typicode.com/users/1');
    if (response.data.id === 1) {
      console.log('사용자가 인증되었습니다.');
      var list = await axios.get('https://jsonplaceholder.typicode.com/todos');
      this.items = list.data;
    }
  } catch (error) {
    handleException(error); // 공통된 에러처리 가능. 
    console.log(error);
  }
}
``` 

> then / catch 는 비동기 처리만 예외처리 함.
> 
> JS의 전통적 예외처리인 try / catch는 전반적인 JS 코드에 예외처리 가능.

<br/>
<br/>
<br/>

# ⌨ async 함수 이용한 코드 리펙토링

<br/>

## 🍺 promise -> async
---

```js
// promise
FETCH_NEWS(context) {
    return fetchNewsList()
        .then(response => {
            context.commit('SET_NEWS', response.data);
        })
        .catch(error => {
            console.log(error);
        });
},
```

```js
// async
async FETCH_NEWS(context) { // async 함수는 무조건 promise를 리턴
  const response = await fetchNewsList();
  context.commit('SET_NEWS', response.data);
  return response;
},
```

<br/>

## 🍺 적용하기
---

### `actions.js`
```js
import {
  fetchNewsList,
  fetchAskList,
  fetchJobsList,
  fetchList,
  fetchUserInfo,
  fetchCommentItem,
} from '../api/index.js';

export default {
  // promise
  // FETCH_NEWS(context) {
  //     return fetchNewsList()
  //         .then(response => {
  //             context.commit('SET_NEWS', response.data);
  //         })
  //         .catch(error => {
  //             console.log(error);
  //         });
  // },

  // async
  async FETCH_NEWS(context) { // async 함수는 무조건 promise를 리턴
    const response = await fetchNewsList();
    context.commit('SET_NEWS', response.data);
    return response;
  },

  // promise
  // FETCH_JOBS({ commit }) {
  //     return fetchJobsList()
  //         .then(({ data }) => {
  //             commit('SET_JOBS', data);
  //         })
  //         .catch(error => {
  //             console.log(error);
  //         });
  // },

  // async
  async FETCH_JOBS({ commit }) {
    try {
      const response = await fetchJobsList();
      commit('SET_JOBS', response.data);
      return response;
    } catch (error) {
      console.log(error);
    }
  },

  // promise
  // FETCH_ASK({ commit }) { 
  //     return fetchAskList()
  //         .then(({ data }) => { 
  //             commit('SET_ASK', data); 
  //         })
  //         .catch(error => {
  //             console.log(error);
  //         });
  // },

  // async
  async FETCH_ASK({ commit }) {
    const response = await fetchAskList();
    commit('SET_ASK', response.data);
    return response;
  }, // api단 에서 예외처리


  FETCH_USER({ commit }, username) {
    return fetchUserInfo(username)
      .then(({ data }) => {
        commit('SET_USER', data);
      })
      .catch(error => {
        console.log(error);
      });
  },
  FETCH_ITEM({ commit }, itemid) {
    return fetchCommentItem(itemid)
      .then(({ data }) => {
        commit('SET_ITEM', data);
      })
      .catch(error => {
        console.log(error);
      });
  },

  // #2
  async FETCH_LIST({ commit }, pageName) {
    // #3
    const response = await fetchList(pageName);
    // #4
    console.log(4);
    commit('SET_LIST', response.data)
    return response;
  },
}
```

<br/>

`/api/index.js`
```js
import axios from 'axios';

// 1. HTTP Request & Response와 관련된 기본 설정
const config = {
  baseUrl: 'https://api.hnpwa.com/v0/'
};

// 2. API 함수들을 정리
function fetchNewsList() {
  // return axios.get('https://api.hnpwa.com/v0/news/1.json');
  return axios.get(`${config.baseUrl}news/1.json`);
}

// api에서 예외처리
async function fetchAskList() {
  try {
    // return axios.get(`${config.baseUrl}ask/1.json`);
    // 아래 코드처럼 await 처리 가능
    const response = await axios.get(`${config.baseUrl}ask/1.json`);
    return response;
  } catch (error) {
    console.log(error);
  }
}

function fetchJobsList() {
  return axios.get(`${config.baseUrl}jobs/1.json`);
}

async function fetchList(pageName) {
  try {
    return await axios.get(`${config.baseUrl}${pageName}/1.json`);
  } catch (error) {
    console.log(error);
  }
}

function fetchUserInfo(username) {
  return axios.get(`${config.baseUrl}user/${username}.json`);
}

function fetchCommentItem(itemid) {
  return axios.get(`${config.baseUrl}item/${itemid}.json`);
}

export {
  fetchNewsList,
  fetchAskList,
  fetchJobsList,
  fetchList,
  fetchUserInfo,
  fetchCommentItem,
}
```