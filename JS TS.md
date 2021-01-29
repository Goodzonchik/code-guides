# JS/TS

Объявление переменных и правила именования:

#### 1. Используйте `const` и `let` вместо `var`.

**eslint: prefer-const, no-const-assign, no-var**

#### 2. Использовуйте оператор `spread` при поверхностном копировании объектов и массивов, а не `Object.assing`.

```ts
// очень плохо
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 });

// плохо
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 });

// хорошо
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 };

// хорошо
const itemsCopy = [...items];
```

#### 3. Используйте литеральную нотацию для создания массива .

**eslint: no-array-constructor**

```ts
// плохо
const items = new Array();

// хорошо
const items = [];
```

#### 4. Избегайте названий из одной буквы. Имя должно быть наглядным.

**eslint: id-length**

#### 5. Используйте `camelCase` для именования объектов, функций и экземпляров.

**eslint: camelcase**

#### 6. Используйте `PascalCase` только для именования конструкторов и классов.

**eslint: new-cap**

#### 7. Используйте верхний регистр для сокращений и буквенных аббревиатур.

**Почему?** Имена предназначены для удобства чтения.

```ts
// плохо
import SmsContainer from './containers/SmsContainer';
// плохо
const HttpRequests;
// хорошо
import SMSContainer from './containers/SMSContainer';
const httpRequests;
```

#### 8. Не используйте `_` в начале или в конце названий.

**eslint: no-underscore-dangle**

#### 9. Используйте одинарные кавычки в коде.

**eslint: quotes**

#### 10. Используйте шаблонные строки вместо конкатенации при создании строки программным путём .

**eslint: prefer-template template-curly-spacing**

```ts
// плохо
var x = 'How are you, ' + name + '?';

// хорошо
var x = `How are you, ${name}?`;
```

#### 11. Никогда не используйте `eval()`, т.к. это открывает множество уязвимостей.

**eslint: no-eval**

#### 12. Не используйте в строках необязательные экранирующие символы.

**eslint: no-useless-escape**

**Почему?** Обратные слеши ухудшают читабельность, поэтому они должны быть только при необходимости.

```ts
// плохо
const foo = '/\'this/\' is "quoted"';

// хорошо
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`;
```

#### 13. Используйте `===` и `!==` вместо `==` и `!=`.

**eslint: eqeqeq**

#### 14. Применяйте сокращение для булевых типов.

```ts
// плохо
if (isValid === true) {}

// хорошо
if (isValid) {}
```

#### 15. Применяйте явное сравнение для строк и чисел.

```ts
// плохо
if (name) {}
if (collection.length) {}


// хорошо
if (name !== '') {}
if (collection.length > 0){}
```

#### 16. Пишите в конце каждой строки точку с запятой.

**eslint: semi**

#### 17. Добавляйте висячие запятые.

**eslint: comma-dangle**

**Почему?** Такой подход даёт понятную разницу при просмотре изменений. Кроме того, транспиляторы типа `Babel` удалят висячие запятые из собранного кода, поэтому вы можете не беспокоиться о проблемах в старых браузерах.

```ts
// плохо
const hero = {
  firstName: 'Dana',
  lastName: 'Scully'
};

// хорошо
const hero = {
  firstName: 'Dana',
  lastName: 'Scully',
};

//(обратите внимание, что висячей запятой не должно быть после rest-аргумента)
createHero(inventorOf, ...heroArgs);
```

#### 18. Не начинайте строку с запятой.

**eslint: comma-style**

```ts
// плохо
const story = [
                once
                , upon
              ];

// хорошо
const story = [
                once,
                upon,
              ];
```

#### 19. Всегда используйте модули (`import`/`export`) вместо нестандартных модульных систем. Вы всегда сможете транспилировать код в вашу любимую модульную систему.

#### 20. Не используйте импорт через `_`.

**Почему?** Это гарантирует, что у вас есть единственный экспорт по умолчанию.

```ts
// плохо
import _ as AirbnbStyleGuide from './AirbnbStyleGuide';

