๐ https://velog.io/@greenth322/DOM-DropDown-%EC%8B%A4%EC%8A%B5

***

## ๐ (๋ด๊ฐ ์์ฑํ)์ ์ฒด ์ฝ๋
```javascript
const contSelect = document.querySelector('.cont-select');
const btnSelect = document.querySelector('.btn-select');
const listMember = document.querySelector('.list-member');
const option = document.querySelectorAll('.opt-member');

// ํ ๊ธ๋ฒํผ์ด ํด๋ฆญ --> ๋ฉ๋ด ๋ณด์ธ๋ค 

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


### ๐ blur์ click์ ์ด์
- blur: focus๊ฐ ํด์ ๋๋ ์๊ฐ์ ์๋ฏธํ๋ค. ์ฆ ์ ์ฝ๋์์๋ btnSelect๊ฐ ์๋ ๋ค๋ฅธ ๊ณณ์ ํด๋ฆญ์ผ๋ก ํฌ์ปค์ค๊ฐ ์ฎ๊ฒจ์ง๋ ์๊ฐ์ ์๋ฏธํ๋ค. ํฌ์ปค์ค๋ document ์ด๋๋ฅผ ํด๋ฆญํ๊ฒ ๋์ด๋ ํด์ ๋๋ค.
- ์ฒ์์๋ mousedown ๋์  click ์ด๋ฒคํธ๋ก ๋ฒํผ์ ๊ฐ์ ์ ๋ฌํ๋๋ก ์์ ์ธ์ ๋ค. ๊ทธ๋ฌ์ ๋๋กญ๋ค์ด ๋ฐ์ ๊ณต๊ฐ์ ํด๋ฆญํ๋ฉด class show๊ฐ ์ฌ๋ผ์ง์ง ์๊ณ  ๋๋กญ๋ค์ด๋ ๋ซํ์ง ์๋๋ค. 
- ์์ธ์ ๋ฐ๋ก ์ด๋ฒคํธ์ ๋ฐ์์์๊ฐ blur > click์ด์ด์ ํ๋ฉด์ ํด๋ฆญํด๋ btnSelect์ ๊ทธ๋๋ก ๋จ์ ์๊ฒ ๋๋ ๊ฒ์ด๋ค.

### ๐ mousedown, mousdeup, click, blur์ ๊ด๊ณ

๋๋๊ฒ๋ ์ด ๋ค ๊ฐ์ ์ด๋ฒคํธ์๋ ๊ด๊ณ๊ฐ ์ฝํ์๋ค. 
1) mousedown + mouseup =  click๊ณผ ๊ฐ๋ค.
2) ์คํ ์ฐ์ ์์: mousedown > blur > mouseup > click

### ๐ ํด๊ฒฐ 

- click ์ด๋ฒคํธ๋ฅผ mousedown์ผ๋ก ๋ณ๊ฒฝํ๋ค.

<br><br>

## ๐ ์ฌํ๋์ ์ฝ๋๋ฆฌ๋ทฐ
1. ๊ฐ์ ์ ๋ฌํ  ๋, ```e.target.textConten```๋ก ์ฌ์ฉํ๋ค๋ฉด, ```textContent```๋ ์ด๋ฒคํธ์ ํ๊ฒ์ ์์์์์ ๋ชจ๋  ๊ฐ์ ๋ถ๋ฌ์จ๋ค. ๊ทธ๋์ ์์ํ  ๋, ์กฐ์ฌํด์ผ ํ๋๋ฐ, ```event.target.nodeName == 'BUTTON'```์ฒ๋ผ ์์ธ์ฒ๋ฆฌ๋ฅผ ํด์ผ ํ๋ค.

2. js๋ก ์ง์  style ์ง์ ํ์ง ๋ง๊ธฐ, ๋์ค์ css๋ก ์คํ์ผ ์ ์ง ๋ณด์๊ฐ ํ๋ค์ด์ง
css ์คํ์ผ์ JS๋ก ๊ณ์ฐํ์ฌ ๋ฃ๋ ๊ฒฝ์ฐ์ ์คํ์ผ ๋ณ๊ฒฝ์ด ์์ ๊ฒฝ์ฐ๋ฅผ ์ ์ธํ๊ณ  style์ ์ฌ์ฉํ์ง ๋ง์. ์ฆ, class๋ฅผ ์์ฑํ๊ณ  ์ง์ฐ๋ ๋ฐฉ๋ฒ์ ์ฌ์ฉํ๋ ๊ฒ์ด ๊ฐ์ฅ ์ข๋ค
 

3. ์ฌํ๋์ด ```creatElement```๋ก JS๋ฅผ ํตํด ์์๋ฅผ ์์ฑํ๋ ์ด์ ๋ ๋์ค์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ ์ฌ์ฉํ  ๋, ์์ ์ด ๋น๋ฒํ๊ฒ ์๊ธธ ์ ์๋ค. ์ด๋ HTML๋ก ์์๋ฅผ ์์ฑํ๋ฉด ๊ณ ์ ๋๊ธฐ ๋๋ฌธ์ ์ ์ง/๋ณด์๊ฐ ์ฉ์ดํ์ง ์๋ค.
 
```javascript
const btn = document.querySelector('.btn-select');
const list = document.querySelector(".list-member");

const arrLang = ['Python','Java','JavaScript','C#','C/C++'];

// ์์ค๋ก ์์๋ฅผ ๋ง๋๋ ์ด์ 
//๋ฐฑ์๋์์ ๋ฐ์ดํฐ๋ฅผ ๋ฐ์์ค๋ฉด(์ง๊ธ์ arrLang ๋ฐฐ์ด) ๋ฐ์ด๋๋ ์์๋ฅผ ์์ ํ  ๋๊ฐ ์๊ธธ ์ผ์ด ๋น๋ฒํ๋ฐ, html๋ก ๋ฐ์๋์ผ๋ฉด staticํด์ ธ์ ๊ด๋ฆฌ๊ฐ ์ด๋ ค์ ์์๋ฅผ JS๋ก ๋ง๋๋ ๊ฒ์.

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
