# console 객체

- 1.log 
```javascript
var a = 1;
var b = 'hello';
var c = true;
console.log(a); // 하나만 로그
console.log(a, b, c); // 여러 개를 동시에 로그
console.log('%d는 숫자 %s는 문자열', a, b); // C 언어처럼 로그
```
- console.log 는 참조를 로깅하기때문에 , 객체처럼 
내용물이 변할 수 있는것들은 실시간으로 변한다.


- 2.dir 
```javascript
function f() { return true; }
console.log(f);
console.dir(f);
```
- dir을 사용하면 해당 객체내의 필드 및 속성들을 알수있다.


- 3.count 
```javascript
console.count('카운터1'); // 카운터1: 1
console.count('카운터1'); // 카운터1: 2
console.count('카운터2'); // 카운터2: 1
console.count('카운터2'); // 카운터2: 2
console.count('카운터1'); // 카운터1: 3
```
- 몇번 호출되었는지 로깅시 사용한다. 인자는 카운터의 이름이다.

- 4.time, timeEnd

```javascript
console.time('타이머');
for (var i = 0; i < 1000000; i++) z = 5;
console.timeEnd('타이머'); // 타이머: 6.76611328125ms
```

코드 수행시간을 확일할때 하다.
인자의 이름은 타이머의 이름이며 , time과 timeEnd에 같은 타이머명을 주어야 
정상작동한다.


