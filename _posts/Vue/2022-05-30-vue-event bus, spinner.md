# 이벤트 버스를 이용한 스피너 컴포넌트 구현

- `ListItem.vue` 에서 처리하던 `created()`를 다시 각각의 View 컴포넌트에서 처리한다.

	```js
	created() {
    const name = this.$route.name; 
    let actionsName;
    if (name === 'news') {
      actionsName = 'FETCH_NEWS';
    } else if (name === 'ask') {
      actionsName = 'FETCH_ASK';
    } else if (name === 'jobs') {
      actionsName = 'FETCH_JOBS';
    }
    this.$store.dispatch(actionsName);
  },

	// 분기처리 된 dispatch를 해당 컴포넌트에 직접 코딩
	```
	
- `/components` 디렉토리에 `Spinner.vue` 생성한다.

- `/utils` 디렉토리 생성 후 `bus.js`를 생성한다.

- `actions.js` 에서 `response` 객체를 리턴시킨다.

	```js
  FETCH_NEWS(context) { 
		fetchNewsList()
			.then(response => {
				context.commit('SET_NEWS', response.data);
				return response; 
				// response 객체(프로미스) 컴포넌트로 넘기기
				// 데이터를 받아와서 꺼낸 다음 뮤테이션즈에 담아주고, 
				// 응답 데이터를 계속 화면으로 돌려 보냄.
			})
			.catch(error => {
				console.log(error);	
			});
	},
	```

- 각각의 컴포넌트에서 `actions.js` 에서 받은 프로미스객체를 체이닝 처리한다.

<br/>
<br/>
<br/>

## **`/components/Spinner.vue`**
---

```html
<template>
  <div class="lds-facebook" v-if="loading">
    <div>
    </div>
    <div>
    </div>
    <div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    loading: {
      type: Boolean,
      required: true,
    },
  },
}
</script>

<style>
.lds-facebook {
  display: inline-block;
  position: absolute;
  width: 64px;
  height: 64px;
  top: 47%;
  left: 47%;
}
.lds-facebook div {
  display: inline-block;
  position: absolute;
  left: 6px;
  width: 13px;
  background: #42b883;
  animation: lds-facebook 1.2s cubic-bezier(0, 0.5, 0.5, 1) infinite;
}
.lds-facebook div:nth-child(1) {
  left: 6px;
  animation-delay: -0.24s;
}
.lds-facebook div:nth-child(2) {
  left: 26px;
  animation-delay: -0.12s;
}
.lds-facebook div:nth-child(3) {
  left: 45px;
  animation-delay: 0;
}
@keyframes lds-facebook {
  0% {
    top: 6px;
    height: 51px;
  }
  50%, 100% {
    top: 19px;
    height: 26px;
  }
}
</style>
```

<br/>
<br/>

## **`/utils/bus.js`**
---

```js
import Vue from 'vue';

export default new Vue();


// Event Bus
// 빈 이벤트 객체를 하나 만들어서 그 이벤트 객체를 이용해
// 컴포넌트간에 데이터를 전달 하는 것 의미.

// new Vue(); 를 그대로 export
// export한 것을 받는 쪽에서
// bus라고 선언하면 인스턴스 객체가 들어감


// ex) 
// bus.js
// export default new Vue();

// App.vue
// import bus(자유롭게선언가능) from './utils/bus.js';


// bus.js
// export const bus = new Vue();

// App.vue
// import { bus } from './utils/bus.js';
```

<br/>
<br/>

## **`NewsView.vue`**
---

```html
<template>
  <div>
    <list-item></list-item>
  </div>
</template>

<script>
import ListItem from '../components/ListItem.vue';
import bus from '../utils/bus.js';

export default {
  components: {
      ListItem,
  },
  created() {
    bus.$emit('start:spinner');
    
    // 처음 created 되자마자 스피너 실행하고, 
    // 데이터를 다 불러오면, end:spinner 실행

    setTimeout(() => { // 스피너 테스트 위해 3초 후 데이터 로드

      this.$store.dispatch('FETCH_NEWS')
      //actions에서 받은 프로미스객체 체이닝 가능
      .then(() => {
        console.log('fetched');
        bus.$emit('end:spinner');
      })
      .catch((error) => {
        console.log(error);
      });

    }, 3000);
    
  },
}
</script>
```