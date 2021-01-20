# JS/TS

1. Использовать для сортировки Intl-API

   a. Понятный интерфейс API

   b. Сортировка не по коду Unicode, а по алфавиту

Код-стайл
Объявление переменных и правила именования:

1. Использование const и let вместо var. eslint: prefer-const, no-const-assign, no-var (переменные)
2. При поверхностном копировании объектов и массивов лучше использовать оператор «…», а не Object.assing (объекты)
   // очень плохо
   const original = { a: 1, b: 2 };
   const copy = Object.assign(original, { c: 3 });

// плохо
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 });

// хорошо
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 };

3. Для создания массива используйте литеральную нотацию. eslint: no-array-constructor (массивы)
   // плохо
   const items = new Array();

// хорошо
const items = [];

4. Для копирования массивов используйте оператор расширения ...
   const itemsCopy = [...items];
5. Избегайте названий из одной буквы. Имя должно быть наглядным. eslint: id-length (именование)
6. Используйте camelCase для именования объектов, функций и экземпляров. eslint: camelcase (именование)
7. Используйте PascalCase только для именования конструкторов и классов. eslint: new-cap (именование)
8. Сокращения или буквенные аббревиатуры всегда должны быть в верхнем или нижнем регистре. (именование) Почему? Имена предназначены для удобства чтения.
   // плохо
   import SmsContainer from './containers/SmsContainer';
   // плохо
   const HttpRequests ;
   // хорошо
   import SMSContainer from './containers/SMSContainer';
   const httpRequests
9. Не используйте \_ в начале или в конце названий. eslint: no-underscore-dangle (именование)
10. Используются одинарные кавычки в коде eslint: quotes (строки)
11. При создании строки программным путём используйте шаблонные строки вместо конкатенации. eslint: prefer-template template-curly-spacing (строки)
    // плохо
    Var x = 'How are you, ' + name + '?';

    // хорошо
    Var x = `How are you, ${name}?`;

12. Никогда не используйте eval(), т.к. это открывает множество уязвимостей. eslint: no-eval (строки)
13. Не используйте в строках необязательные экранирующие символы. eslint: no-useless-escape (строки)
    Почему? Обратные слеши ухудшают читабельность, поэтому они должны быть только при необходимости.
    // плохо
    const foo = '\'this\' \i\s \"quoted\"';

// хорошо
const foo = '\'this\' is "quoted"';
const foo = `my name is '${name}'`; 14. Используйте === и !== вместо == и !=. eslint: eqeqeq (операторы сравнения и равенства) 15. Для булевых типов применять сокращение (операторы сравнения и равенства)
// плохо
if (isValid === true) …
// хорошо
if (isValid) … 16. Для строк и чисел применяйте явное сравнение (операторы сравнения и равенства)
// плохо
if (name) ИЛИ if (collection.length)
// хорошо
if (name !== '') ИЛИ if (collection.length > 0) 17. Каждая строка заканчивается точкой с запятой eslint: semi
Почему? Когда JavaScript встречает перенос строки без точки с запятой, он использует правило под названием Автоматическая Вставка Точки с запятой (Automatic Semicolon Insertion), чтобы определить, стоит ли считать этот перенос строки как конец выражения и (как следует из названия) поместить точку с запятой в вашем коде до переноса строки. Однако, ASI содержит несколько странных форм поведения, и ваш код может быть сломан, если JavaScript неверно истолкует ваш перенос строки. Эти правила станут сложнее, когда новые возможности станут частью JavaScript. Явное завершение ваших выражений и настройка вашего линтера для улавливания пропущенных точек с запятыми помогут вам предотвратить возникновение проблем. 18. Добавляйте висячие запятые. eslint: comma-dangle (запятые)
Почему? Такой подход даёт понятную разницу при просмотре изменений. Кроме того, транспиляторы типа Babel удалят висячие запятые из собранного кода, поэтому вы можете не беспокоиться о проблемах в старых браузерах.
// плохо
const hero = {
firstName: 'Dana',
lastName: 'Scully'
};

// хорошо
const hero = {
lastName: 'Scully',
};

