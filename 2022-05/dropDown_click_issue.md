📌 https://velog.io/@greenth322/DOM-DropDown-%EC%8B%A4%EC%8A%B5

***

## 📎 (내가 작성한)전체 코드
```javascript
const contSelect = document.querySelector('.cont-select');
const btnSelect = document.querySelector('.btn-select');
const listMember = document.querySelector('.list-member');
const option = document.querySelectorAll('.opt-member');

// 토글버튼이 클릭 --> 메뉴 보인다 

btnSelect.addEventListener('click', function(){
    listMember.classList.toggle('show');
    btnSelect.classList.toggle('on');
})

btnSelect.addEventListener('blur', function(){
    listMember.classList.remove('show');
    btnSelect.classList.remove('on');
})

option.forEach(function(item){
    item.addEventListener('mousedown',function(e){
        const value = e.currentTarget.textContent;
        btnSelect.textContent = value;
        btnSelect.classList.add('selected-style')

    })
})
```


### 🙋 blur와 click의 이슈
- blur: focus가 해제되는 순간을 의미한다. 즉 위 코드에서는 btnSelect가 아닌 다른 곳에 클릭으로 포커스가 옮겨지는 순간을 의미한다. 포커스는 document 어디를 클릭하게 되어도 해제된다.
- 처음에는 mousedown 대신 click 이벤트로 버튼의 값을 전달하도록 식을 세웠다. 그러자 드롭다운 밖의 공간을 클릭하면 class show가 사라지지 않고 드롭다운도 닫히지 않는다. 
- 원인은 바로 이벤트의 발생순서가 blur > click이어서 화면을 클릭해도 btnSelect에 그대로 남아 있게 되는 것이다.

### 🙋 mousedown, mousdeup, click, blur의 관계

놀랍게도 이 네 개의 이벤트에는 관계가 얽혀있다. 
1) mousedown + mouseup =  click과 같다.
2) 실행 우선순위: mousedown > blur > mouseup > click

### 🙋 해결 

- click 이벤트를 mousedown으로 변경한다.

<br><br>

## 📎 재현님의 코드리뷰
1. 값을 전달할 때, ```e.target.textConten```로 사용했다면, ```textContent```는 이벤트의 타겟의 자식요소의 모든 값을 불러온다. 그래서 위임할 때, 조심해야 하는데, ```event.target.nodeName == 'BUTTON'```처럼 예외처리를 해야 한다.

2. js로 직접 style 지정하지 말기, 나중에 css로 스타일 유지 보수가 힘들어짐
css 스타일을 JS로 계산하여 넣는 경우와 스타일 변경이 없을 경우를 제외하고 style을 사용하지 말자. 즉, class를 생성하고 지우는 방법을 사용하는 것이 가장 좋다
 

3. 재현님이 ```creatElement```로 JS를 통해 요소를 생성하는 이유는 나중에 데이터를 받아서 사용할 떄, 수정이 빈번하게 생길 수 있다. 이때 HTML로 요소를 작성하면 고정되기 때문에 유지/보수가 용이하지 않다.
 
```javascript
const btn = document.querySelector('.btn-select');
const list = document.querySelector(".list-member");

const arrLang = ['Python','Java','JavaScript','C#','C/C++'];

// 자스로 요소를 만드는 이유
//백엔드에서 데이터를 받아오면(지금은 arrLang 배열) 데이나나 요소를 수정할 떄가 생길 일이 빈번한데, html로 박아놓으면 static해져서 관리가 어려워 요소를 JS로 만드는 것임.

arrLang.forEach((item)=> {
    const li = document.createElement('li');
    const btn = document.createElement('button');

    btn.setAttribute('type','button');
    //<button type = "button"></button>
    btn.textContent = item;
    // btn.classList.add('') = btn.setAttribute('class','');
    li.appendChild(btn);
    list.appendChild(li);
});

btn.addEventListener('click', () => {
    btn.classList.toggle('on');
});

list.addEventListener('click', (event) => {
    if (event.target.nodeName === 'BUTTON') {
        btn.textContent = event.target.textContent;
        btn.classList.remove('on');
    }
});
```
