
๐ https://velog.io/@greenth322/Scope-Closure-Class

***

### ๐ ์ ์ญ Scope

- ์คํฌ๋ฆฝํธ ์ด๋๋  ์ ๊ทผ์ด ๊ฐ๋ฅํ๋ค
- ํ์, ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ฌ์ฉ ์ ์ถฉ๋ ๋๋ฌธ์ ์ง์

### ๐ ๋ธ๋ญ Scope

- ์ค๊ดํธ ์์ด ๋ธ๋ญ
- ์ค๊ดํธ ์์์๋ง ์ ๊ทผ ๊ฐ๋ฅ
- ๋ธ๋ก ๋ด๋ถ์์ ์ ์๋ ๋ณ์๋ ๋ธ๋ก ์คํ์ด ๋๋๋ฉด ํด์ 

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

์ค๋ช)
- ๋ธ๋ญ ๋ด๋ถ์์ var๋ก ์ ์ธํ๋ฉด ๋ฐ์์๋ ๊ฐ์ ๋ถ๋ฌ์ฌ ์ ์์
- ๋ธ๋ญ ๋ด๋ถ์์ let์ผ๋ก ์ ์ธํ๋ฉด ๋ฐ์์ ๋ถ๋ฅด๋ฉด ์๋ฌ
- world๋ฅผ ๋ถ๋ฅด๊ณ  ์ถ๋ค๋ฉด
    
    1) let์ var๋ก ๋ฐ๊พธ๊ฑฐ๋, 2) ์์ชฝ์์ ์ฝ์๋ก๊ทธ ์ฐ๊ธฐ
    

### ๐ ํจ์ scope

> ๐ก **scope ์ญํ ** 
1) ์ด๋ฆ ์ถฉ๋ ๋ฌธ์  ํด๊ฒฐ
2) ์๋ ๋ฉ๋ชจ๋ฆฌ ๊ด๋ฆฌ

- ํจ์ ๋ด๋ถ์์ ์ธ๋ถ๋ก ์ ๊ทผ ๊ฐ๋ฅ (ํจ์ ๋ด๋ถ์ ์ ์๋์๋ค๋ฉด, ๊ทธ ์ ์ด๋๋  ์ ๊ทผ ๊ฐ๋ฅ) , ํจ์ ์ธ๋ถ์์ ๋ด๋ถ๋ก ์ ๊ทผ ๋ถ๊ฐ๋ฅ

```jsx
var func1 = function(){
            var a =1;
            var b = 2;
            console.log(a + b);
            // return a + b;
        } // ํจ์๊ฐ ์คํ๋๋ฉด ๋ฉ๋ชจ๋ฆฌ ์ ํจ์๊ฐ ํ๊ดด -> ๋ค ์ฌ๋ผ์ง (์๋ ๋ฉ๋ชจ๋ฆฌ ๊ด๋ฆฌ)
        var a = 20;
        func1(); //3 
        //๋จผ์  ํจ์ ์์์ a๋ฅผ ์ฐพ์๊ณ , ์์ผ๋ฉด ๋ฐ์์ ํ์  
        //์ด๊ฒ ๋ฐ๋ก **์ค์ฝํ์ฒด์ธ**
        //scope: 1) ์ด๋ฆ ์ถฉ๋ ๋ฌธ์  ํด๊ฒฐ 2) ์๋ ๋ฉ๋ชจ๋ฆฌ ๊ด๋ฆฌ
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

- ์์ ์ ์ธํ์ง ์์ผ๋ฉด ๋ฐ์์๋ ์คํ ๊ฐ๋ฅ
- ์์์ ์ ์ธํ๋ฉด ๋ฐ์์ ์คํ ๋ถ๊ฐ๋ฅ(์ ๊ทผ ๋ถ๊ฐ๋ฅํด์)

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

### ๐ Closure(ํด๋ก์ )

- ๋ด๋ถ ํจ์๊ฐ ์ธ๋ถ ํจ์๋ณด๋ค ์ค๋ ์ด์ ์๋ ๊ฒฝ์ฐ์,  ์ธ๋ถํจ์์ ์๋ ๋ณ์๋ค์ ํ๊ดด๋์ง ์๊ณ  ์ด์์ ์คํ๋๋ ๊ฒ์ ์๋ฏธํ๋ค.
- ์ธ๋ถ์์๋ ์ ๊ทผํ  ์ ์๋ ํ์๋ ๊ณต๊ฐ = ๋น๊ณต๊ฐ property

```jsx
var outer = function(){
            var a =1; // ์ธ๋ถ์์๋ ์ ๊ทผํ  ์ ์๋ ํ์๋ ๊ณต๊ฐ = ๋น๊ณต๊ฐ ํ๋กํผํฐ
            // a๋ inner๋ ์ฐ๊ฒฐ๋์ด ์์
            //inner ๊ฐ ๋ฐ์ ๊ณต๊ฐ ์ ๊ธ ๊ถํ์ด ์์!!!
            var inner = function(){
                var b = 6;
                var c = 7;
                a = a + b + c;
                console.log(a);
            }
            return inner;
        }
        var newInner = outer();
        newInner(); // innerํจ์๊ฐ ๋ค์ด๊ฐ ๊ฒฐ๊ตญ 
        //ouer๋ ๋ฆฌํด์ ๋ง๋ ์ฌ๋ผ์ง๊ณ  (์คํ์ด๋์ผ๋๊น), 
        //๊ทธ ํ inner๊ฐ newInner๋ฅผ ๋ง๋ ์คํ๋จ

        console.log(a);//undefinded ์ธ๋ถ์ ๊ทผ
