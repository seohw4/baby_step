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

- username이 빈칸이거나 너무 길지 않도록 확인
  - .length로 string의 길이 확인
    ↓

```javascript
const loginInput = document.querySelector("#login-form input");
const loginButton = document.querySelector("#login-form button");

function loginButtonClick() {
  const username = loginInput.value;
  if (username === "") {
    alert("Please write your name");
  } else if (username.length > 15) {
    alert("Your name is too long");
  }
}

loginButton.addEventListener("click", loginButtonClick);
```

사실 input 자체의 기능으로 위와 같이 길게 코드 짜지 않아도 가능
++ input의 유효성 검사를 작동시키려면 input이 form 안에 있어야함
↓

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <mata charset="UTF-8" />
    <mata name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Momentum App</title>
  </head>
  <body>
    <form id="login-form">
      <input
        required
        maxlength="15"
        type="text"
        placeholder="What is your name?"
      />
      <button>Log In</button>
    </form>
    <script src="start.js"></script>
  </body>
</html>
```

```javascript
const loginInput = document.querySelector("#login-form input");
const loginButton = document.querySelector("#login-form button");

function loginButtonClick() {
  const username = loginInput.value;
  console.log(username);
}

loginButton.addEventListener("click", loginButtonClick);
```

username을 입력하고 버튼을 눌렀을 때 페이지가 새로고침 됨
→ input안에 있는 button을 누르거나 type이 submit인 input을 눌렀을 때 input이 더 존재하지 않는다면 자동으로 form이 submit되기 때문
→ button 안누르고 그냥 enter쳐도 submit 됨
→→ 결국 button을 clink하는 행위가 의미 없어졌다는 말
