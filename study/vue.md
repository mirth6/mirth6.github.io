vue



##### vue 인스턴스 생성

```javascript
new Vue({
  // instance option properties
  template: "",
  el: "",
  methods: {}
  // ...
});
```

인스턴스 옵션 : *data, template, el, methods, life cycle hook* 



##### 인스턴스 라이프 사이클

초기화 작업

- 데이터 관찰
- 템플릿 컴파일
- 돔에 객체 연결
- 데이터 변경시 돔 업데이트

```javascript
new Vue({
  data: {
    a: 1
  },
  created: function() {
    // this 는 vm 을 가리킴
    console.log("a is: " + this.a);
  }
});
```

라이프사이클: created, mounted, updated, destroyed



##### 컴포넌트 등록

```html
<div id="app">
  <my-component></my-component>
</div>


new Vue({
  el: "#app",
  // 컴포넌트 등록 코드
  components: {
    // '컴포넌트 이름': 컴포넌트 내용
    "my-component": {
      template: "<div>A custom component!</div>"
    }
  }
});
```

global component등록

```js
Vue.component('my-component', {
  // 컴포넌트 내용
  template: '',
  ...
})
```

local component등록

```js
var cmp = {
  // 컴포넌트 내용
  template: '',
  ...
}

new Vue({
  components: {
    'my-cmp' : cmp
  }
})
```



##### 부모자식 컴포넌트

컴포넌트 통신

- 부모->자식 : pass props

- 자식-> 부모: emit events

##### props

```html
<!-- 상위 컴포넌트 -->
<div id="app">
  <!-- 하위 컴포넌트에 상위 컴포넌트가 갖고 있는 message를 전달함 -->
  <child-component v-bind:propsdata="message"></child-component>
</div>
```

```js
// 하위 컴포넌트
Vue.component("child-component", {
  // 상위 컴포넌트의 data 속성인 message를 propsdata라는 속성으로 넘겨받음
  props: ["propsdata"],
  template: '<p>{{ propsdata }}</p>'
});

// 상위 컴포넌트
var app = new Vue({
  el: "#app",
  data: {
    message: "Hello Vue! from Parent Component"
  }
});
```

**주의할 점: props 변수 명을 카멜 기법(aBow)으로 정의하면 html 태그에서 사용할 때는 케밥 기법(`-`)으로 선언해야 한다. 아래는 만약 프롭스 속성 명을 카멜 기법인 passedData로 선언했을 때의 주의 메시지**



##### event bus

```js
// 화면 개발을 위한 인스턴스와 다른 별도의 인스턴스를 생성하여 활용
var eventBus = new Vue();

new Vue({
  // ...
});
```

###### 이벤트 발생시킬 컴포넌트

```js
eventBus.$emit("refresh", 10);
```

###### 이벤트 받을 컴포넌트

```js
// 이벤트 버스 이벤트는 일반적으로 라이프 사이클 함수에서 수신
new Vue({
  created: function() {
    eventBus.$on("refresh", function(data) {
      console.log(data); // 10
    });
  }
});
```

##### 만약, `eventBus`의 콜백 함수 안에서 해당 컴포넌트의 메서드를 참고하려면 `vm` 사용

```js
new Vue({
  methods: {
    callAnyMethod() {
      // ...
    }
  },
  created() {
    var vm = this;
    eventBus.$on("refresh", function(data) {
      console.log(this); // 여기서의 this는 이벤트 버스용 인스턴스를 가리킴
      vm.callAnyMethod(); // vm은 현재 인스턴스를 가리킴
    });
  }
});
```



##### 동일한 상위 컴포넌트를 가진 하위 컴포넌트들 간의 통신은 아래와 같이 해야 한다.

- Child(하위) -> Parent(상위) -> Children(하위 2개)