```

**1) ๋ชจ๋ ํจํด**

- ํ๋์ ํจ์ ์์ ๋ชจ๋ ํฌํจ

```jsx
//๋ชจ๋ ํจํด
        function Person() {
            let age = 15;
            // ์๊ธฐ๊ฐ ํด๋ก์  ๊ณต๊ฐ
            // age์ return age๋ ์ฐ๊ฒฐ๋ ์ํ
            return {
                getAge: function () { return age },
                setAge: function (data) { age = data }
            }
        }
        const person = Person(); //new ์๋ ๊ฑฐ ์ฃผ์
        console.log(person.getAge());
        console.log(person.age);//undefinded 
			 //์ด์ ๋? ํจ์ ๋ฐ์์ ํจ์ ๋ด๋ถ์ ์ ์ธ๋ ๊ฐ์ ๋ถ๋ฌ์ฌ ์ X
        person.setAge(40);
        console.log(person.getAge());//40
```

**2) ์ฌ์ฉ์ ์ ์ ํ์ ํจํด**

- ํจ์ + ํ๋กํ ํ์
- ํํ๋ ํจ์ ๋ฐ์ผ๋ก ๋์์์ง๋ง, ๊ฒฐ๊ตญ ํ๋กํ ํ์์ ์ค์ ํด์ค์ผ๋ก์จ PersonTypeํจ์ ์๊ณผ ์ฐ๊ฒฐ๋ ํด๋ก์ ์ ์ผ๋ถ์ด๋ค!!

```jsx
// ์ฌ์ฉ์ ์ ์ ํ์ ํจํด
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
//ํ๋กํ ํ์์ ์จ๊ธฐ์ง ์์์ ๋ง ์ ๊ทผ/๋ณ๊ฒฝ์ด ๊ฐ๋ฅ
```

**3)** **๋ชจ๋ + ์ฌ์ฉ์ ์ ์ ํ์**

- ํจ์ ์์ ํจ์ ํํ
- ํจ์๋ฅผ ์ ์ธ ํ, ํ๋กํ ํ์ ์ถ๊ฐ
- ๊ฐ๊ฒฐ๋ฒ์ : ์คํ ํจ์๋ฅผ ํ๋์ ๋ณ์๋ก ๋ฌถ์ด ์ ์ธ ํ ์ฆ์ ์คํ ํจ์๋ก ์์ฑ

```jsx
//๋ชจ๋ + ์ฌ์ฉ์ ์ ์ ํ์ ํผํฉ ํจํด, ๋น๊ณต๊ฐ ๋ณ์๋ฅผ ํฌํจํ ํ์์ ์์ฑํ  ๋ ์ฌ์ฉ
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
//Person3์ innerPersonType ๋ค์ด๊ฐ
const person3 = new Person3();

