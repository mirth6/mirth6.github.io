# React

[TOC]

라이브러리

서드파티 라이브러리 - 라우터

양방향 바인딩 (뷰변화 모델변화, 모델변화 뷰변화)



virtual DOM





webpack : 빌드했을때 확장자 별로 묶어줌

babel : 





JSX : html형식으로 

- 여러개 태그가 생기면 한 큰 테그안에 넣어줘야함

- {}

- 삼항연산자

  ```
  {value === 1 }
  ```

  

- css 

  - className=App
  - style={}

- 주석처리

  ```jsx
  {/*주석쓰기*/}
  <h1 //이렇게 주석도 가능>
  ```

  

- ㅇ



###### App.js

```react
import React, {Component} from 'react';

class App extends Component{
    render(){
        return(
            <div></div>
        )
    }
}

export default App
```



### Props

- 부모컴포넌트가 자식 컴포넌트에 전달

  ```
  <Child value="value">
  ```



###### Parent.js

```react
class Parent extends Component{
    
    static defaultProps = { name: '철수'}
    render(){
        return(
            <Child name="돌쇠">
        )
    }
}
```

###### Child.js

```react
class Child extends Component{
    render(){
        return(
            <div>
                안녕 내 이름은 {this.props.name}이야
            </div>
        )
    }
}
```



##### 함수형 컴포넌트

- 딱히 기능없이 props 만 받아와서 보여주기만 하는 경우 주로 사용

```react
import React from 'react';

const Child = ({name}) =>{
    return <div>안녕 내 이름은 {name}이야 </div>;
};

Child.defaultProps = {
    name: '철수'
};

export default Child
```



### state

- 컴포넌트 내부에 있음
- setState()를 통해 변경 해야함 -> 직접하면 rerender안됨

###### Counter.js

```react
import React, {Component} from 'react';

class Counter extends Component{
    //state는 객체여야함
    state = { 
		number: 0         
    }

	//화살표 함수로 해야 this가 뭔지 알아
	handleIncrease = () =>{ 
        this.setState({
            number : this.state.number + 1
        })
    }
    
    //화살표 함수로 안하는 경우
    constructor(props){
        super(props);
        this.handleDecrease = this.handleDecrease.bind(this);
    }
    handleDecrease(){
         this.setState({
            number : this.state.number - 1
        })       
    }

	//render
    render(){
        return(
            <div>
            	<h1>카운터</h1>
                <div>값: {this.state.number}</div>
            	<button onClick = {this.handleIncrease}> + </button>
            	<button onClick = {this.handleDecrease}> - </button>
            </div>
        )
    }
}

export default Counter
```





### LifeCycle api

![lifeCycle](https://pbs.twimg.com/media/DZ-97vzW4AAbcZj?format=jpg&name=large)



#### Mounting

- 컴포넌트가 브라우저 상에 나타남

##### constructor

##### getDerivedStateFromProps

##### render

##### componenetDidMount

- 외부 라이브러리



#### Updating

- props나 state가 바뀜

##### shouldComponentUpdate

##### getSnapshotBeforeUpdate

- 렌더링 결과물이
- 스크롤위치 해당 돔 크기 가져올때

##### componenetDidUpdate

- 업데이트 되었을때 호출
- 이전 상태와 지금 상태가 다를때



#### Unmaounting

- 컴포넌트가 브라우저에서 사라질때

##### com

- 설정할 리스너 언마운팅 하기







## TypeScript

https://react-etc.vlpt.us/06.typescript-basic.html



###### reference

JSX 참고문서: [https://react-anyone.vlpt.us/03.html](https://www.youtube.com/redirect?q=https%3A%2F%2Freact-anyone.vlpt.us%2F03.html&redir_token=WqG839__z-nbEwPhayTWcTZqvBN8MTU5MDQ3MzMwNkAxNTkwMzg2OTA2&v=8RVoVvgaQdY&event=video_description) 

let:  [https://developer.mozilla.org/ko/docs...](https://www.youtube.com/redirect?q=https%3A%2F%2Fdeveloper.mozilla.org%2Fko%2Fdocs%2FWeb%2FJavaScript%2FReference%2FStatements%2Flet&redir_token=WqG839__z-nbEwPhayTWcTZqvBN8MTU5MDQ3MzMwNkAxNTkwMzg2OTA2&v=8RVoVvgaQdY&event=video_description) 

const: [https://developer.mozilla.org/ko/docs...](https://www.youtube.com/redirect?q=https%3A%2F%2Fdeveloper.mozilla.org%2Fko%2Fdocs%2FWeb%2FJavaScript%2FReference%2FStatements%2Fconst&redir_token=WqG839__z-nbEwPhayTWcTZqvBN8MTU5MDQ3MzMwNkAxNTkwMzg2OTA2&v=8RVoVvgaQdY&event=video_description) 

화살표 함수: [https://developer.mozilla.org/ko/docs...](https://www.youtube.com/redirect?q=https%3A%2F%2Fdeveloper.mozilla.org%2Fko%2Fdocs%2FWeb%2FJavaScript%2FReference%2FFunctions%2F%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98&redir_token=WqG839__z-nbEwPhayTWcTZqvBN8MTU5MDQ3MzMwNkAxNTkwMzg2OTA2&v=8RVoVvgaQdY&event=video_description)

