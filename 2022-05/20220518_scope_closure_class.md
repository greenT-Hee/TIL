
🔗 https://velog.io/@greenth322/Scope-Closure-Class

***

### 📌 전역 Scope

- 스크립트 어디든 접근이 가능하다
- 협업, 라이브러리 사용 시 충돌 때문에 지양

### 📌 블럭 Scope

- 중괄호 안이 블럭
- 중괄호 안에서만 접근 가능
- 블록 내부에서 정의된 변수는 블록 실행이 끝나면 해제

```jsx
if(true){
	var value = 'hello';
}
console.log(value) // hello

if(true){
	let value = 'world';
}
console.log(value) // hello

if(true){
	let value = 'world';
    console.log(value);
} //world
```

설명)
- 블럭 내부에서 var로 선언하면 밖에서도 값을 불러올 수 있음
- 블럭 내부에서 let으로 선언하면 밖에서 부르면 에러
- world를 부르고 싶다면
    
    1) let을 var로 바꾸거나, 2) 안쪽에서 콘솔로그 찍기
    

### 📌 함수 scope

> 💡 **scope 역할** 
1) 이름 충돌 문제 해결
2) 자동 메모리 관리

- 함수 내부에서 외부로 접근 가능 (함수 내부에 정의되었다면, 그 안 어디든 접근 가능) , 함수 외부에서 내부로 접근 불가능

```jsx
var func1 = function(){
            var a =1;
            var b = 2;
            console.log(a + b);
            // return a + b;
        } // 함수가 실행되면 메모리 상 함수가 파괴 -> 다 사라짐 (자동 메모리 관리)
        var a = 20;
        func1(); //3 
        //먼저 함수 안에서 a를 찾아고, 없으면 밖에서 탐색  
        //이게 바로 **스코프체인**
        //scope: 1) 이름 충돌 문제 해결 2) 자동 메모리 관리
```

```jsx
var func = function(){
            var a = 1;
            var b = 2; 
            
            var func2 = function(){
                var b  = 5;
                var c = 6;
                a = a + b + c
                console.log(a)
            }
            func2(); 
        }
        func(); //12
```

- 안에 선언하지 않으면 밖에서도 실행 가능
- 안에서 선언하면 밖에서 실행 불가능(접근 불가능해서)

```jsx
function test(){
            val1 = 'hello'
            var val2 = 'world'
        }
        test();
        console.log(val1); //hello
        console.log(val2); //undefined
```
<br>

***

### 📌 Closure(클로저)

- 내부 함수가 외부 함수보다 오래 살아 있는 경우에,  외부함수에 있던 변수들은 파괴되지 않고 살아서 실행되는 것을 의미한다.
- 외부에서는 접근할 수 없는 폐쇄된 공간 = 비공개 property

```jsx
var outer = function(){
            var a =1; // 외부에서는 접근할 수 없는 폐쇄된 공간 = 비공개 프로퍼티
            // a랑 inner는 연결되어 있음
            //inner 가 밖의 공간 전급 권한이 있음!!!
            var inner = function(){
                var b = 6;
                var c = 7;
                a = a + b + c;
                console.log(a);
            }
            return inner;
        }
        var newInner = outer();
        newInner(); // inner함수가 들어감 결국 
        //ouer는 리턴을 만나 사라지고 (실행이됐으니까), 
        //그 후 inner가 newInner를 만나 실행됨

        console.log(a);//undefinded 외부접근
```

**1) 모듈 패턴**

- 하나의 함수 안에 모두 포함

```jsx
//모듈 패턴
        function Person() {
            let age = 15;
            // 요기가 클로저 공간
            // age와 return age랑 연결된 상태
            return {
                getAge: function () { return age },
                setAge: function (data) { age = data }
            }
        }
        const person = Person(); //new 없는 거 주의
        console.log(person.getAge());
        console.log(person.age);//undefinded 
			 //이유는? 함수 밖에서 함수 내부에 선언된 값을 불러올 수 X
        person.setAge(40);
        console.log(person.getAge());//40
```

**2) 사용자 정의 타입 패턴**

- 함수 + 프로토타입
- 형태는 함수 밖으로 나와있지만, 결국 프로토타입을 설정해줌으로써 PersonType함수 안과 연결된 클로저의 일부이다!!