// хорошо
import AirbnbStyleGuide from './AirbnbStyleGuide';
```

#### 21. Импортируйте из пути только один раз.

**eslint: no-duplicate-imports**

**Почему?** Наличие нескольких строк, которые импортируют из одного и того же файла, может сделать код неподдерживаемым.

```ts
// плохо
import foo from 'foo';
import { named } from 'foo';

// хорошо
import foo, { named1, named2 } from 'foo';
```

#### 22. Не экспортируйте изменяемые переменные.

**eslint: import/no-mutable-exports**

**Почему?** Вообще, следует избегать мутации, в особенности при экспорте изменяемых переменных. Несмотря на то, что эта техника может быть необходима в редких случаях, в основном только константа должна быть экспортирована.

```ts
// плохо
let foo = 3;
export { foo };

// хорошо
const foo = 3;
export { foo };
```

#### 23. Используйте экспорт по умолчанию в модулях с единственным экспортом, а не экспорт по имени.

**eslint: import/prefer-default-export**

**Почему?** Для того чтобы поощрять создание множества файлов, которые бы экспортировали одну сущность, т.к. это лучше для читабельности и поддержки кода.

```ts
// плохо
export function foo() {}

// хорошо
export default function foo() {}
```

#### 24. Поместите все импорты выше остальных инструкций.

**eslint: import/first**

**Почему?** Так как `import` обладает подъёмом, то хранение их всех в начале файла предотвращает от неожиданного поведения.

#### 25. Делайте отступы у импортов на нескольких строках, как у многострочных литералов массива и объекта.

**Почему?** Фигурные скобки следуют тем же правилам отступа как и любая другая фигурная скобка блока в этом руководстве, тоже самое касается висячих запятых.

```ts
// плохо
import { longNameA, longNameB, longNameC, longNameD, longNameE } from 'path';

// хорошо
import {
          longNameA,
          longNameB,
          longNameC,
          longNameD,
          longNameE
        } from 'path';
```

#### 26. Используйте конструкцию /*_ ... _*/ для многострочных комментариев.

```ts
// плохо
// make() возвращает новый элемент
// соответствующий переданному названию тега
//

// хорошо
/*
- make() возвращает новый элемент
- соответствующий переданному названию тега
*/
```

#### 27. Используйте двойной слеш // для однострочных комментариев. 

Располагайте такие комментарии отдельной строкой над кодом, который хотите пояснить. Если комментарий не является первой строкой блока, добавьте сверху пустую строку.

```ts
// плохо
const active = true; // это текущая вкладка

// хорошо
// это текущая вкладка
const active = true;

// хорошо
function getType() {
  console.log('fetching type...');

  // установить по умолчанию тип 'no type'
  const type = this.type || 'no type';

  return type;
}
```

#### 28. Начинайте все комментарии с пробела, так их проще читать.

**eslint: spaced-comment**

```ts
// плохо
//это текущая вкладка

// хорошо
// это текущая вкладка

/*
  make() возвращает новый элемент
 */
```

#### 29. Помечайте технический долг комментариями `FIXME` или `TODO`.

Если известен номер задачи, в которой планируется исправление, то стоит указать и его. Или указать номер задачи, в рамках которой был добавлен комментарий.

#### 30. Используйте объявление `const` или `let` для каждой переменной или присвоения.

**eslint: one-var**

```ts
// плохо
const items = getItems(),
  goSportsTeam = true;

// хорошо
const items = getItems();
const goSportsTeam = true;
```

#### 31. Группируйте в первую очередь `const`, а затем `let`.

**Почему?** Это полезно, когда в будущем вам понадобится создать переменную, зависимую от предыдущих.

```ts
// плохо
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;

// хорошо
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
```

#### 32. Создавайте переменные там, где они вам необходимы, но помещайте их в подходящее место.

#### 33. Не создавайте цепочки присваивания переменных.

**eslint: no-multi-assign**

```ts
// плохо
let a = (b = c = 1);

