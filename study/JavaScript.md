# JavaScript

[TOC]



## 기초--------------------------------------------------------------------

#### 변수

```javascript
var
let
const
```

##### 변수 선언, 할당

```javascript
/* var : 재선언, 재할당 가능 */		   
var test = 'test1';					>>test1
var test = 'test2';					>>test2
test = 'test3';						>>test3

/* let : 재선언 불가능, 재할당 가능 */
let test = 'test1';					>>test1
let test = 'test2';					>>error!!!
test = 'test3';						>>test3

/* const : 재선언, 재할당 불가능*/
const test = 'test1'				>>test1
const test = 'test2'				>>error!!!
test = 'test3'						>>error!!!
```

##### 변수 scope

```javascript
if(v>5){
    var blockV = 10;
    let blockL = 20;
    const blockC = 30; 
}
console.log(blockV);		>>10
console.log(blockL);		>>''
console.log(blockC);		>>''

var v=10
function func(){
    var fv = 10;
    v += 100;
}
func();
console.log(fv)			>>''
console.log(v)			>>110

```

var: function scope

let :block scope

const: block scope

#### 배열

```javascript
var arr = [10,20,30,40,50];
var mixArr = [10, "string", variable];

console.log(arr)				>> [10,20,30,40,50]
console.log(arr[0])				>> 10
```

#### Object

```javascript
var person = {
	name:{
		firstname: '혜희',
		lastname: '김',  
	},
	age:26,
	married:false,
    favorite: ["밥","잠",2],
};

console.log(person.age) 					>> 26

document.write(person['name']);					>> [object Object]
document.write(person['name']['firstname']);	>> 혜희
document.write(person['age']);					>> 26
```

#### 함수

```javascript
function func(x,y){
    var z;
    z = x+y;
    console.log(`${x} plus ${y} is ${z}`)		>>3 plus 6 is 9
    return z
}
    
console.log( func(3,6) );						>>9
```

##### 내장함수

```javascript
var txt = 'hello world';
console.log(txt.length);					>>11
console.log(txt.indexOf('world'));			>>6
console.log(txt.slice(0,3));				>>hel
console.log(txt.replace('world','you'));	>>hello you
console.log(txt.toUpperCase());				>>HELLO WORLD
    
var num = 10;
console.log(num.toFixed(3));				>>10.000
console.log(num.toString());				>>10
    
console.log(Math.PI);						>>3.141592653589793
console.log(Math.max(10,20,30));			>>30
console.log(Math.random());					>>0~1사이의 랜덤한 수

var arr = [10,20,30,40,50];
console.log(arr[2]);						>>30
console.log(arr.slice(1,4));				>>20,30,40
console.log(arr.pop());						>>50	(arr=[10,20,30,40])
arr.push(1000);								>> (arr=[10,20,30,40,1000])			
console.log(arr.join("!"));					>>10!20!30!40!1000
console.log(arr.sort());					>>10,1000,20,30,40 (사전식 정렬)
console.log(arr.reverse());					>>40,30,20,1000,10

var date = new Date();
console.log(date);							>>Wed Sep 25 2019 16:28:10 GMT+0900 (한국 표준시)
console.log(date.getMonth()+1);				>>9 (1월: 0)
console.log(date.getDate());				>>25
console.log(date.getDay());					>>3 (일요일: )
console.log(date.getHours());				>>16
```

##### 



#### 연산

```javascript
var num = 100;
var str = '100';
        
console.log(num+num);			>>200
console.log(str+str);			>>100100
console.log(num**num);			>>10000 (100^100)
console.log(num == str);		>>true (타입 안봄)
console.log(num === str);		>>false
```

#### if문

```javascript
if(false){
	console.log('if');
}else if(true){
	console.log('else if');
}else{
	console.log('else');
}

>> else if
```

#### switch문

```javascript
var n = 2;
switch(n){
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

#### 반복문

```javascript
arr = [10,20,30,40,50];