// хорошо (обратите внимание, что висячей запятой не должно быть после rest-аргумента)
createHero(
inventorOf,
...heroArgs
); 19. Не начинайте строку с запятой. eslint: comma-style (запятые)
// плохо
const story = [
once
, upon
];

    // хорошо
    const story = [
      once,
      upon
    ];

20. Всегда используйте модули (import/export) вместо нестандартных модульных систем. Вы всегда сможете транспилировать код в вашу любимую модульную систему. (модули)
21. Не используйте импорт через _. (модули)
    Почему? Это гарантирует, что у вас есть единственный экспорт по умолчанию.
    // плохо
    import _ as AirbnbStyleGuide from './AirbnbStyleGuide';

// хорошо
import AirbnbStyleGuide from './AirbnbStyleGuide'; 22. Не экспортируйте прямо из импорта. (модули)
Почему? Несмотря на то, что запись в одну строку является краткой, разделение на отдельные строки делает вещи последовательными.
// плохо
// файл es6.js
export { es6 as default } from './AirbnbStyleGuide';

// хорошо
// файл es6.js
import { es6 } from './AirbnbStyleGuide';
export default es6; 23. Импортируйте из пути только один раз. eslint: no-duplicate-imports (модули)
Почему? Наличие нескольких строк, которые импортируют из одного и того же файла, может сделать код неподдерживаемым.
// плохо
import foo from 'foo';
import { named} from 'foo';

// хорошо
import foo, { named1, named2 } from 'foo'; 24. Не экспортируйте изменяемые переменные. eslint: import/no-mutable-exports (модули)
Почему? Вообще, следует избегать мутации, в особенности при экспорте изменяемых переменных. Несмотря на то, что эта техника может быть необходима в редких случаях, в основном только константа должна быть экспортирована.
// плохо
let foo = 3;
export { foo };

// хорошо
const foo = 3;
export { foo }; 25. В модулях с единственным экспортом предпочтительнее использовать экспорт по умолчанию, а не экспорт по имени. eslint: import/prefer-default-export (модули)
Почему? Для того чтобы поощрять создание множества файлов, которые бы экспортировали одну сущность, т.к. это лучше для читабельности и поддержки кода.
// плохо
export function foo() {}

// хорошо
export default function foo() {} 26. Поместите все импорты выше остальных инструкций. eslint: import/first (модули)
Почему? Так как import обладает подъёмом, то хранение их всех в начале файла предотвращает от неожиданного поведения. 27. Импорты на нескольких строках должны быть с отступами как у многострочных литералов массива и объекта. (модули)
Почему? Фигурные скобки следуют тем же правилам отступа как и любая другая фигурная скобка блока в этом руководстве, тоже самое касается висячих запятых.
// плохо
import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

// хорошо
import {
longNameA,
longNameB,
longNameC,
longNameD,
longNameE,
} from 'path';

28. Используйте конструкцию /\*_ ... _/ для многострочных комментариев. (комментарии)
    // плохо
    // make() возвращает новый элемент
    // соответствующий переданному названию тега
    //

// хорошо
/\*\*

- make() возвращает новый элемент
- соответствующий переданному названию тега
  \*/

29. Используйте двойной слеш // для однострочных комментариев. Располагайте такие комментарии отдельной строкой над кодом, который хотите пояснить. Если комментарий не является первой строкой блока, добавьте сверху пустую строку. (комментарии)
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
} 30. Начинайте все комментарии с пробела, так их проще читать. eslint: spaced-comment (комментарии)
// плохо
//это текущая вкладка
// хорошо
// это текущая вкладка

/\*\*

- make() возвращает новый элемент
  \*/

31. Если комментарий начинается со слов FIXME или TODO, то это помогает другим разработчикам быстро понять, когда вы хотите указать на проблему, которую надо решить, или когда вы предлагаете решение проблемы, которое надо реализовать. Такие комментарии, в отличие от обычных, побуждают к действию: FIXME: -- нужно разобраться с этим или TODO: -- нужно реализовать. (комментарии)
32. Используйте объявление const или let для каждой переменной или присвоения. eslint: one-var (переменные)
    // плохо
    const items = getItems(),
    goSportsTeam = true;

