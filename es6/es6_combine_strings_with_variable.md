# ES6 - Combine strings with variable

```javascript
// 일반적으로 이렇게 사용하는 방식을
const url = 'https://www.youtube.com/embed' + videoId;

// 이렇게 사용할 수 있다.
const url = `https://www.youtube.com/embed/${videoId}`;


// *주의: 기존 방식은 ''으로 묶여있고 
//        새 방식에서는 ``으로 묶여있다.
```