let a = 1;
let b = a;
let c = a;
```

#### 34. В присвоении избегайте разрывов строк до и после =. Если ваше присвоение нарушает правило `max-len`, оберните значение в круглые скобки.

**eslint operator-linebreak**

**Почему?** Разрывы строк до и после = могут приводить к путанице в понимании значения.

```ts
// плохо
const foo = 
          superLongLongLongLongLongLongLongLongFunctionName();

// хорошо
const foo = superLongLongLongLongLongLongLongLongFunctionName();

// хорошо
const foo = 'superLongLongLongLongLongLongLongLongString';
```

#### 35. Запретите неиспользуемые переменные.

**eslint: no-unused-vars**

**Почему?** Переменные, которые объявлены и не используются в коде, скорее всего, являются ошибкой из-за незавершённого рефакторинга. Такие переменные занимают место в коде и могут привести к путанице при чтении.

#### 36. Избегайте, по возможности, `get()` и `set()` для полей класса.

**Почему?** могут возникнуть проблемы с тестированием, пониманием логики и поддержкой. Исключение – создание компонента с `ControlValueAccessor` или `getter` для `FormControl`

#### 37. Используйте `Number.isNaN` и `Number.isFinite` вместо `isNaN` и `isFinite`.

**Почему?** Глобальная функция `isNaN` приводит не-числа к числам, возвращая `true` для всего, что приводится к `NaN`. Если такое поведение необходимо, сделайте его явным.

#### 38. Перемещайте на новыую строку условия, если ваш управляющий оператор (`if`, `while` и т.д.) слишком длинный или превышает максимальную длину строки.

**Почему?** Наличие операторов в начале строки приводит к выравниванию операторов и напоминает цепочку методов. Это также улучшает читаемость, упрощая визуальное отслеживание сложной логики.

```ts
// плохо
if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
  thing1();
}

// хорошо
if (
  (foo === 123 || bar === 'abc') &&
  doesItLookGoodWhenItBecomesThatLong() &&
  isThisReallyHappening()
) {
  thing1();
}
```

#### 39. Ставьте 1 пробел перед открывающей фигурной скобкой у блока.

**eslint: space-before-blocks**

```ts
// плохо
function test(){
  console.log('test');
}
// хорошо
function test() {
  console.log('test');
}
```

#### 40. Ставьте 1 пробел перед открывающей круглой скобкой в операторах управления (`if`, `while` и т.п.). Не оставляйте пробелов между списком аргументов и названием в объявлениях и вызовах функций.

**eslint: keyword-spacing**

```ts
// плохо
if(isJedi) {
}

// хорошо
if (isJedi) {
}
```

#### 41. Разделяйте операторы пробелами.

**eslint: space-infix-ops**

```ts
// плохо
const x = y+5;

// хорошо
const x = y + 5;
```

#### 42. В конце файла оставляйте одну пустую строку.

**eslint: eol-last**

#### 43. Используйте переносы строк и отступы, когда делаете длинные цепочки методов (больше 2 методов). Ставьте точку в начале строки, чтобы дать понять, что это не новая инструкция, а продолжение цепочки.

**eslint: newline-per-chained-call no-whitespace-before-property**

```ts
// плохо
$('#items').find('.selected').highlight().end().find('.open').updateCount();

// хорошо
$('#items')
    .find('.selected')
    .highlight();
```

#### 44. Оставляйте пустую строку между блоком кода и следующей инструкцией.

```ts
// плохо
if (foo) {
  return bar;
}
return baz;

// хорошо
if (foo) {
  return bar;
}

return baz;
```

#### 45. Не добавляйте отступы до или после кода внутри блока.

**eslint: padded-blocks**

```ts
// плохо
function bar() {

  console.log(foo);

}
// хорошо
function bar() {
  console.log(foo);
}
```

#### 46. Не используйте множество пустых строк для заполнения кода.

**eslint: no-multiple-empty-lines**

#### 47. Не добавляйте пробелы между круглыми скобками и их содержимым.

**eslint: space-in-parens**

```ts
// плохо
function bar( foo ) {}

