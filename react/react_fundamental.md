# React.js 기초

## React.js 의 기본형태
```javascript
class RobotBox extends React.Componet {
	render() {
		return <div>Hello From React</div>;
	}
}

let target = document.getElementById('robot-app');

ReactDom.render(<RobotBox />, target);
```

모든 component는(코드에서 `class RobotBox`)
* `React.Component`를 `extends`해야 한다.
* `render()` function을 포함해야 한다.

`ReactDOM.render()`의 argument
* 첫 번째 argument는 `<component />`의 형태로 rendering할 component를 받는다
  * component의 첫 문자는 대문자로 쓴다. (HTML의 태그는 소문자)
* 두 번째 argument는 HTML의 id를 받아온 변수을 받는다.


## JSX 의 javascript 로의 변형
```javascript
<div>Story Box</div>
``` 를 javascript로 변경하면
```javascript
React.createElement('div', null, 'Story Box')
```

```javascript
<StoryBox />
```를 javascript로 변경하면
```javascript
React.createElement(StoryBox, null)
```과 같이 변경된다

* `React.createElement('element', 'attr', 'content')`와 같이 나타낼 수 있다.
* *attr는 dictionary 형태

## JSX -> HTML 로의 변환과정
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


## javascript 의 요소를 사용할 수 있다.
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
* CSS의 class를 사용할 때, class라고 쓰지 않고 className을 사용한다.


## JSX 에서의 반복문
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

