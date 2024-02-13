### LOGIN

- div 에 class나 id 중 하나 추가
- querySelector()로는 classname, tagname 모두 검색 가능하므로, 대상이 id인지 무엇인지 원하는 것을 명확히 해줘야함
- click을 인지해서 input의 value 얻음
  ↓

```javascript
const loginForm = document.querySelector("#login-form");
const loginInput = loginForm.querySelector("input");
const loginButton = loginForm.querySelector("button");

function loginButtonClick() {
  console.log(loginInput.value);
}

loginButton.addEventListener("click", loginButtonClick);
```
