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

const title = document.querySelector("#hello");
와
const title = document.getElementById("hello"); 는 같은 일을 함
