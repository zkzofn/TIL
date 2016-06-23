# React.js ����

## React.js �� �⺻����
```javascript
class RobotBox extends React.Componet {
	render() {
		return <div>Hello From React</div>;
	}
}

let target = document.getElementById('robot-app');

ReactDom.render(<RobotBox />, target);
```

��� component��(�ڵ忡�� `class RobotBox`)
* `React.Component`�� `extends`�ؾ� �Ѵ�.
* `render()` function�� �����ؾ� �Ѵ�.

`ReactDOM.render()`�� argument
* ù ��° argument�� `<component />`�� ���·� rendering�� component�� �޴´�
  * component�� ù ���ڴ� �빮�ڷ� ����. (HTML�� �±״� �ҹ���)
* �� ��° argument�� HTML�� id�� �޾ƿ� ������ �޴´�.


## JSX �� javascript ���� ����
```javascript
<div>Story Box</div>
``` �� javascript�� �����ϸ�
```javascript
React.createElement('div', null, 'Story Box')
```

```javascript
<StoryBox />
```�� javascript�� �����ϸ�
```javascript
React.createElement(StoryBox, null)
```�� ���� ����ȴ�

* `React.createElement('element', 'attr', 'content')`�� ���� ��Ÿ�� �� �ִ�.
* *attr�� dictionary ����

## JSX -> HTML ���� ��ȯ����
* JSX
```javascript
<div>
	<h3>Stories App</h3>
	<p> className="lead">Sample paragraph</p>
<div>
```
* javascript
```javascript
React.createElement("div", null,
	React.createElement("h3", null, "Stories App"),
	React.createElement("p", {className:"lead"}, "Sample paragraph")
);
```

* HTML
```javascript
<div> data-reactroot>
	<div>
		<h3>Stories App</h3>
		<p class="lead">Sample paragraph</p>
	</div>
</div>
```


## javascript �� ��Ҹ� ����� �� �ִ�.
```javascript
class StoryBox extends React.Component {
	render() {
		const now = new Date();

		return (
			<div>
				<h3>Stories</h3>
				<p className="lead">
					Current time: {now.toTimeStrings()}
				</p>
			</div>
		);
	}
}
```
* CSS�� class�� ����� ��, class��� ���� �ʰ� className�� ����Ѵ�.


## JSX ������ �ݺ���
```javascript
class StoryBox extends React.Component {
	render() {
		...
		const topicsList = ['HTML', 'JavasScript', 'React'];

		return (
			<div>
				...
				<ul>
					{topicsList.map( topic => <li>{topic}</li> )}
				</ul>
			</div>
		);
	}
}
```