console.log(person3.getAge());
person3.age //undfinded ๋ฐ์์ ํจ์ ์์ ๊ฐ์ ๋ถ๋ฌ์ค๋ ค๊ณ  ํ์ผ๋๊น

//person2.getAge()
//15
//person2.setAge(22)
//person2.getAge()
//22
```

```jsx
// ๋ ๊ฐ๋จํ๊ฒ ํํ(์ฆ์ ์คํํจ์๋ก)
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

### ๐ ์ปค์คํ์์ฑํจ์

```jsx
// ์ด์  ๋ฐฐ์ด ์์ฑ์ ํจ์ ํ์
        function Robot(name){
            this.name = name;
        }

        Robot.prototype.sayYourName =  function(){
            console.log(`์๋ฆฌ๋น๋ฆฌ. ์  ์ด๋ฆ์ ${this.name}์๋๋ค. ์ฃผ์ธ๋.`);
        }
        const bot1 = new Robot('์ฌํ');
        console.log(bot1.name);
```

### ๐ class

- ๊ฐ์ ๋ ๋ฌธ๋ฒ์ ์๊ฐ ์ ํ์ค  (Syntactic sugar) - ๋ฌ๋ฌํ๋ค~
- ***constructor๋ new ํค์๋ ์์ฑ ์ ์๋ ์คํ***

```jsx
**//class
        //ํด๋์ค๋ ํจ์๊ฐ ์๋๋ค
        // ํด๋์ค ์์์ ํจ์ function ์๋ต
        class RobotClass{
            //์์ฑ์ํจ์
            constructor(name){
                //์ธ์คํด์ค ๊ฐ๋ฅดํด
                this.name = name;
            }
            sayYourName(){
                console.log(`์๋ฆฌ๋น๋ฆฌ. ์  ์ด๋ฆ์ ${this.name}์๋๋ค. ์ฃผ์ธ๋.`);
            }
        }

        const botclass1 = new RobotClass('๋ธ๋๋ ');
        const botclass2 = new RobotClass('๋ธ๋๋ ');
        console.log(botclass1.sayYourName());

//botclass2.sayYourName() == botclass1.sayYourName() true
// ๊ฐ์ ํจ์๋ฅผ ์ฌ์ฉ**
```

```jsx
//์ค์ต
class MyInfo{
            constructor(name,age,number){
                this.name = name;
                this.age = age;
                this.number =number;
            }
            sayMyNmae(){
                console.log(`hello world...!My name is ${this.name}. I am ${this.age} years old, and my phone number is ${this.number}. Don't contact to me(โฌโ็ฟโ)โฏ`);
            }
        }

        const hello = new MyInfo('๊นํํฌ','26','010-1234-5678');
        console.log(hello.sayMyNmae());
```

**<์์>**

```jsx
class Boss {
            constructor(name) {
                this.name = name;
            }

            sayYourName() {
                console.log(`๋๋ ${this.name}์๋ค!!!!`);
            }
    }

    //extend, super
    //this๋ค์ ๋ค ์ ๊ธฐ๋ค ์ธ์คํด์ค
    class BabyBoss extends Boss{
        constructor(name){
            super(name);
            this.ownName = '์์ดํฌ';
        }

        sayBabyName(){
            this.sayYourName();
            console.log('I am your father');
        }
    }
    

    const baby = new BabyBoss('ํํฌ');

    // baby.sayYourName();
    // 044.html:18 ์๋ฆฌ๋น๋ฆฌ. ์  ์ด๋ฆ์ ํํฌ์๋๋ค. ์ฃผ์ธ๋.
    // undefined
    // baby.name
    // 'ํํฌ'
    // baby.ownName
    // '์์ดํฌ'
