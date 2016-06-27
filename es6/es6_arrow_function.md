# ES6 - Arraw function

CoffeScript ���� ������ �κ��̴�.

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

* Fat Arrow �� ����: let FunctionName = (argument) => { function }
* Fat Arrow �� ���: this binding �� �ڵ����� �̷������. �� �Լ��� ����� ���� ����ȴ�.

* ���� �� ������ this �� �쿬�� window �� ���� ������, fat arrow �� �̿��� �Ͱ� �̿����� ���� ���� `this`���ε��� �ٸ���.

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
	var self = this;				// Animal�� ���� ������ self��� ������ �Ҵ��ؼ� ���
	self.age = 0;

	setInterval(function growUp() {
		self.age++;				// setInterval()�� callback�� growUp �ȿ�����
	}, 1000);					// Animal ��ü�� ���� ������ ��� �̾��
}
```