# JS on the browser

##### - JS는 자동으로 HTML과 상호작용 <br/> - HTML 문서는 document라는 객체로 정의됨 <br/> - document는 JS에서 HTML에 접근할 수 있는 방법 <br/> - console에 document를 입력하면 작성한 HTML을 가져옴

---

## HTML in Javascript

- console.dir() -> JS객체의 모든 속성을 콘솔에 보여줌
- HTML에서 element(항목)을 가지고 와서 JS에서 항목 변경 가능

## Searching for elements

- document의 함수로 element를 가져오는 방법

1. getElementsBy어쩌구()
   -> array를 return
2. querySeletor()
   -> element를 css 방식으로 검색함
   -> selector 안의 첫 번째 element 한 개 만 return함
   -> querySlectorAll() 을 사용하면 모든 element를 return

   ex)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>momentum</title>
  </head>
  <body>
    <div class="hello">
      <h1>Grab me!</h1>
    </div>
    <script src="start.js"></script>
  </body>
</html>
```

```javascript
const title = document.querySelector(".hello h1");

console.log(title);
```

```javascript
const title = document.querySelector("div.hello:first-child h1");
console.log(title);
```

const title = document.querySelector("#hello");
와
const title = document.getElementById("hello"); 는 같은 일을 함

## Events

- 모든 js는 모든 event들을 listen 가능
- event를 listen 하는 법

  - 원하는element.addEventListener("원하는event", 원하는function) 의 형식
    -> removeEventListener로 event listener 제거 가능

    ex) click event를 listen 후 function 실행

  ```javascript
  const title = document.querySelector("div.hello:first-child h1");

  function handleTitleClick() {
    title.style.color = "lightblue";
  }

  title.addEventListener("click", handleTitleClick);
  ```

  - 원하는element.on원하는event = 원하는function 의 형식
    ex)

  ```javascript
  const title = document.querySelector("div.hello:first-child h1");

  function handleTitleClick() {
    title.style.color = "lightblue";
  }

  title.onclick = handleTitleClick;
  ```

- event 찾기

  - google search

  1. 찾고싶은 element에 mdn 붙여서 검색
  2. 링크에 Web APIs 문장 포함된 페이지 찾음
     -> js 관점의 HTML Heading Element란 의미

  - console.dir() 이용해서 element를 출력

  1. 출력 된 많은 property 중 on 붙은 것을 event listener로 사용 가능
  2. event로 쓸 때는 on 빼고 사용

  ex) 여러 event listener와 function

  ```javascript
  const title = document.querySelector("div.hello:first-child h1");

  function handleTitleClick() {
    title.style.color = "lightblue";
  }

  function handleMouseEnter() {
    title.innerText = "Mouse is here!";
  }

  function handleMouseLeave() {
    title.innerText = "Mouse is gone!";
  }

  title.addEventListener("click", handleTitleClick);
  title.addEventListener("mouseenter", handleMouseEnter);
  title.addEventListener("mouseleave", handleMouseLeave);
  ```

- window event listener도 다양하게 존재

## CSS in Javascript

ex) 코드 더 깔끔하게

```javascript
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
  if (h1.style.color === "blue") {
    h1.style.color = "lightblue";
  } else {
    h1.style.color = "blue";
  }
}

h1.addEventListener("click", handleTitleClick);
```

↓

```javascript
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
  const currentColor = h1.style.color;
  let newColor;
  if (currentColor === "blue") {
    newColor = "lightblue";
  } else {
    newColor = "blue";
  }
  h1.style.color = newColor;
}

h1.addEventListener("click", handleTitleClick);
```

- css에서 ._classname_ 에 색깔 등의 무언가를 할당 후 이 class를 어떤 element에 지정하면 element는 할당 된 스타일을 가짐
  ex)

```css
body {
  background-color: lemonchiffon;
}
h1 {
  color: cornflowerblue;
  transition: color 0.5s ease-in-out;
}

.active {
  color: slateblue;
}
```

```javascript
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
  if (h1.className === "active") {
    h1.className = "";
  } else {
    h1.className = "active";
  }
}

h1.addEventListener("click", handleTitleClick);
```

위 예시의 active처럼 raw string을 반복해서 쓰는 경우 오타같은 에러 자주 남 -> 안좋은 코드
-> 그냥 constant 해주는게 좋음
ex)

```javascript
const h1 = document.querySelector("div.hello:first-child h1");

function handleTitleClick() {
  const activeClass = "active";
  if (h1.className === activeClass) {
    h1.className = "";
  } else {
    h1.className = activeClass;
  }
}

h1.addEventListener("click", handleTitleClick);
```

- 기존에 쓴 class name을 유지하려면 js로 class name 변경하는건 좋지않음 -> 일 많아짐
  ↓
  classList 사용

  - class들의 목록으로 작업 가능
    (className은 이전 class들과 상관 없이 모든 것을 교체해버림)
  - classList만의 다양한 function이 또 존재
    ex) classList.contains : 명시한 class가 HTML element의 class에 포함되어 있는지 알려줌

  ex)

  ```javascript
  const h1 = document.querySelector("div.hello:first-child h1");

  function handleTitleClick() {
    const activeClass = "active";
    if (h1.classList.contains(activeClass)) {
      h1.classList.remove(activeClass);
    } else {
      h1.classList.add(activeClass);
    }
  }
  h1.addEventListener("click", handleTitleClick);
  ```

  ↓
  toggle function으로 한 번에 구현 가능
  ex)

  ```javascript
  const h1 = document.querySelector("div.hello:first-child h1");

  function handleTitleClick() {
    h1.classList.toggle("active");
  }

  h1.addEventListener("click", handleTitleClick);
  ```
