📌 https://velog.io/@greenth322/DOM-%EC%A0%95%EB%A6%AC 

***

### DOM이란??

- HTML 문서 내용을 트리형태로 구조화하여 웹페이와 JS(프로그래밍을 연결)
- 브라우저에 자바스크립트를 연결하기 전 ‘파싱’하는 것이 돔!
- ***파싱: 바꾸다, 전환하다***
- **노드**: 각 요소와 속성, 콘텐츠 표현 단위 (텍스트, 주석,줄바꿈까지 다 노드)*
- 노드 범위 안에 요소가 있는 것
- 유사배열객체: 키값을 인덱스처럼 만들어서 사용

### DOM 트리 접근하기

- getElement시리즈들은 불편해서 잘 쓰지 않음 (IE8부터 지원이 가능하지만)
- document.getElementsByTagName('li')[0] —> 불편
- querySelector은 처음 값만, querySelectorAll 해당 모든 값

```jsx
// 해당하는 Id를 가진 요소에 접근하기
document.getElementById()

// 해당하는 모든 요소에 접근하기
document.getElementsByTagName();

// 해당하는 클래스를 가진 모든 요소에 접근하기
document.getElementsByClassName();

**// css 선택자로 단일 요소에 접근하기
document.querySelector("selector");

// css 선택자로 여러 요소에 접근하기
document.querySelectorAll("selector");**
```

### DOM 제어 명령어

1. **이벤트 삽입**

`target.addEventListener( type, listener )`

- type: click, mouseover, mouseout, whell ...
- 우선: **mousedown > blur > mouseclick > click**
- event type가 너무 많기 때문에 여기서 찾아서 쓰기

[https://developer.mozilla.org/ko/docs/Web/Events](https://developer.mozilla.org/ko/docs/Web/Events)

```jsx
const myBtn = document.querySelector("button");

myBtn.addEventListener('click', function(){
	console.log("hello world");
})
```

1. **class 제어하기 - 실습 023.htm(클릭하면 색상 바꾸기)**
- **DOM api로 요소의 class 제어**
- classList.add(): 클래스 생성
- classList.toggle(): 클래스 토글, 없으면 넣고, 있으면 제거
- classList.remove(): 클래스 제거
- classList.contains(): 해당 클래스 있는지 확인

1. **요소 제어**
- **DOM api로 요소 생성, 제거, 위치**
- **createElement(target):** target 요소 만들기
- **createTextNode(target):** target 텍스트 생성
- **appendChild**: 자식으로 붙인다./ **append**를 사용하기도 한다(최근 생긴 기능) —> 텍스트 요소를 바로 자식 요소로 넣을 수도 있는데, ei에 지원이 안된다는 건 역시...
- **removeChild(target):** element의 target 자식 요소 제거
- **insertBefore(target, location):** 타겟 요소를 로케이션 앞으로

1. **JS 문자열로 element, text노드 생성 및 추가하기**

```html
<p></p>
<input type="text">
<button>Write Something!</button>
```

**중요!** **myP.textContent = myInput.value;**

```jsx

const myBtn = document.querySelector("button");
const myP = document.querySelector("p");
const myInput = document.querySelector("input");

myBtn.addEventListener('**click**', function(){
	myP.textContent = myInput.value;
});

// input 요소에 'input' 이벤트를 연결하면 실시간으로 값이 반영되게 만들 수도 있습니다.
myInput.addEventListener('**input**', ()=>{
  myP.textContent = myInput.value;
});
```

026.html ) 

```jsx
myP.innerHTML = "<strong>I'm Strong!!</strong>";
myP.outerHTML = "<div></div>";

// innerText 속성은 요소의 **렌더링된** 텍스트 콘텐츠를 나타냅니다. 
//(**렌더링된**에 주목하세요. ****innerText는 "사람이 읽을 수 있는" 요소만 처리합니다.)
// textContent 속성은 노드의 텍스트 콘텐츠를 표현합니다
```

 **innerHTML** 