```jsx
// 사용자 정의 타입 패턴
function PersonType(){
	this.age = 35;
}

PersonType.prototype.getAge = function(){
     return this.age;
}

PersonType.prototype.getAge = function(age){
     this.age = age;
}
		

const person2 = new PersonType();
console.log(person2.age);
console.log(person2.getAge()); //35
console.log(person2.setAge(15));
console.log(person2.getAge()); //15
//프로토타입은 숨기지 않아서 막 접근/변경이 가능
```

**3)** **모듈 + 사용자 정의 타입**

- 함수 안의 함수 형태
- 함수를 선언 후, 프로토타입 추가
- 간결버전: 실행 함수를 하나의 변수로 묶어 선언 후 즉시 실행 함수로 작성

```jsx
//모듈 + 사용자 정의 타입 혼합 패턴, 비공개 변수를 포함한 타입을 생성할 떄 사용
function PersonType2(){
	let age = 25;
            
function innerPersonType(){};
innerPersonType.prototype.getAge = function(){
	return age;
}
innerPersonType.prototype.setAge = function(data){
	age = data;
}
 return innerPersonType;
}

 const Person3 = PersonType2(); 
//Person3에 innerPersonType 들어감
const person3 = new Person3();

console.log(person3.getAge());
person3.age //undfinded 밖에서 함수 안의 값을 불러오려고 했으니까

//person2.getAge()
//15
//person2.setAge(22)
//person2.getAge()
//22
```

```jsx
// 더 간단하게 표현(즉시 실행함수로)
        const PersonType3 = (
            function () {
                let age = 15;

                function innerPersonType() { }

                innerPersonType.prototype.getAge = function () {
                    return age;
                }

                return innerPersonType;
            }
        )();

        const personWithSecret = new PersonType3();
        console.log(personWithSecret.getAge());
```

<br>

***

### 📌 커스텀생성함수

```jsx
// 어제 배운 생성자 함수 형식
        function Robot(name){
            this.name = name;
        }

        Robot.prototype.sayYourName =  function(){
            console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
        }
        const bot1 = new Robot('재현');
        console.log(bot1.name);
```

### 📌 class

- 개선된 문법을 슈가 신텍스  (Syntactic sugar) - 달달하다~
- ***constructor는 new 키워드 생성 시 자동 실행***

```jsx
**//class
        //클래스는 함수가 아니다
        // 클래스 안에서 함수 function 생략
        class RobotClass{
            //생성자함수
            constructor(name){
                //인스턴스 가르킴
                this.name = name;
            }
            sayYourName(){
                console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
            }
        }

        const botclass1 = new RobotClass('브랜든');
        const botclass2 = new RobotClass('브랜든');
        console.log(botclass1.sayYourName());

//botclass2.sayYourName() == botclass1.sayYourName() true
// 같은 함수를 사용**
```

```jsx
//실습
class MyInfo{
            constructor(name,age,number){
                this.name = name;
                this.age = age;
                this.number =number;
            }
            sayMyNmae(){
                console.log(`hello world...!My name is ${this.name}. I am ${this.age} years old, and my phone number is ${this.number}. Don't contact to me(╬▔皿▔)╯`);
            }
        }

        const hello = new MyInfo('김태희','26','010-1234-5678');
        console.log(hello.sayMyNmae());
```

**<상속>**

```jsx
class Boss {
            constructor(name) {
                this.name = name;
            }

            sayYourName() {
                console.log(`나는 ${this.name}아다!!!!`);
            }
    }

    //extend, super
    //this들은 다 애기들 인스턴스
    class BabyBoss extends Boss{
        constructor(name){
            super(name);
            this.ownName = '아이크';
        }

        sayBabyName(){
            this.sayYourName();
            console.log('I am your father');
        }
    }
    

    const baby = new BabyBoss('태희');

    // baby.sayYourName();
    // 044.html:18 삐리비리. 제 이름은 태희입니다. 주인님.
    // undefined
    // baby.name
    // '태희'
    // baby.ownName
    // '아이크'
```

- 자식(파생요소)에서 constructor(생성자 함수)를 생략해도  super 함수가 자동으로 호출되어 부모 class의 프로퍼티를 상속
- **생성자 함수에서 this 값을 사용할 경우 super 함수는 반드시 this 보다 먼저 실행**
- 파생 클래스가 아닌 클래스에서 사용하려고 해도 에러가 발생
    
    → extend 꼭 쓰고 super를 사용해야 한다는 소리임
    

```jsx
//소세지 실습
class Sausage {
        constructor(material1, material2){
            this.material1 = material1;
            this.material2 = material2;
        }

