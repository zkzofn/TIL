# React.js 기초

## React.js 의 기본구조
![Imgur](http://i.imgur.com/ougcJUI.png)

## React.js 의 기본형태
```javascript
class RobotBox extends React.Component {
	render() {
		return <div>Hello From React</div>;
	}
}

let target = document.getElementById('robot-app');

ReactDom.render(<RobotBox />, target);
```

모든 component 는(코드에서 `class RobotBox`부분)
* `React.Component`를 `extends`해야 한다.
* `render()` function을 포함해야 한다.

`ReactDOM.render()`의 argument
* 첫 번째 argument는 `<component />`의 형태로 rendering할 component를 받는다
  * component의 첫 문자는 대문자로 쓴다. (HTML의 태그는 소문자)
* 두 번째 argument는 HTML의 id를 받아온 변수을 받는다.


## JSX 의 javascript 로의 변형
```javascript
<div>Story Box</div>  //를 javascript로 변경하면
```
```javascript
React.createElement('div', null, 'Story Box')
```

```javascript
<StoryBox />  //를 javascript로 변경하면
```
```javascript
React.createElement(StoryBox, null)  //과 같이 변경된다
```

* `React.createElement('element', 'attr', 'content')`와 같이 나타낼 수 있다.
* *attr는 dictionary 형태

## JSX -> HTML 로의 변환과정
1. JSX
```javascript
<div>
	<h3>Stories App</h3>
	<p> className="lead">Sample paragraph</p>
<div>
```
2. javascript
```javascript
React.createElement("div", null,
	React.createElement("h3", null, "Stories App"),
	React.createElement("p", {className:"lead"}, "Sample paragraph")
);
```

3. HTML
```javascript
<div> data-reactroot>
	<div>
		<h3>Stories App</h3>
		<p class="lead">Sample paragraph</p>
	</div>
</div>
```


## javascript 의 요소를 사용할 수 있다.
* CSS의 class를 사용할 때, class라고 쓰지 않고 className을 사용한다.
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
위의 <ul></ul> 태그 안의 내용은 아래와 같이 변형된다.
```javascript
<li>HTML</li>
<li>Javascript</li>
<li>React</li>
```

## Component
### Component structure
Components 가 화면을 구성할 때는 아래 그림과 같이 각각의 요소를 component 로 구성한다.
![Imgur](http://i.imgur.com/qsegLf7.png)

* 하나의 Component 는 하나의 function 이나 object 를 이룬다.
* 하나의 Component는 하나의 `.js`파일에 구현한다. *1)
* **React.js 의 장점** : 한 화면에 많은 Components 를 보여줘도 속도가 빠르다.

1)
![Imgur](http://i.imgur.com/2i71mDb.png)

### Component 기초
하나의 Component 를 사용하기 위해서는 아래에서 export 시켜줘야 한다.
```javascript
import React from 'react';

const SearchBar = () => {
	return <input />;
}

export default SearchBar;
```

위에서 만든 component를 다른 `.js`파일에서 import 하여 사용할 수 있다.
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

import SearchBar from 'search_bar';
```
위에서 가리키는 from 'search_bar' 는 components/search_bar.js 의 search_bar 를 가리킨다.


여러줄을 `return`하고 싶을 때에는 () 로 묶는다.
```javascript
return (
	<div>
		<SearchBar />
	<div>
);
```

### Functional component / Class component 의 차이
* Functional component (const 로 선언)는 JSX를 내보내는 역할만 한다. (간단한 기능!)
  * Props 를 이용해서 input, output 을 markup 하는 역할만 한다.
* Class component (class 로 선언)는 state, variables, methods 등 다양한 기능을 할 수 있다.

### Class component
Class component 는 아래와 같이 `new`를 이용해서 사용할 수 있다.
```javascript
class SearchBar extends React.Component {
	render() {
		return <input />;
	}
}

var searchBarObject = new searchBar;
```

`extends React.Component`의 두 가지 표현방식

1.
```javascript
import React from 'react';

class SearchBar extends React.Component {}

```
2.
```javascript
improt React, { Component } from 'react';

class SearchBar extends Component {}
```

### State 기초
`class component` 는 `constructor`, `state` 를 가질 수 있다.
여기서 `state`는 클래스의 멤버변수 역할을 하는 것으로 이해했다.

`state` 값을 설정할 때 
```javascript
render() {
	O - return <input onChange={event => this.setState({ term: event.target.value })} />;
	X = this.state.term = event.target.value;
}
```


### Event Handling
이벤트 핸들링은 JSX 태그 안의 `on`을 통해서 이벤트 핸들링이 가능하다.

ex) `<input>`에 대한 이벤트 핸들링은 다음과 같이 할 수 있다.
```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
	render () {
		return <input onChange={this.onInputChange} />;
	}

	onInputChange(event) {
		console.log(event.target.value);
	}
}

export default SearchBar;
```

위의 내용을 ES6 문법을 적용하여 `arrow function`을 적용하면 다음과 같이 표현할 수 있다.
```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
	render() {
		return <input onChange={event => console.log(event.target.value)} />;
	}
}

export default SearchBar;
```

위 `event => ` 에서 `event`는 argument 인데 argument가 한 개인 경우는 괄호없이 사용 가능하다.
Argument 가 2개 이상일 경우에는 `(arg1, arg2, ...)` 형태로 사용할 수 있다.




### Event Handling + state 값 사용 예
```javascript
import React, { component } from 'react';

class SearchBar extents Component {
	constructor(props) {
		super(props);
		
		this.state = { term: '' }
	}

	render() {
		return (
			<div>
				<input onChange={event => this.setState({ term: event.target.value })} />
				Value of the input: {this.state.term}
			</div>
		)
	}
}

export default SearchBar;
```

![Imgur](http://i.imgur.com/H6RqP6W.png)


`state` 의 변수명과 `param`의 이름이 같으면 `{ key : value }`형식으로 쓰지 않고 `param` 하나만 써줘도 `setState` 가 가능하다.
`props`를 사용할 때 class component 에서는 `this.props`로 사용해야 하고
functional component 에서는 argument 로 받기 때문에 `this`없이 `props`로 바로 사용할 수 있다.

```javascript
class App extends Component {
	constructor(props) {
		super(props);

		this.state = { videos: [] };

		YTSearch({key: API_KEY, term: 'surfboards'}, (videos) => {
			this.setState({ videos });
		});
		// this.setState({ videos: videos }); 이렇게 key : value 형식으로 쓰지 않아도 가능
	}
}
```

### Youtube API 사용해서 동영상 재생
첫 번째 `argument`는 youtube API의 configure option
두 번째 `argument`는 callback function
```javascript
YTSearch({key: API_KEY, term: 'surfboards'}, function(data) {
	console.log(data);
});
```


