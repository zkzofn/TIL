# React.js ����

## React.js �� �⺻����
![Imgur](http://i.imgur.com/ougcJUI.png)

## React.js �� �⺻����
```javascript
class RobotBox extends React.Component {
	render() {
		return <div>Hello From React</div>;
	}
}

let target = document.getElementById('robot-app');

ReactDom.render(<RobotBox />, target);
```

��� component ��(�ڵ忡�� `class RobotBox`�κ�)
* `React.Component`�� `extends`�ؾ� �Ѵ�.
* `render()` function�� �����ؾ� �Ѵ�.

`ReactDOM.render()`�� argument
* ù ��° argument�� `<component />`�� ���·� rendering�� component�� �޴´�
  * component�� ù ���ڴ� �빮�ڷ� ����. (HTML�� �±״� �ҹ���)
* �� ��° argument�� HTML�� id�� �޾ƿ� ������ �޴´�.


## JSX �� javascript ���� ����
```javascript
<div>Story Box</div>  //�� javascript�� �����ϸ�
```
```javascript
React.createElement('div', null, 'Story Box')
```

```javascript
<StoryBox />  //�� javascript�� �����ϸ�
```
```javascript
React.createElement(StoryBox, null)  //�� ���� ����ȴ�
```

* `React.createElement('element', 'attr', 'content')`�� ���� ��Ÿ�� �� �ִ�.
* *attr�� dictionary ����

## JSX -> HTML ���� ��ȯ����
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


## javascript �� ��Ҹ� ����� �� �ִ�.
* CSS�� class�� ����� ��, class��� ���� �ʰ� className�� ����Ѵ�.
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
���� <ul></ul> �±� ���� ������ �Ʒ��� ���� �����ȴ�.
```javascript
<li>HTML</li>
<li>Javascript</li>
<li>React</li>
```

## Component
### Component structure
Components �� ȭ���� ������ ���� �Ʒ� �׸��� ���� ������ ��Ҹ� component �� �����Ѵ�.
![Imgur](http://i.imgur.com/qsegLf7.png)

* �ϳ��� Component �� �ϳ��� function �̳� object �� �̷��.
* �ϳ��� Component�� �ϳ��� `.js`���Ͽ� �����Ѵ�. *1)
* **React.js �� ����** : �� ȭ�鿡 ���� Components �� �����൵ �ӵ��� ������.

1)
![Imgur](http://i.imgur.com/2i71mDb.png)

### Component ����
�ϳ��� Component �� ����ϱ� ���ؼ��� �Ʒ����� export ������� �Ѵ�.
```javascript
import React from 'react';

const SearchBar = () => {
	return <input />;
}

export default SearchBar;
```

������ ���� component�� �ٸ� `.js`���Ͽ��� import �Ͽ� ����� �� �ִ�.
```javascript
import React from 'react';
import ReactDOM from 'react-dom';

import SearchBar from 'search_bar';
```
������ ����Ű�� from 'search_bar' �� components/search_bar.js �� search_bar �� ����Ų��.


�������� `return`�ϰ� ���� ������ () �� ���´�.
```javascript
return (
	<div>
		<SearchBar />
	<div>
);
```

### Functional component / Class component �� ����
* Functional component (const �� ����)�� JSX�� �������� ���Ҹ� �Ѵ�. (������ ���!)
  * Props �� �̿��ؼ� input, output �� markup �ϴ� ���Ҹ� �Ѵ�.
* Class component (class �� ����)�� state, variables, methods �� �پ��� ����� �� �� �ִ�.

### Class component
Class component �� �Ʒ��� ���� `new`�� �̿��ؼ� ����� �� �ִ�.
```javascript
class SearchBar extends React.Component {
	render() {
		return <input />;
	}
}

var searchBarObject = new searchBar;
```

`extends React.Component`�� �� ���� ǥ�����

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

### State ����
`class component` �� `constructor`, `state` �� ���� �� �ִ�.
���⼭ `state`�� Ŭ������ ������� ������ �ϴ� ������ �����ߴ�.

`state` ���� ������ �� 
```javascript
render() {
	O - return <input onChange={event => this.setState({ term: event.target.value })} />;
	X = this.state.term = event.target.value;
}
```


### Event Handling
�̺�Ʈ �ڵ鸵�� JSX �±� ���� `on`�� ���ؼ� �̺�Ʈ �ڵ鸵�� �����ϴ�.

ex) `<input>`�� ���� �̺�Ʈ �ڵ鸵�� ������ ���� �� �� �ִ�.
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

���� ������ ES6 ������ �����Ͽ� `arrow function`�� �����ϸ� ������ ���� ǥ���� �� �ִ�.
```javascript
import React, { Component } from 'react';

class SearchBar extends Component {
	render() {
		return <input onChange={event => console.log(event.target.value)} />;
	}
}

export default SearchBar;
```

�� `event => ` ���� `event`�� argument �ε� argument�� �� ���� ���� ��ȣ���� ��� �����ϴ�.
Argument �� 2�� �̻��� ��쿡�� `(arg1, arg2, ...)` ���·� ����� �� �ִ�.




### Event Handling + state �� ��� ��
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


`state` �� ������� `param`�� �̸��� ������ `{ key : value }`�������� ���� �ʰ� `param` �ϳ��� ���൵ `setState` �� �����ϴ�.
`props`�� ����� �� class component ������ `this.props`�� ����ؾ� �ϰ�
functional component ������ argument �� �ޱ� ������ `this`���� `props`�� �ٷ� ����� �� �ִ�.

```javascript
class App extends Component {
	constructor(props) {
		super(props);

		this.state = { videos: [] };

		YTSearch({key: API_KEY, term: 'surfboards'}, (videos) => {
			this.setState({ videos });
		});
		// this.setState({ videos: videos }); �̷��� key : value �������� ���� �ʾƵ� ����
	}
}
```

### Youtube API ����ؼ� ������ ���
ù ��° `argument`�� youtube API�� configure option
�� ��° `argument`�� callback function
```javascript
YTSearch({key: API_KEY, term: 'surfboards'}, function(data) {
	console.log(data);
});
```