for(var i=0; i<arr.length; i++){
    consol.log(arr[i]);					>>10 20 30 40 50
}
    
j = 1
while (j<5){
    console.log(j);						>>1 2 3 4
    j++;
}
```







## with HTML

##### 1. body안에 바로 작성

```html
<html>
	<head>
    	<title> 헤드 제목 </title>
        <link rel="stylesheet" href="index.css" />
	</head>    

	<body>
    	<p id="one"> hello world </p>
     ***********************************************************
    	<script>
			document.getElementById('one').innerHTML = '';
    		document.write('');
    		window.alert('경고창');
    		console.log('콘솔');
		</script>
     ***********************************************************
	</body>
</html>
```

*순차적으로 읽음 -> script를 body뒤에 두는게 좋아

##### 2. 다른 파일로 작성

```html
<html>
	<head>
    	<title> 헤드 제목 </title>
        <link rel="stylesheet" href="index.css" />
	</head>     

	<body>
    	<p id="one"> hello world </p>
      ***********************************************************
    	<script src="index.js"> </script>
      ***********************************************************
	</body>
</html>
```

###### index.js

```js

```



#### 출력



#### DOM 함수

```html
<body>
	<h1 id="title"> This is Title </h1>
    
	<script>
		const t = document.getElementById("title")
        console.log(document)							>
        console.log(t)									>> This is Title
	</script>
</body>
```



##### getElement

```html
<body>
    
    <div class = "one"> 일 </div>
    <div class = "one two" id=""> 이 </div>
    <div class = "one two four"> 삼 </div>
    <script>
        k = document.getElementsByClassName('one');
        document.write(k['0']['innerHTML']);		>>일
        document.write(k['2']['className']);		>>one two four

    </script>
</body>
```

​	document.getElementById('id');
​    document.querySelector('query');

​    document.getElementsByName('name');
​    document.getElementsByClassName('classname');
​    document.querySelectorAll('query');

#### event

이벤트 종류 참조: https://developer.mozilla.org/ko/docs/Web/Events

.addEventListener("이벤트 이름", 함수);

```javascript
function handleResize(event){		//자바 스크립트가 자동으로 Event객체를 만들어서 넘겨줌
    console.log(event)		
    console.log("사이즈가 조정되었습니다.")
}

window.addEventListener("resize",handleResize);		//이벤트 발생시 함수 호출
window.addEventListener("resize",handleResize());	//이벤트 발생 안해도 바로 함수 호출
```

```html
<body>
	<h1 id="title"> 제목 </h1>
    
<script>
    const title = document.querySelector("#title");

    function handleClick(){
		title.style.color = "blue"
    }

    title.addEventListener("click",handleClick);
</script>
</body>

>>'제목'을 클릭하면 글자가 파란색으로 바뀜
```



### 글자색 바꾸기

###### index.html

```html
<html>
	<head>
    	<title> 헤드 제목 </title>
        <link rel="stylesheet" href="index.css" />
	</head>     

	<body>
    	<h1 id="hello"> 헬로 월드! </p>
    	<script src="index.js"> </script>
	</body>
</html>
```

###### index.css

```css
h1 {
    color: #000000;	//검정색
}

.clicked{
	color: #ffffff; //흰색
}
```

###### index.js

```javascript
const title = document.querySelector('#hello');

const CLICKED_CLASS = "clicked"

function handleClick(){
    
    const hasClass = title.classList.contains(CLICKED_CLASS);
    if(hasClass){
        title.classList.remove(CLICKED_CLASS);
    }else{
    	title.classList.add(CLICKED_CLASS);    
    }
    
}

title.addEventListener("click",handleClick);

>> '헬로 월드!'를 클릭하면 흰색<->검정색으로 바뀜
```

[7]~[12] 코드를 title.classList.toggle(CLICKED_CLASS);로 대체 가능