// хорошо
function bar(foo) {}
```

#### 48. Не добавляйте пробелы между квадратными скобками и их содержимым.

**eslint: array-bracket-spacing**

```ts
// плохо
[ 1, 2, 3] ;
// хорошо
[1, 2, 3];
```

#### 49. Добавляйте пробелы между фигурными скобками и их содержимым.

**eslint: object-curly-spacing**

```ts
// плохо
const foo = { clark: 'kent' };

// хорошо
const foo = {clark: 'kent'};
```

#### 50. Старайтесь не допускать, чтобы строки были длиннее 120 символов. Замечание: длинные строки с текстом освобождаются от этого правила и не должны разбиваться на несколько строк.

**eslint: max-len**

**Почему?** Это обеспечивает удобство чтения и поддержки кода.

#### 51. Должно быть согласованное расстояние между открывающим символом блока и следующим символом на одной и той же строке. Тоже самое касается расстояния между закрывающим символом блока и предыдущим символом.

**eslint: block-spacing**

```ts
// плохо
function foo() {
return true;
}
if (foo) {
bar = 0;
}

// хорошо
function foo() {
  return true;
}

if (foo) {
  bar = 0;
}
```

#### 52. Избегайте пробелов перед запятыми и ставьте его после.

**eslint: comma-spacing**

```ts
// плохо
var foo = 1 ,
  bar = 2;
var arr = [1 ,2];

// хорошо
var foo = 1,
  bar = 2;
var arr = [1, 2];
```

#### 53. Избегайте пробелов внутри скобок вычисляемого свойства.

**eslint: computed-property-spacing**

```ts
// плохо
obj[ foo ];
obj[ 'foo' ];

// хорошо
obj[foo];
obj['foo'];
```

#### 54. Избегайте пробелов между функциями и их вызовами.

**eslint: func-call-spacing**

```ts
// плохо
func ();

// хорошо
func();
```

#### 55. Избегайте пробелов в конце строки.

**eslint: no-trailing-spaces**

#### 56. Используйте фигурные скобки, когда блок кода занимает несколько строк.

**eslint: nonblock-statement-body-position**

```ts
// плохо
if (test)
    return false;

// плохо
function foo() {return false;}

// хорошо
if (test) return false;

// хорошо
if (test) {
  return false;
}

// хорошо
function bar() {
  return false;
}
```

#### 57. расположите оператор `else` на той же строчке, где находится закрывающая фигурная скобка блока `if`, если блоки кода в условии `if` и `else` занимают несколько строк.

**eslint: brace-style**

```ts
// плохо
if (test) {
}
else {
}

// хорошо
if (test) {
} else {
}
```

#### 58. Не пишите блок `else`, если в блоке `if` всегда выполняется оператор `return`.

**eslint: no-else-return**

```ts
// плохо
function foo() {
  if (x) {
    return x;
  } else {
    return y;
  }
}

// хорошо
function foo() {
  if (x) {
    return x;
  }

  return y;
}

// хорошо
function cats() {
  if (x) {
    return x;
  }

  if (y) {
    return y;
  }
}
```

#### 59. Никогда не объявляйте функции в нефункциональном блоке (`if`, `while`, и т.д.). Вместо этого присвойте функцию переменной.

**eslint: no-loop-func**

#### 60. Никогда не называйте параметр arguments. Он будет иметь приоритет над объектом `arguments`, который доступен для каждой функции.

```ts
// плохо
function foo(name, options, arguments) {}

// хорошо
function foo(name, options, args) {}
```

#### 61. Не используйте `arguments`, вместо этого используйте синтаксис оставшихся параметров `...`.

**eslint: prefer-rest-params**

**Почему?** `...` явно говорит о том, какие именно аргументы вы хотите извлечь. Кроме того, такой синтаксис создаёт настоящий массив, а не массивоподобный объект как arguments.

```ts
// плохо
function concatenateAll() {}