*요소(element) 내에 포함된 HTML 마크업을 가져오거나 설정*
태그 이름들이 나오지 않고, 우리가 평소 html 작성한 것처럼 텍스트만 깔끔하게 보임
단점: 경고, 보안에 취약하기 때문에 사용 지양

**! 주의 사항 !** 

인라인으로 JS나 style 등을 적어서 오류 만들지 말기 
무조건 js, css ,html 파일 따로따로 만들어서 관리하자
ex) onclick도 같이 인라인에 쓸 것을 addEvetListner(’click’, listner)로 사용

```jsx
//string으로 넣어도 (이미지 로드 실패)오류가 뜨는 경우임
const name = "<img src='x' onerror='alert(1)'>";
document.querySelector('div').innerHTML = name; // shows the alert
```

**innerText 와 textContent**
```jsx
const myP = document.querySelector("p");
myP.innerText = "<strong>I'm Strong!!</strong>";
myP.textContent = "<strong>I'm Strong!!</strong>";
```

**❗ innerText**
- innerText는 정말 사람이 읽어야만 하는 콘텐츠만 보여줌
- 편리할 것 같지만 css에 순종적이라는 단점이 있음 
	- visibility:hidden 같은 비표시 속성 노드는 반환 X
    - css를 고려하여 로드하느라 textContent보다 느림
    
**❗ textContent**
- textContent는 다른 노드들도 같이 출력이 됨
- 그래서 사용할 때 생긴 텍스트 여백을 trim()의 방법으로 없애서 사용한다.

1. **insertAdjacnetHTML:**

요소 노드를 주어진 위치에 배치


```jsx

<strong class="sayHi">
    반갑습니다.
</strong>

const sayHi = document.querySelector('.sayHi');
sayHi.insertAdjacentHTML('beforebegin', '<span>안녕하세요 저는</span>');
sayHi.insertAdjacentHTML('afterbegin', '<span>재현입니다</span>');
sayHi.insertAdjacentHTML('beforeend', '<span>면접오시면</span>');
sayHi.insertAdjacentHTML('afterend', '<span>치킨사드릴게요</span>');

```

**1. DOM 안에서 노드 탐색**
**노드 ≠ 요소 (노드 범위 안에 요소가 있는 것)**
**암기하기**

```html
<!-- 주석입니다 주석. -->
<article class="cont">
    <h1>안녕하세요 저는 이런 사람입니다.</h1>
    <p>지금부터 자기소개 올리겠습니다</p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Deserunt incidunt voluptates laudantium fugit, omnis
    dolore itaque esse exercitationem quam culpa praesentium, quisquam repudiandae aut. Molestias qui quas ea iure
    officiis.
    <strong>감사합니다!</strong>
</article>
```

```jsx
const cont = document.querySelector(".cont");
console.log(cont.firstElementChild);  // 첫번째 자식을 찾습니다.
console.log(cont.lastElementChild);   // 마지막 자식을 찾습니다.
console.log(cont.nextElementSibling); // 다음 형제요소를 찾습니다.
//previousElementSibling: 이전 형제 요소를 찾는 게 따로 있음 != 노드
console.log(cont.previousSibling);    // 이전 형제노드를 찾습니다.
console.log(cont.children);           // 모든 직계자식을 찾습니다.
console.log(cont.parentElement);      // 부모 요소를 찾습니다.
```

- 텍스트, 주석,줄바꿈까지 다 노드다.
- element가 있어야 요소를 찾는 것
- 자주 사용하지만, 나중에 요소나 노드가 추가되면 엉키게 되는 문제가 발생할 수 있기 때문에, class로 직접 호명하는 게 제일 안전하건 맞다.
    
    —> css에서 nth-child와 비슷한 것
    

### 이벤트 객체