```

- ์์(ํ์์์)์์ constructor(์์ฑ์ ํจ์)๋ฅผ ์๋ตํด๋  super ํจ์๊ฐ ์๋์ผ๋ก ํธ์ถ๋์ด ๋ถ๋ชจ class์ ํ๋กํผํฐ๋ฅผ ์์
- **์์ฑ์ ํจ์์์ this ๊ฐ์ ์ฌ์ฉํ  ๊ฒฝ์ฐ super ํจ์๋ ๋ฐ๋์ this ๋ณด๋ค ๋จผ์  ์คํ**
- ํ์ ํด๋์ค๊ฐ ์๋ ํด๋์ค์์ ์ฌ์ฉํ๋ ค๊ณ  ํด๋ ์๋ฌ๊ฐ ๋ฐ์
    
    โ extend ๊ผญ ์ฐ๊ณ  super๋ฅผ ์ฌ์ฉํด์ผ ํ๋ค๋ ์๋ฆฌ์
    

```jsx
//์์ธ์ง ์ค์ต
class Sausage {
        constructor(material1, material2){
            this.material1 = material1;
            this.material2 = material2;
        }

        taste(){
            console.log(`${this.material1}์ ${this.material2}๋ง์ด ๋๋ค!! ๋ฐฐ๊ณ ํ๋ค!`);
        }
    }
    const sausage = new Sausage('์๊ณ ๊ธฐ','ํ');

    class FireSausage extends Sausage{
        constructor(material1){
            super(material1);
            console.log(`${this.material1}์ด ๋๊ธฐ ์์ํฉ๋๋ค!`)
        }
    }

    const firesausage = new FireSausage('๋ถ๋ง');

// ์ฌํ๋ ์ฝ๋
class FireSausage extends Sausage{
    constructor(material1, material2,material3){
            **super(material1,material2); //์์ํด์จ ๊ฐ๋ค**
            this.material2 = material3;
        }
     taste(){
         console.log(`${this.material1}์ ${this.material2}์ ๋ถ๋ง๋ ๋๋ค!! ๋ฐฐ๊ณ ํ๋ค!`);
        }
    }

    const firesausage = new FireSausage('์๊ณ ๊ธฐ','ํ');
```

**๋ด๊ฐ ์ ๋ฆฌํ ์ต์ข ์ฝ๋**

```jsx
class Sausage {
        constructor(material1, material2){
            this.material1 = material1;
            this.material2 = material2;
        }

        taste(){
            console.log(`${this.material1}์ ${this.material2}๋ง์ด ๋๋ค!! ๋ฐฐ๊ณ ํ๋ค!`);
        }
    }
    const sausage = new Sausage('์๊ณ ๊ธฐ','ํ');

    class FireSausage extends Sausage{
        constructor(material1, material2,material3){
            super(material1,material2);
            this.material2 = material3;
        }

        taste(){
            console.log(`${this.material1}์ ${this.material2}์ ${this.material3}๋ ๋๋ค!! ๋ฐฐ๊ณ ํ๋ค!`);
        }
    }

    const firesausage = new FireSausage('์๊ณ ๊ธฐ','ํ','๋ถ๋ง');
```
<br>

### ๐ ๋น๊ณต๊ฐ ํ๋กํผํฐ
**1) getter, setter ๋ฐฉ์(๊ตฌ)**

- ํน๋ณํ ํจ์, ์ธ์ด๊ฐ ์๋๋ผ ๊ทธ๋ฅ ๊ธฐ์ ์ ๋ถ๋ฅด๋ ๋ง๋ก ์ฝ์์ฒ๋ผ ์ฐ์ด๋ ๊ฒ์ด๋ค.
- #password์ฒ๋ผ #์ ๋ถ์ฌ ๋น๊ณต๊ฐ ํ๋กํผํฐ๋ก ๋ง๋ ๋ค
- ์ผ๋ฐ class ํจ์์ ํ๋กํผํฐ์ ์ ๊ทผํ๋ ๋ฐฉ์์ผ๋ก ๊ฐ๋ฉด error๊ฐ ๋จ๋ฉด์, ๊ฐ์ ๋ณด์ฌ์ฃผ์ง ์๋๋ค.
- getPassword๋ฅผ getter๋ผ๊ณ  ๋ถ๋ฅด๋ฉฐ, ๊ฐ์ ๋ถ๋ฌ์ค๋ ์ญํ ์ ํ๋ค.
- getPassword๋ฅผ setter๋ผ๊ณ  ๋ถ๋ฅด๋ฉฐ, ๊ฐ์ ์์ ํ  ๋ ์ฌ์ฉํ๋ค.
- ํ์ง๋ง setPassword ๋ฉ์๋๋ฅผ ์ฌ์ฉํ์ฌ ๊ฐ์ ์์ ํ๊ณ  ๋ฐํํ  ์ ์๋ค.

```jsx
class Robot {
            #password