        taste(){
            console.log(`${this.material1}와 ${this.material2}맛이 난다!! 배고프다!`);
        }
    }
    const sausage = new Sausage('소고기','파');

    class FireSausage extends Sausage{
        constructor(material1){
            super(material1);
            console.log(`${this.material1}이 나기 시작합니다!`)
        }
    }

    const firesausage = new FireSausage('불맛');

// 재현님 코드
class FireSausage extends Sausage{
    constructor(material1, material2,material3){
            **super(material1,material2); //상속해온 값들**
            this.material2 = material3;
        }
     taste(){
         console.log(`${this.material1}와 ${this.material2}와 불맛도 난다!! 배고프다!`);
        }
    }

    const firesausage = new FireSausage('소고기','파');
```

**내가 정리한 최종 코드**

```jsx
class Sausage {
        constructor(material1, material2){
            this.material1 = material1;
            this.material2 = material2;
        }

        taste(){
            console.log(`${this.material1}와 ${this.material2}맛이 난다!! 배고프다!`);
        }
    }
    const sausage = new Sausage('소고기','파');

    class FireSausage extends Sausage{
        constructor(material1, material2,material3){
            super(material1,material2);
            this.material2 = material3;
        }

        taste(){
            console.log(`${this.material1}와 ${this.material2}와 ${this.material3}도 난다!! 배고프다!`);
        }
    }

    const firesausage = new FireSausage('소고기','파','불맛');
```
<br>

### 📌 비공개 프로퍼티
**1) getter, setter 방식(구)**

- 특별한 함수, 언어가 아니라 그냥 기술을 부르는 말로 약속처럼 쓰이는 것이다.
- #password처럼 #을 붙여 비공개 프로퍼티로 만든다
- 일반 class 함수의 프로퍼티에 접근하는 방식으로 가면 error가 뜨면서, 값을 보여주지 않는다.
- getPassword를 getter라고 부르며, 값을 불러오는 역할을 한다.
- getPassword를 setter라고 부르며, 값을 수정할 때 사용한다.
- 하지만 setPassword 메소드를 사용하여 값을 수정하고 반환할 수 있다.

```jsx
class Robot {
            #password

            constructor(name, pw) {
                this.name = name;
                this.#password = pw;
            }

            sayYourName() {
                console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
            }

            getPassword() {
                return this.#password
            }

            setPassword(pw) {
                this.#password = pw;
            }
        }

        const bot = new Robot('태희','1234');

//bot.password
//undefined
//bot.#password
//VM226:1 Uncaught SyntaxError: Private field '#password' must be declared in an enclosing class
//bot.setPassword(1234);
// undefined
// bot
// Robot {name: '영웅', #password: 1234}
// bot.getPassword()
// 1234
```

**2) get, set 방식(신)**

- 게터,세터의 간편 버전이 겟셋 → 자바스크립트 지원
- 함수를 실행하지 않고, like 일반 프로퍼티에 접근하는 방법과 똑같이 사용
- 이처럼 너무 쉽게 프로퍼티 값에 접근할 수 있어서 비공개로는 부적절
- 협업과 유지보수에도 부적절. 왜냐하면, 접근 방식이 일반 객체와 같아 로직을 판단하기 어렵게 만들기 때문이다. (주석 필요)

```jsx
class Robot {
            #password

            constructor(name, pw) {
                this.name = name;
                this.#password = pw;
            }

            sayYourName() {
                console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
            }
            get password() {
                return this.#password
								//console.log(this.#password)
            }

            set password(pw) {
                this.#password = pw;
            }

        // bot.password
        // '1234'
        // bot.password = 123456678
        // 123456678
        // bot
        // Robot {name: '태희', #password: 123456678}
        // bot.password
        // 123456678

        // 함수를 실행하지 않고 마치 객체에 접근하는 방법과 똑깉이 사용
        // 유지보수에 별로
        }
// get, set은 너무 갑볍게 접근하기 때문에 비공개 프로퍼티로 적절X

        const bot = new Robot('태희','1234');
```