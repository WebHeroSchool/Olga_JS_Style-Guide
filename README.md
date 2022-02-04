<h2 id='link'>10 правил читабельного и правильного кода JS</h2>

+ [первое](#Первое)
+ [второе](#Второе)
+ [третье](#Третье)
+ [четвертое](#Четвертое)
+ [пятое](#Пятое)
+ [шестое](#Шестое)
+ [седьмое](#Седьмое)
+ [восьмое](#Восьмое)
+ [девятое](#Девятое)
+ [десятое](#Десятое)
***
<h4 id='Первое'>Первое правило</h4>

###### Не объявляй функцию внутри цикла.
:x: ***~~плохая практика~~***
``` js
for (let i=10; i; i--) {
  (function() { return i; })();
}

while(i) {
  const a = function() { return i; };
  a();
}
``` 
:heavy_check_mark: ***хорошая практика***
``` js
const a = function() {};

for (let i=10; i; i--) {
  a();
}
``` 
&nbsp;
<h4 id='Второе'>Второе правило</h4>

###### Не используй `argument` для получения аргументов, вместо этого используй `rest` оператор.
:x: ***~~плохая практика~~***
``` js
function foo() {
  console.log(arguments);
}

function foo(action) {
  const args = Array.prototype.slice.call(arguments, 1);
  action.apply(null, args);
}

function foo(action) {
  const args = [].slice.call(arguments, 1);
  action.apply(null, args);
}
``` 
:heavy_check_mark: ***хорошая практика***
``` js
function foo(...args) {
    console.log(args);
}

function foo(action, ...args) {
    action.apply(null, args); 
}
``` 
&nbsp;
<h4 id='Третье'>Третье правило</h4>

###### Всегда ставь один пробел перед `()` и перед `{}` в функциях.
:x: ***~~плохая практика~~***
``` js
const f = function(){};
const g = function (){};
const h = function() {};
``` 
:heavy_check_mark: ***хорошая практика***
``` js
const x = function () {};
const y = function a() {};
``` 
&nbsp;
<h4 id='Четвертое'>Четвертое правило</h4>

###### Называй функции-конструкторы с большой буквы.
:x: ***~~плохая практика~~***
``` js
const colleague = new person();
const friend = new person.acquaintance();
``` 
:heavy_check_mark: ***хорошая практика***
``` js
const colleague = new Person();
const friend = new person.Acquaintance();
``` 
&nbsp;
<h4 id='Пятое'>Пятое правило</h4>

###### Не пиши пустой конструктор в классах. Классы имеют конструктор по умолчанию.
:x: ***~~плохая практика~~***
``` js
class Jedi {
  constructor() {}

  getName() {
    return this.name;
  }
}


class Rey extends Jedi {
  constructor(...args) {
    super(...args);
  }
}
``` 
:heavy_check_mark: ***хорошая практика***
``` js
class Rey extends Jedi {
  constructor(...args) {
    super(...args);
    this.name = 'Rey';
  }
}
``` 
&nbsp;
<h4 id='Шестое'>Шестое правило</h4>

###### Используй один импорт на модуль, не дублируй импорты.
:x: ***~~плохая практика~~***
``` js
import foo from 'foo';
// … другие import-ы … //
import { named1, named2 } from 'foo';
``` 
:heavy_check_mark: ***хорошая практика***
``` js
import foo, { named1, named2 } from 'foo';
// или так:
import foo, {
  named1,
  named2,
} from 'foo';
``` 
&nbsp;
<h4 id='Седьмое'>Седьмое правило</h4>

###### При использовании генераторов ставь один пробел перед `*` , но не ставь пробел после `*` .
:x: ***~~плохая практика~~***
``` js
function * generator() {}
let anonymous = function * () {};
let shorthand = {* generator() {} };
``` 
:heavy_check_mark: ***хорошая практика***
``` js
function *generator() {}
let anonymous = function *() {};
let shorthand = { *generator() {} };
``` 
&nbsp;
<h4 id='Восьмое'>Восьмое правило</h4>

###### Используйте фигурные скобки для создания блоков в `case` и `default` в конструкции `switch...case` , которые содержат лексические объявления (например: `let`, `const`, `function` и `class`).
*Лексические объявления видны во всем блоке `switch`, но инициализируются только при срабатывании определенного `case`. Чтобы убедиться, что лексическое объявление применяется только к текущему `case`, необходимо использовать скобки.*
:x: ***~~плохая практика~~***
``` js
switch (foo) {
  case 1:
    let x = 1;
    break;
  case 2:
    const y = 2;
    break;
  case 3:
    function f() {
      // ...
    }
    break;
  default:
    class C {}
}
``` 
:heavy_check_mark: ***хорошая практика***
``` js
switch (foo) {
  case 1: {
    let x = 1;
    break;
  }
  case 2: {
    const y = 2;
    break;
  }
  case 3: {
    function f() {
      // ...
    }
    break;
  }
  case 4:
    bar();
    break;
  default: {
    class C {}
  }
}
``` 
&nbsp;
<h4 id='Девятое'>Девятое правило</h4>

###### При смешивании операторов заключай их в скобки. Единственным исключением являются стандартные арифметические операторы: `+`, `-` и `**`, так как их приоритет широко понят. Рекомендуется заключать в скобки `/` и `*`, потому что их приоритет может быть неоднозначным, когда они смешаны. Это позволит избежать ошибок. Также код станет более читабельным
:x: ***~~плохая практика~~***
``` js
const foo = a && b < 0 || c > 0 || d + 1 === 0;
const bar = a ** b - 5 % d;

if (a || b && c) {
  return d;
}

const bar = a + b / c * d;
``` 
:heavy_check_mark: ***хорошая практика***
``` js
const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

const bar = a ** b - (5 % d);

if (a || (b && c)) {
  return d;
}

const bar = a + (b / c) * d;
``` 
&nbsp;
<h4 id='Десятое'>Десятое правило</h4>

###### Ставь один пробел после открывающей фигурной скобки и перед закрывающей в теле функций, условий если они написаны в строку.
:x: ***~~плохая практика~~***
``` js
function foo() {return true;}
if (foo) { bar = 0;}
``` 
:heavy_check_mark: ***хорошая практика***
``` js
function foo() { return true; }
if (foo) { bar = 0; }
``` 
[Вернуться наверх](#link)