            constructor(name, pw) {
                this.name = name;
                this.#password = pw;
            }

            sayYourName() {
                console.log(`์๋ฆฌ๋น๋ฆฌ. ์  ์ด๋ฆ์ ${this.name}์๋๋ค. ์ฃผ์ธ๋.`);
            }

            getPassword() {
                return this.#password
            }

            setPassword(pw) {
                this.#password = pw;
            }
        }

        const bot = new Robot('ํํฌ','1234');

//bot.password
//undefined
//bot.#password
//VM226:1 Uncaught SyntaxError: Private field '#password' must be declared in an enclosing class
//bot.setPassword(1234);
// undefined
// bot
// Robotย {name: '์์', #password: 1234}
// bot.getPassword()
// 1234
```

**2) get, set ๋ฐฉ์(์ )**

- ๊ฒํฐ,์ธํฐ์ ๊ฐํธ ๋ฒ์ ์ด ๊ฒ์ โ ์๋ฐ์คํฌ๋ฆฝํธ ์ง์
- ํจ์๋ฅผ ์คํํ์ง ์๊ณ , like ์ผ๋ฐ ํ๋กํผํฐ์ ์ ๊ทผํ๋ ๋ฐฉ๋ฒ๊ณผ ๋๊ฐ์ด ์ฌ์ฉ
- ์ด์ฒ๋ผ ๋๋ฌด ์ฝ๊ฒ ํ๋กํผํฐ ๊ฐ์ ์ ๊ทผํ  ์ ์์ด์ ๋น๊ณต๊ฐ๋ก๋ ๋ถ์ ์ 
- ํ์๊ณผ ์ ์ง๋ณด์์๋ ๋ถ์ ์ . ์๋ํ๋ฉด, ์ ๊ทผ ๋ฐฉ์์ด ์ผ๋ฐ ๊ฐ์ฒด์ ๊ฐ์ ๋ก์ง์ ํ๋จํ๊ธฐ ์ด๋ ต๊ฒ ๋ง๋ค๊ธฐ ๋๋ฌธ์ด๋ค. (์ฃผ์ ํ์)

```jsx
class Robot {
            #password

            constructor(name, pw) {
                this.name = name;
                this.#password = pw;
            }

            sayYourName() {
                console.log(`์๋ฆฌ๋น๋ฆฌ. ์  ์ด๋ฆ์ ${this.name}์๋๋ค. ์ฃผ์ธ๋.`);
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
        // Robotย {name: 'ํํฌ', #password: 123456678}
        // bot.password
        // 123456678

        // ํจ์๋ฅผ ์คํํ์ง ์๊ณ  ๋ง์น ๊ฐ์ฒด์ ์ ๊ทผํ๋ ๋ฐฉ๋ฒ๊ณผ ๋๊น์ด ์ฌ์ฉ
        // ์ ์ง๋ณด์์ ๋ณ๋ก
        }
// get, set์ ๋๋ฌด ๊ฐ๋ณ๊ฒ ์ ๊ทผํ๊ธฐ ๋๋ฌธ์ ๋น๊ณต๊ฐ ํ๋กํผํฐ๋ก ์ ์ X

        const bot = new Robot('ํํฌ','1234');
```