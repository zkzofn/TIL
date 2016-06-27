# ES6 - Arraw function

CoffeScript 에서 차용한 부분이다.

```javascript 
let fn = (x, y, z) => {
	console.log(this);
	console.log(x, y, z);
	return
}

fn(1, 2, 3);



var fn = function(x, y, z) {
	console.log(x, y, z);
	console.log(this);
	return 1;
}

fn(1, 2, 3);
```

* Fat Arrow 의 문법: let FunctionName = (argument) => { function }
* Fat Arrow 의 기능: this binding 이 자동으로 이루어진다. 이 함수가 선언된 곳과 연결된다.

* 위의 두 예제는 this 가 우연히 window 에 나와 있지만, fat arrow 를 이용한 것과 이용하지 않은 것의 `this`바인딩은 다르다.

```javascript
//ES6
function Animal() {
	this.age = 0;
	
	setInterval(() => {
		this.age++;
	}, 1000);
}

var animal = new Animal();


//OLD WAY
function Animal() {
	var self = this;				// Animal에 대한 참조를 self라는 변수에 할당해서 사용
	self.age = 0;

	setInterval(function growUp() {
		self.age++;				// setInterval()의 callback인 growUp 안에서도
	}, 1000);					// Animal 객체에 대한 참조를 계속 이어나감
}
```