// хорошо
function concatenateAll(...args) {}
```

#### 62. Используйте синтаксис записи аргументов по умолчанию, а не изменяйте аргументы функции.

```ts
// очень плохо
function handleThings(opts) {
  opts = opts || {};
}

// хорошо
function handleThings(opts = {}) {
  // ...
}
```

#### 63. Всегда вставляйте последними параметры по умолчанию.

```ts
// плохо
function handleThings(opts = {}, name) {}

// хорошо
function handleThings(name, opts = {}) {}
```

#### 64. Никогда не изменяйте параметры.

**eslint: no-param-reassign**

#### 65. Отдавайте предпочтение использованию оператора расширения `...` при вызове вариативной функции.

**eslint: prefer-spread**

**Почему?** Это чище, вам не нужно предоставлять контекст, и не так просто составить `new` с `apply()`.

```ts
// плохо
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

// хорошо
const x = [1, 2, 3, 4, 5];
console.log(...x);

// хорошо
new Date(...[2016, 8, 5]);
```

#### 66. Используйте фигурные скобки для `case` и `default`, если они содержат лексические декларации (например, let, const, function, и class).

**eslint: no-case-declarations.**

```ts
// плохо
switch (foo) {
  case 1:
    let x = 1;
    break;
  case 2:
}

// хорошо
switch (foo) {
  case 1: {
    let x = 1;
    break;
  }
  case 2: {
    const y = 2;
    break;
  }
}
```

#### 67. Не указывайте тернарный оператор внутри другого.

**eslint: no-nested-ternary.**

```ts
// плохо
const foo = maybe1 > maybe2 ? 'bar' : value1 > value2 ? 'baz' : null;

// хорошо
const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
```

#### 68. Избегайте ненужных тернарных операторов.

**eslint: no-unneeded-ternary.**

```ts
// плохо
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;

// хорошо
const foo = a || b;
const bar = !!c;
const baz = !c;
```

#### 69. Используйте точечную нотацию для доступа к свойствам.

**eslint: dot-notation**

```ts
// плохо
const isJedi = luke['jedi'];

// хорошо
const isJedi = luke.jedi;
```

#### 70. Используйте `extends` для наследования.

**Почему?** Это встроенный способ наследовать функциональность прототипа, не нарушая `instanceof`.

#### 71. Методы могут возвращать this, чтобы делать цепочки вызовов.

```ts
// плохо
Jedi.prototype.jump = function () {
  this.jumping = true;
  return true;
};

Jedi.prototype.setHeight = function (height) {
  this.height = height;
};

const luke = new Jedi();
luke.jump();
luke.setHeight(20);

// хорошо
class Jedi {
  jump() {
    this.jumping = true;
    return this;
  }

  setHeight(height) {
    this.height = height;
    return this;
  }
}

const luke = new Jedi();
luke.jump().setHeight(20);
```

#### 72. Опустите конструктор по умолчанию, если он не задан явно.

**eslint: no-useless-constructor**

#### 73. Избегайте дублирующих членов класса.

**eslint: no-dupe-class-members**

**Почему?** Если объявление члена класса повторяется, без предупреждения будет использовано последнее. Наличие дубликатов скорее всего приведёт к ошибке.

#### 74. Используйте операторы `return` внутри функций обратного вызова в методах массива.

Можно опустить `return`, когда тело функции состоит из одной инструкции, возвращающей выражение без побочных эффектов.

**eslint: array-callback-return**

```ts
// плохо
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
const flatten = acc.concat(item);
});

// хорошо
[1, 2, 3].map((x) => {
const y = x + 1;
return x \* y;
});

// хорошо
[1, 2, 3].map((x) => x + 1);
```

#### 75. Используйте разрывы строк после открытия и перед закрытием скобок, если массив располагается на нескольких строках.

```ts
// плохо
const arr = [[0, 1],[2, 3],[4, 5],];

// хорошо
const arr = [
  [0, 1],
  [2, 3],
  [4, 5],
];