// хорошо
const items = getItems();
const goSportsTeam = true; 33. В первую очередь группируйте const, а затем let.
Почему? Это полезно, когда в будущем вам понадобится создать переменную, зависимую от предыдущих.
// плохо
let i;
const items = getItems();
let dragonball;
const goSportsTeam = true;

// хорошо
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i; 34. Создавайте переменные там, где они вам необходимы, но помещайте их в подходящее место. (переменные) 35. Не создавайте цепочки присваивания переменных. eslint: no-multi-assign (переменные)
Почему? Такие цепочки создают неявные глобальные переменные.
// плохо
let a = b = c = 1;

let a = 1;
let b = a;
let c = a; 36. В присвоении избегайте разрывов строк до и после =. Если ваше присвоение нарушает правило max-len, оберните значение в круглые скобки. eslint operator-linebreak. (переменные)
Почему? Разрывы строк до и после = могут приводить к путанице в понимании значения.
// плохо
const foo =
superLongLongLongLongLongLongLongLongFunctionName();

// хорошо
const foo = (
superLongLongLongLongLongLongLongLongFunctionName()
);

// хорошо
const foo = 'superLongLongLongLongLongLongLongLongString'; 37. Запретить неиспользуемые переменные. eslint: no-unused-vars (переменные)
Почему? Переменные, которые объявлены и не используются в коде, скорее всего, являются ошибкой из-за незавершённого рефакторинга. Такие переменные занимают место в коде и могут привести к путанице при чтении. 38. Каждый компонент должен иметь блок-обертку.
Почему? Потенциально может привести проблемам верстки, если настроен какой-нибудь сдвиг по тегу, который повлияет на первый тег.
//Плохо
<div>1</div>
<div>2</div>
//Хорошо
<div>
<div>1</div>
<div>2</div>

</div>
39.	Инстанс сервиса, класса и т.д. должен иметь такое же имя, только в camelCase, если он единственный  в классе.
	Почему? Теряется контекст использования
	//Плохо:
	link = new LinkService().
	//Хорошо:
	linkService = new LinkService().
40.	По возможности избегать get() и set() для полей класса
Почему? могут возникнуть проблемы с тестированием, пониманием логики и поддержкой. Явное исключение – создание компонента с ControlValueAccessor

41. Использовать Number.isNaN и Number.isFinite вместо isNaN и isFinite.
    Почему? Глобальная функция isNaN приводит не-числа к числам, возвращая true для всего, что приводится к NaN. Если такое поведение необходимо, сделайте его явным.
42. Если ваш управляющий оператор (if, while и т.д.) слишком длинный или превышает максимальную длину строки, то каждое (сгруппированное) условие можно поместить на новую строку. Логический оператор должен располагаться в начале строки.
    Почему? Наличие операторов в начале строки приводит к выравниванию операторов и напоминает цепочку методов. Это также улучшает читаемость, упрощая визуальное отслеживание сложной логики.
    // плохо
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
    thing1();
    }

// хорошо
if (
(foo === 123 || bar === 'abc')
&& doesItLookGoodWhenItBecomesThatLong()
&& isThisReallyHappening()
) {
thing1();
}

43. Ставьте 1 пробел перед открывающей фигурной скобкой у блока. eslint: space-before-blocks (пробелы)
    // плохо
    function test(){
    console.log('test');
    }
    // хорошо
    function test() {
    console.log('test');
    }

