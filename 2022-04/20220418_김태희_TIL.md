👉 velog:  https://bit.ly/3tRm4Ce
# login 화면 구현
 ## 📘 재현님과의 코드 리뷰 정리!

<img src="https://velog.velcdn.com/images/greenth322/post/361dca2c-383d-456c-9a48-92422d152582/image.PNG">

### 📌 로그인1.html/css
#### 1. 레이아웃은 position을 사용하지 않는다! 왜? 요소가 추가 되면 디자인이 망가지거나 밀려나는 등 다른 normal-flow 요소드ㅡㄹ과 겹침 현상이 일어날 수 있다 
#### 2. padding으로 요소들의 크기를 지정하면 좋다. <br> 소속된 요소들의 크기가 변하거나 추가되어도 유연하게 유지보수가 가능하기 때문이다. <br> 단!! ```<a>``` 태그의 크기를 조정할 때 padding은 주의해야 한다. 다른 곳까지 클릭이 될 수 있기 때문이다.
#### 3. button은 inline!! --> 버튼 중앙 정렬 시, display:block; + margin: 0 auto; 
#### 4. cusor: pointer 설정은 사용자 편리를 위함
#### 5. 열린 태그는 가상 태그를 사용할 수 없다!! 가상태그는 꼭 닫힌 태그와 쓰는 것 잊지 않기!
#### 6.  <span style="background-color:#4cfc8d">[float]</span><br> - 가상 요소는 기본적으로 inline 요소라서 너비/높이 지정이 불가함 > 하지만, float 설정을 하게 되면 inline-block으로 바뀌어 높이/너비 지정이 가능해진다. <br> - float을 사용했을 경우는 margin으로 조정(float은 inline-block이니까) <br> - float을 부모에게도 주면, 자식들이 다 float이어도 자식을 알아본다.
***
<img src="https://velog.velcdn.com/images/greenth322/post/c45a36f1-fe3d-4b13-9bea-949d3134e66e/image.PNG" width="450">

<img src="https://velog.velcdn.com/images/greenth322/post/45fcf5fa-5973-4bd5-89cf-173d853b41a4/image.PNG" width="450">

### 📌 로그인2.html/css

#### 1. ```<img>```에는 꼭 alt값을 주어 자세하게 시각장애인들도 이해할 수 있도록 웹접근성을 지켜주자<br> ex) 닫기 버튼: close X, 로그인 창 닫기 O
#### 2. close 닫기 버튼을 position을 주는 이유: 스크린리더가 가장 나중에 읽도록! 모달 맨 위에서 제목 다음으로 바로 닫기가 읽히면 시각장애인분들이 당황할 수 있다. html에서도 가장 마지막 식에 작성한다.
####  3. height은고정값으로 지정하지 말자.  레이아웃이든 디자인 요소이든<br>(특히 p태그와 같은 텍스트 요소는 line-heigt 등으로 조정하는 것 지양)
####  4. 재활용할 디자인의 변경사항은 따로 css를 분리해서 작성하기
####  5. <span style="color:blue">input은 항상 label을 사용하고, 숨길 시 hidden으로 설정한다!!! </span>  
  
#### 6. margin은 축약형으로 사용하려고 노력(코딩 간결하게)
#### 7. position으로 요소 자리 잡는 거 제발 그만! 😱
#### 8. border: 크기 설정에 따라 요소를 미뤄냄 <br> outline: 다른 요소를 미뤄내지 않음 <br> outline-offset: input과 박스의 사이 거리
#### 9. 의미 없는 선 정도는 회원가입 I 아이디/비번찾기 html 특수 문자를 써도 웹 표준에 문제는 되지 않는다.
#### 10. section 꼭 안에 h2 또는 h3을 써서 제목을 달아줘서 영역을 확실하게 구분하고, 눈에 보일 필요가 없다면 display: hidden으로 가리기
***
### 🍒 모듈용 html, css를 만들어 사용하기(보다 효율적, 고평가)   
####  - 개인 작업: 모듈식 작성 --> 레이아웃 잡고 디자인 구현<br> - 팀 단위 작업: 리더가 모듈 작성하고, 나머지 팀원들은 각자의 할당량 작성하고, 추후 모듈을 받으면 활용하여 디자인 구현 완성하기

### 🍒 모듈 html/css를 구현한 결과이다. 
#### 너비는 100% 또는 100vw로, height은 아무런 설정 없이 작성한다. 다른 곳에 복사하여 넣을 때, 유연하게 크기를 조정해야 하기 때문이다.

> <img src="https://velog.velcdn.com/images/greenth322/post/a8b9137d-1488-47fe-b690-0576f2e4f1a1/image.png" width="950">