- addEventListener - 이벤트핸들러, 이벤트리스너로 불림
- 이밴트핸들러에는 이벤트와 관련된 모든 정보를 가지는 매개변수가 전동됨
    —> 이게 바로 이벤트 객체
    
```jsx
const btnFirst = document.querySelector('.btn-first');
        //이벤트핸들러 = 이벤트리스너라고 부른다
        btnFirst.addEventListener('click', (event) => {
            console.log(event); //event는 자동완성으로 만들어진 것, 이름은 내 마음대로 바꿔도 됨, e로 많이 씀
        });

//원범님의 설명
**function handleClick(param){
  return function(event){
  }
}
element.addEventListener("click",handleClick(뭐변수이런거))**
```

### 이벤트 흐름 ⭐⭐⭐ - 028.html

***면접에서 다수 기출됨으로 냅다 압기하기***

***이 이벤트 흐름이 이벤트 객체 정보에 싹 들어가있는 거*** 

**[이벤트 흐름 설명]**

이벤트가 시작된다 (ex- click)

**1단계 캡처링**

- 윈도우 → document→ body →타겟까지, 이벤트가 발생한 곳을 찾을 떄까지 DOM트리를 따라서 내려감 (캡처링 이벤트: addEventListener에서 true가 적힌 곳을 찾는다 )

**2단계 버블링**

- 다시 거꾸로  돔을 타고 올라가면서 버블링 ```addEventListener``` 실행
- 부모요소를 타고 올라감
- true값이 없거나 false가 적혀 있는 것
- 우리가 지금까지 배워온 것

—> 항상 캠처링 이벤트 핸들러가 먼저 실행됨!! 마크업이 버블링보다 뒤에 있어도 실행은 캡처링이 우선

### 이벤트 위임- 029.html

- addEventListener를 부모에게 주고, 타겟을 자식으로 하여 이벤트를 실행

```jsx
<article class="parent">
<ol>
<li><button class="btn-first" type="button">버튼1</button></li>
<li><button type="button">버튼2</button></li>
<li><button type="button">버튼3</button></li>
</ol>
</article>

<script>
    const parent = document.querySelector('.parent');
    parent.addEventListener('click', function (event) {
        console.log(event.target); // 이벤트가 발생한 바로 그 요소, 버튼 그 자체
        console.log(event.currentTarget); // 이벤트와 연결된 부모요소
    })
</script>

```

- console.log(event.target) —> ```<li></li>```
    
    이벤트가 발생한 바로 그 요소
    
- console.log(event.currnetTarget) —> ```<article class = “parent”></article>```
    
    이벤트와 연결된 부모요소
    

```jsx
<script>
        const parent = document.querySelector('.parent');
        parent.addEventListener('click', function (event) {
            console.log(event.target); // <li></li>
            //event.target.nodeName을 넣으면 노드네임 확인 가능
            console.log(event.target.nodeName); LI
            if (event.target.nodeName === "BUTTON") {
                event.target.innerText = "버튼4";
            }
        })
    </script>
```

### 이벤트 this

***this는 이벤트가 연결된 노드를 참조***

일반 함수는 ```<article class=”parent”>```를 가르킨다. 이벤트가 연결된 요소 
화살표 함수로 바꾸면 this는 바로 자신의 부모 scope를 참조함

```jsx
<div></div>
    <article class="parent">
        <ol>
            <li><button class="btn-first" type="button">버튼1</button></li>
            <li><button type="button">버튼2</button></li>
            <li><button type="button">버튼3</button></li>
        </ol>
    </article>

    <script>
        const parent = document.querySelector('.parent');
        parent.addEventListener('click', (event) => {
            console.log(this);
        })
        //일반 함수는 parent를 가르킨다. 이벤트가 연결된 요소 
        // 화살표 함수로 바꾸면 this는 바로 자신의 부모 scope를 참조함, 
    </script>
```
![](https://velog.velcdn.com/images/greenth322/post/f7ce4ff4-8925-41a5-a56f-2778aa2cc35f/image.png)