44. Ставьте 1 пробел перед открывающей круглой скобкой в операторах управления (if, while и т.п.). Не оставляйте пробелов между списком аргументов и названием в объявлениях и вызовах функций. eslint: keyword-spacing (пробелы)
    // плохо
    if(isJedi) {
    // хорошо
    if (isJedi) {
45. Разделяйте операторы пробелами. eslint: space-infix-ops (пробелы)
    // плохо
    const x=y+5;
    // хорошо
    const x = y + 5;

46. В конце файла оставляйте одну пустую строку. eslint: eol-last (пробелы)
47. Используйте переносы строк и отступы, когда делаете длинные цепочки методов (больше 2 методов). Ставьте точку в начале строки, чтобы дать понять, что это не новая инструкция, а продолжение цепочки. eslint: newline-per-chained-call no-whitespace-before-property
    // плохо
    $('#items').find('.selected').highlight().end().find('.open').updateCount();
// хорошо
$('#items')
    .find('.selected')
    .highlight()
48. Оставляйте пустую строку между блоком кода и следующей инструкцией. (пробелы)
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

49. Не добавляйте отступы до или после кода внутри блока. eslint: padded-blocks (пробелы)
    // плохо
    function bar() {

console.log(foo);

}
// хорошо
function bar() {
console.log(foo);
} 50. Не используйте множество пустых строк для заполнения кода. eslint: no-multiple-empty-lines (пробелы) 51. Не добавляйте пробелы между круглыми скобками и их содержимым. eslint: space-in-parens (пробелы)
// плохо
function bar( foo ) {

// хорошо
function bar(foo) {

52. Не добавляйте пробелы между квадратными скобками и их содержимым. eslint: array-bracket-spacing
    // плохо
    [ 1, 2, 3 ];
    // хорошо
    [1, 2, 3];

53. Добавляйте пробелы между фигурными скобками и их содержимым. eslint: object-curly-spacing (пробелы)
    // плохо
    const foo = {clark: 'kent'};

// хорошо
const foo = { clark: 'kent' }; 54. Старайтесь не допускать, чтобы строки были длиннее 100 символов (включая пробелы). Замечание: длинные строки с текстом освобождаются от этого правила и не должны разбиваться на несколько строк. eslint: max-len
Почему? Это обеспечивает удобство чтения и поддержки кода. 55. Должно быть согласованное расстояние между открывающим символом блока и следующим символом на одной и той же строке. Тоже самое касается расстояния между закрывающим символом блока и предыдущим символом. eslint: block-spacing (пробелы)
// плохо
function foo() {return true;}
if (foo) { bar = 0;}
// хорошо
function foo() { return true; }
if (foo) { bar = 0; } 56. Избегайте пробелов перед запятыми и ставьте его после. eslint: comma-spacing
// плохо
var foo = 1,bar = 2;
var arr = [1 , 2];
// хорошо
var foo = 1, bar = 2;
var arr = [1, 2]; 57. Избегайте пробелов внутри скобок вычисляемого свойства. eslint: computed-property-spacing (пробелы)
// плохо
obj[foo ]
obj[ 'foo']
// хорошо
obj[foo]
obj['foo'] 58. Избегайте пробелов между функциями и их вызовами. eslint: func-call-spacing (пробелы)
// плохо
func ();
func
();
// хорошо
func(); 59. Избегайте пробелов в конце строки. eslint: no-trailing-spaces (пробелы) 60. Избегайте множества пустых строк и новой строки в начале файлов. Разрешайте только одну пустую строку в конце файла. eslint: no-multiple-empty-lines (пробелы) 61. Используйте фигурные скобки, когда блок кода занимает несколько строк. eslint: nonblock-statement-body-position (блоки)
// плохо
if (test)
return false;
// хорошо
if (test) return false;
// хорошо
if (test) {
return false;
}
// плохо
function foo() { return false; }
// хорошо
function bar() {
return false;
} 62. Если блоки кода в условии if и else занимают несколько строк, расположите оператор else на той же строчке, где находится закрывающая фигурная скобка блока if. eslint: brace-style (блоки)
// плохо
if (test) {
}
else {
// хорошо
if (test) {
} else {}

63. Если в блоке if всегда выполняется оператор return, последующий блок else не нужен. return внутри блока else if, следующем за блоком if, который содержит return, может быть разделён на несколько блоков if. eslint: no-else-return (блоки)
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

64. Используйте функциональные выражения вместо объявлений функций. eslint: func-style (функции)
    Почему? У объявлений функций есть подъём. Это означает, что можно использовать функцию до того, как она определена в файле, но это вредит читабельности и поддержке.
    // плохо
    function foo() {
    // ...
    }
    // плохо
    const foo = function () {
    // ...
    };
    // хорошо
    // лексическое имя, отличное от вызываемой(-ых) переменной(-ых)
    const foo = function uniqueMoreDescriptiveLexicalFoo() {
    // ...
    };
65. Никогда не объявляйте функции в нефункциональном блоке (if, while, и т.д.). Вместо этого присвойте функцию переменной. eslint: no-loop-func (функции)
66. Никогда не называйте параметр arguments. Он будет иметь приоритет над объектом arguments, который доступен для каждой функции. (функции)
    // плохо
    function foo(name, options, arguments) {
    // хорошо
    function foo(name, options, args) {
67. Не используйте arguments, вместо этого используйте синтаксис оставшихся параметров .... eslint: prefer-rest-params (функции)
    Почему? ... явно говорит о том, какие именно аргументы вы хотите извлечь. Кроме того, такой синтаксис создаёт настоящий массив, а не массивоподобный объект как arguments.
    // плохо
    function concatenateAll() {
    // хорошо
    function concatenateAll(...args) {
68. Используйте синтаксис записи аргументов по умолчанию, а не изменяйте аргументы функции.
    // очень плохо
    function handleThings(opts) {
    opts = opts || {};
    }
    // хорошо
    function handleThings(opts = {}) {
    // ...
    }
69. Всегда вставляйте последними параметры по умолчанию.
    // плохо
    function handleThings(opts = {}, name) {
    // хорошо
    function handleThings(name, opts = {}) {
70. Используйте Отступы при определении функции. eslint: space-before-function-paren space-before-blocks
    Почему? Однородность кода — это хорошо. Вам не надо будет добавлять или удалять пробел при манипуляции с именем.
    // плохо
    const f = function(){};

// хорошо
const x = function () {};

71. Никогда не изменяйте параметры. eslint: no-param-reassign
72. Отдавайте предпочтение использованию оператора расширения ... при вызове вариативной функции. eslint: prefer-spread
    Почему? Это чище, вам не нужно предоставлять контекст, и не так просто составить new с apply.
    // плохо
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

// хорошо
const x = [1, 2, 3, 4, 5];
console.log(...x);

// хорошо
new Date(...[2016, 8, 5]); 73. Функции с многострочным определением или запуском должны содержать такие же отступы, как и другие многострочные списки в этом руководстве: с каждым элементом на отдельной строке, с запятой в конце элемента. eslint: function-paren-newline
// плохо
function foo(bar,
baz,
quux) {}
// хорошо
function foo(
bar,
baz,
quux,
) {} 74. Используйте фигурные скобки для case и default, если они содержат лексические декларации (например, let, const, function, и class). eslint: no-case-declarations.
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
} 75. Тернарные операторы не должны быть вложены и в большинстве случаев должны быть расположены на одной строке. eslint: no-nested-ternary.
// плохо
const foo = maybe1 > maybe2
? "bar"
: value1 > value2 ? "baz" : null;
// хорошо
const foo = maybe1 > maybe2 ? 'bar' : maybeNull; 76. Избегайте ненужных тернарных операторов. eslint: no-unneeded-ternary.
// плохо
const foo = a ? a : b;
const bar = c ? true : false;
const baz = c ? false : true;

// хорошо
const foo = a || b;
const bar = !!c;
const baz = !c; 77. Используйте точечную нотацию для доступа к свойствам. eslint: dot-notation (свойства объекта)
// плохо
const isJedi = luke['jedi'];

// хорошо
const isJedi = luke.jedi; 78. В Angular для доступа к полям формы используется метод form.get(‘controlName’). Свойство controls используется для доступа к полям, с целью массовых операций (генерация формы в цикле) (свойства объекта) (https://angular.io/guide/reactive-forms#step-3-accessing-the-formarray-control / https://angular.io/guide/reactive-forms#step-4-displaying-the-form-array-in-the-template) 79. Используйте оператор \*\* для возведения в степень. eslint: no-restricted-properties. (свойства объекта)
// плохо
const binary = Math.pow(2, 10);

// хорошо
const binary = 2 \*\* 10; 80. Используйте extends для наследования. (классы и конструкторы)
Почему? Это встроенный способ наследовать функциональность прототипа, не нарушая instanceof. 81. Методы могут возвращать this, чтобы делать цепочки вызовов. (классы и конструкторы)
// плохо
Jedi.prototype.jump = function () {
this.jumping = true;
return true;
};

Jedi.prototype.setHeight = function (height) {
this.height = height;
};

const luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20); // => undefined

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
luke.jump()
.setHeight(20); 82. У классов есть конструктор по умолчанию, если он не задан явно. Можно опустить пустой конструктор или конструктор, который только делегирует выполнение родительскому классу. eslint: no-useless-constructor (классы и конструкторы) 83. Избегайте дублирующих членов класса. eslint: no-dupe-class-members (классы и конструкторы)
Почему? Если объявление члена класса повторяется, без предупреждения будет использовано последнее. Наличие дубликатов скорее всего приведёт к ошибке. 84. Используйте операторы return внутри функций обратного вызова в методах массива. Можно опустить return, когда тело функции состоит из одной инструкции, возвращающей выражение без побочных эффектов. eslint: array-callback-return (массивы)
// хорошо
[1, 2, 3].map((x) => {
const y = x + 1;
return x \* y;
});

// хорошо
[1, 2, 3].map((x) => x + 1);

// плохо - нет возвращаемого значения, следовательно, `acc` становится `undefined` после первой итерации
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
const flatten = acc.concat(item);
}); 85. Если массив располагается на нескольких строках, то используйте разрывы строк после открытия и перед закрытием скобок. (массивы)
// плохо
const arr = [
[0, 1], [2, 3], [4, 5],
];

// хорошо
const arr = [[0, 1], [2, 3], [4, 5]];

const objectInArray = [
{
id: 1,
},
{
id: 2,
},
]; 86. При обращении к нескольким свойствам объекта используйте деструктуризацию объекта. eslint: prefer-destructuring
Почему? Деструктуризация избавляет вас от создания временных переменных для этих свойств.
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
// отлично
function getFullName({ firstName, lastName }) {
return `${firstName} ${lastName}`;
} 87. Используйте деструктуризацию массивов. eslint: prefer-destructuring
const arr = [1, 2, 3, 4];
// плохо
const first = arr[0];
const second = arr[1];
// хорошо
const [first, second] = arr; 88. Когда вам необходимо использовать анонимную функцию (например, при передаче встроенной функции обратного вызова), используйте стрелочную функцию. eslint: prefer-arrow-callback, arrow-spacing (стрелочные функции)
Почему? Таким образом создаётся функция, которая выполняется в контексте this, который мы обычно хотим, а также это более короткий синтаксис.
// плохо
[1, 2, 3].map(function (x) {
const y = x + 1;
return x \* y;
});

// хорошо
[1, 2, 3].map((x) => {
const y = x + 1;
return x \* y;
}); 89. Если тело функции состоит из одного оператора, возвращающего выражение без побочных эффектов, то опустите фигурные скобки и используйте неявное возвращение. В противном случае, сохраните фигурные скобки и используйте оператор return. eslint: arrow-parens, arrow-body-style
Почему? Синтаксический сахар. Когда несколько функций соединены вместе, то это лучше читается. (стрелочные функции)
// плохо
[1, 2, 3].map((number) => {
const nextNumber = number + 1;
`A string containing the ${nextNumber}.`;
});

// хорошо
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

// хорошо
[1, 2, 3].map((number) => {
const nextNumber = number + 1;
return `A string containing the ${nextNumber}.`;
});

// плохо
foo(() => bool = true); 90. В случае, если выражение располагается на нескольких строках, то необходимо обернуть его в скобки для лучшей читаемости. Почему? Это чётко показывает, где функция начинается и где заканчивается. (стрелочные функции) 91. Всегда оборачивайте аргументы круглыми скобками для ясности и согласованности. eslint: arrow-parens (стрелочные функции)
Почему? Минимизирует различия при удалении или добавлении аргументы.
// плохо
[1, 2, 3].map(x => x _ x);
// хорошо
[1, 2, 3].map((x) => x _ x);

92. Зафиксируйте расположение тела стрелочной функции с неявным возвратом. eslint: implicit-arrow-linebreak (стрелочные функции)
    // плохо
    (foo) =>
    bar;
    (foo) =>
    (bar);
    // хорошо
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
    bar
    )
93. Не используйте итераторы. Применяйте функции высшего порядка вместо таких циклов как for-in или for-of. eslint: no-iterator no-restricted-syntax (итераторы и генераторы)
    Почему? Это обеспечивает соблюдение нашего правила о неизменности переменных. Работать с чистыми функциями, которые возвращают значение, проще, чем с функциями с побочными эффектами.
    Используйте map() / every() / filter() / find() / findIndex() / reduce() / some() / ... для итерации по массивам, а Object.keys() / Object.values() / Object.entries() для создания массивов, с помощью которых можно итерироваться по объектам.
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

// отлично (используйте силу функций)
const sum = numbers.reduce((total, num) => total + num, 0);
sum === 15;

Дополнительные пункты:

1. Значение enum сейчас с 1-цы, хотя по документации начинается с 0 (возможно 0 === false). Нужно зафиксировать с пояснением или начать делать с 0.
2. Enum-ы с бэкенда формируются в PascalCase, на фронте принято писать в camelCase, нужно выбрать единый вариант именования.
3. Разделять импорты на подгруппы, как в Fora/коде ангуляра.
4. Разделять поля пустыми строками по типу доступности public и private
5. Использовать alias-ы путей для @shared и @core и аналогичных путей в Vue, потенциально в react-е.
6. Нужны правила именования. Например, именование ошибок bad или invalid (выработать правила именования, чтобы собирать имена как конструктор)
7. Зафиксированные названия для полей схожих по смыслу: комментарий, примечание, аннотация, описание.
8. На карточке редактирования использовать поле isNew или isEdit, смысла в них немного но условия в логике меняются местами, сбивает с толку. Нужно выбрать что предпочтительнее.
9. В pipe не должно быть публичных методов, кроме transform. (Был метод list, который возвращал NgOption из enum).
10. Предлагаю использовать значения «по-умолчанию» для всех полей в классе.
11. Писать ли стили и темплейты в контроллере, если они короткие или никогда?
12. Писать ли скобки у стрелочных функций в конструкции Promise.then(x => {x*x}) или же с неявным возвратом значения Promise.then(x => x*x)
13. Очистка значения поля через null или undefined (правильнее null, но в коде встречались использования undefined).
14. Избегать стилизации по тегу, кроме html, body, \* для сборса базовых стилей.
15. Задавать ли стили для компонентов в виде иерархии в обязательном порядке
16. Правильно по best practies: throw new Error(), а не throw 'someString';
17. Предлагаю делать преведение к Boolean через Boolean(), а не через !!, не слишком очевидно. Но new Boolean() – не правильно использовать.
18. Использовать ли по умолчанию на всех таблицах и списках функцю trackBy для предотвращения лишних перерисовок
19. Что предпочтительнее subscribe или вызов функции по input?
20. Как динамически включать/отключать валидаторы?
21. Нужны правила именования стилей, сейчас kebab-case, но если использовать БЭМ, то применяется «\_». Нужно хорошо обсудить.
22. Нужна единая структура описания компонентов
23. Назвать сервис в компоненте также, как называется сервис linkOf: LinkService
24. Сделать папку overrides, в которой будут храниться стили для переопределения компонентов, и они будут подключаться к основному style.scss. Также отдельно вынести переменные, чтобы их можно было везде подключать.
25. Формы должны иметь значения по-умолчанию соответствующие их отображению. Пустая строка, false, пустой массив и т.д. При очистке фильтров, можно прировнять значения формы к конфигурации формы.
26. У методов/функций тип входных и выходных данных указывать через “|”, а не через интерфейс. (Интерфейс может не до конца отслеживать все используемые поля)