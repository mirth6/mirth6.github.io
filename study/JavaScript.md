# JavaScript

[TOC]



### 기초--------------------------------------------------------------------

##### 변수

```javascript
var
let
const
```

##### 배열

```javascript
var arr = [10,20,30,40,50];
var mixArr = [10, "string", variable];

console.log(arr)				>> [10,20,30,40,50]
console.log(arr[0])				>> 10
```

##### Object

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

console.log(person.age) >> 26

document.write(person['name']);					>> [object Object]
document.write(person['name']['firstname']);	>> 혜희
document.write(person['age']);					>> 26
```



##### 연산

```javascript
var num = 100;
var str = '100';
        
console.log(num+num);			>>200
console.log(str+str);			>>100100
console.log(num**num);			>>10000 (100^100)
console.log(num == str);		>>true (타입 안봄)
console.log(num === str);		>>false
```

##### if문

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

##### switch문

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

##### 반복문

```javascript
arr = [10,20,30,40,50];

for(var i=0; i<arr.length; i++){
    document.write(arr[i]);
}
    
while (j<10){
    document.write(j);
    j++;
}
```

##### 







##### 출력

```html
<body>
    <p id="one"> hello world </p>
    
    <script>
		document.getElementById('one').innerHTML = '';
    	document.write('');
    	window.alert('경고창');
    	console.log('콘솔');
	</script>
</body>
```

*순차적으로 읽음 -> script를 body뒤에 두는게 좋아

##### 함수

```html
<script>
	function func(x,y){
        var z;
        z = x+y;
        console.log(`${x} plus ${y} is ${z}`)
        return z
    }
    document.write( func(3,6) );
</script>
```

##### DOM 함수

```html
<body>
	<h1 id="title"> This is Title </h1>
	<script>
		const t = document.getElementById("title")
        console.log(t)		>> 
	</script>
</body>
```

##### 내장함수

```html
<script>
	var txt = 'hello world';
    document.write(txt.length);					>>11
    document.write(txt.indexOf('world'));		>>6
    document.write(txt.slice(0,3));				>>hel
    document.write(txt.replace('world','you'));	>>hello you
    document.write(txt.toUpperCase());			>>HELLO WORLD
    
    var num = 10;
    document.write(num.toFixed(3));				>>10.000
    document.write(num.toString());				>>10
    
    document.write(Math.PI);					>>3.141592653589793
    document.write(Math.max(10,20,30));			>>30
    document.write(Math.random());				>>0~1사이의 랜덤한 수
    
    var date = new Date();
    document.write(date);						>>Wed Sep 25 2019 16:28:10 GMT+0900 (한국 표준시)
    document.write(date.getMonth()+1);			>>9 (1월: 0)
    document.write(date.getDate());				>>25
    document.write(date.getDay());				>>3 (일요일: )
    document.write(date.getHours());			>>16
</script>
```

##### 배열

```html
<script>
    var arr = [10,20,30,40,50];
    document.write(arr[2]);				>>30
    document.write(arr.slice(1,4));		>>20,30,40
    document.write(arr.pop());			>>50	(arr=[10,20,30,40])
    arr.push(1000);						>> (arr=[10,20,30,40,1000])			
    document.write(arr.join("!"));		>>10!20!30!40!1000
    document.write(arr.sort());			>>10,1000,20,30,40 (사전식 정렬)
    document.write(arr.reverse());		>>40,30,20,1000,10
</script>
```

##### object

```html
<script>
	var person = {
        name:{
            firstname: '혜희',
            lastname: '김',  
        },
        age:26,
        married:false,
    };
    person.age >> 26
	document.write(person['name']);					>>[object Object]
    document.write(person['name']['firstname']);	>>혜희
    document.write(person['age']);					>>26
</script>
```

##### 변수 scope

```html
<script>
	var v=10
    if(v>5){
       	var blockV = 10;
    	let blockL = 20;
    	const blockC = 30; 
    }
    document.write(blockV);		>>10
    document.write(blockL);		>>''
    document.write(blockC);		>>''
        
    function func(){
        var fv = 10;
        v += 100;
    }
    func();
    document.write(fv)			>>''
    document.write(v)			>>110
</script>
```

var: function scope

let :block scope

const: block scope

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