const objectInArray = [
  {
    id: 1,
  },
  {
    id: 2,
  },
];
```

#### 76. Используйте деструктуризацию объекта при обращении к нескольким свойствам объекта.

**eslint: prefer-destructuring**

**Почему?** Деструктуризация избавляет вас от создания временных переменных для этих свойств.

```ts
// плохо
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// хорошо
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

#### 77. Используйте деструктуризацию массивов.

**eslint: prefer-destructuring**

```ts
const arr = [1, 2, 3, 4];

// плохо
const first = arr[0];
const second = arr[1];

// хорошо
const [first, second] = arr;
```

#### 78. Используйте стрелочную функцию, когда нужно использовать анонимную функцию.

**eslint: prefer-arrow-callback, arrow-spacing**

**Почему?** Таким образом создаётся функция, которая выполняется в контексте `this`, который мы обычно хотим, а также это более короткий синтаксис.

```ts
// плохо
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x \* y;
});

// хорошо
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x \* y;
});
```

#### 79. Опустите фигурные скобки и используйте неявное возвращение, если тело функции состоит из одного оператора, возвращающего выражение без побочных эффектов.

В противном случае, сохраните фигурные скобки и используйте оператор `return`.

**eslint: arrow-parens, arrow-body-style**

**Почему?** Синтаксический сахар. Когда несколько функций соединены вместе, то это лучше читается.

```ts
// плохо
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

foo(() => (bool = true));

// хорошо
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  return `A string containing the ${nextNumber}.`;
});
```

#### 80. Всегда оборачивайте аргументы круглыми скобками для ясности и согласованности.

**eslint: arrow-parens**

**Почему?** Минимизирует различия при удалении или добавлении аргументы.

```ts
// плохо
[1, 2, 3].map((x) => x * x);

// хорошо
[1, 2, 3].map((x) => x * x);
```

#### 81. Не используйте итераторы.

Применяйте функции высшего порядка вместо таких циклов как `for-in` или `for-of`.

**eslint: no-iterator no-restricted-syntax**

**Почему?** Это обеспечивает соблюдение нашего правила о неизменности переменных. Работать с чистыми функциями, которые возвращают значение, проще, чем с функциями с побочными эффектами.

Используйте `map() / every() / filter() / find() / findIndex() / reduce() / some() / ...` для итерации по массивам, а `Object.keys() / Object.values() / Object.entries()` для создания массивов, с помощью которых можно итерироваться по объектам.

```ts
const numbers = [1, 2, 3, 4, 5];

// плохо
let sum = 0;
for (let num of numbers) {
  sum += num;
}
sum === 15;

// хорошо
let sum = 0;
numbers.forEach((num) => {
  sum += num;
});
sum === 15;

const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;
```

#### 82. Используйте для сортировки `Intl-API`.

#### 83. Указывайте все возможные значения типов входных и выходных параметров у методов/функций через `|`.

```ts
// Плохо
private Method(value: number): string {
  return value ? value.toString() : null
}

// Хорошо
private Method(value: number): string | null {
  return value ? value.toString() : null
}
```

#### 84. Именуйте поля в `enum` с большой буквы.

**Почему?** На бэкенде принято называть поля в `enum` с большой буквы. Для поддержания консистентности.

#### 85. Используйте `null` для очистки значения поля, а не `undefined`.

```ts
// плохо
someField = undefined;

// хорошо
someField = null;
```

#### 86. Приводите значение логических вычислений к `boolean`, если есть вероятность возврата другого значения.

```ts
const valid = false;
const errors = {
  required: true;
}

// Плохо
validation(): boolean{
  return valid || errors
}

//  Хорошо
validation(): boolean{
  return Boolean(valid || errors)
}
```

#### 87. Выносите тело запроса в константу/переменную.

```ts
const updateRequest = {
    id: this.id,
    number: this.number,
    date: this.date,
  },
};
this.requestService
  .update(updateRequest)
  .subscribe((response) => {
    ...
  });
```

#### 88. Используйте отступ в 4 пробела.

#### 89. Не используйте конструкцию `as any`.