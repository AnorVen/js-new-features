# Новые возможности JavaScript — `const`

Переменные, объявленные с ключевым словом `const`, являются постоянными и их
значение нельзя изменить в исходном коде. При определении переменной типа
`const` ей нужно сразу же задавать значение, иначе произойдёт ошибка.

Во многих языках, в том числе и в JavaScript, по традиции константы пишут большими
буквами, чтобы отделить их от переменных и не путать.

То, как мы делали это ранее:

```javascript
// ECMAScript 5
var COMPANY = 'Yandex';

console.log(COMPANY);
// Ожидаемый результат: "Yandex"
```

И в сообществе, до появления `const`, была договорённость, что переменные, объявленные
большими буквами, переопределять нельзя.  
Теперь всё иначе:

```javascript
// ECMAScript 6
const COMPANY; // Ошибка! Нельзя объявлять const без присваивания значения
```

```javascript
// ECMAScript 6
const COMPANY = 'Yandex';

COMPANY = 'Яндекс'; // Ошибка! Нельзя переопределять постоянную переменную

console.log(COMPANY);
```

Стоит отметить, что переменные типа `const` не поднимаются движком V8, как и `let`.
Подробнее об этом можно почитать в описании переменной типа `let`.

```javascript
// ECMAScript 6
console.log(COMPANY); // Ошибка! Такой переменной не существует

const COMPANY = 'Yandex';
```

Однако можно изменять объект, который присвоен постоянной переменной. Дело в том,
что переменная хранит не сам объект, а ссылку на него.

```javascript
// ECMAScript 6
const OBJ = {
  prop: true,
};

console.log(OBJ.prop);
// Ожидаемый результат: true

OBJ.prop = false;

console.log(OBJ.prop);
// Ожидаемый результат: false
```

Это происходит из-за того, что изменяется свойство самого объекта, а не значение постоянной
переменной (которая хранит ссылку на объект, а она не меняется).  
Тоже самое работает и с массивами.

Итого: ключевое слово const объявляет константу, причём доступ к ней осуществляется по ссылке
(как, впрочем, и ко всем переменным в JS). Таким образом, внутреннее состояние не примитивных
объектов можно менять, даже если они константы, но не присваивать в переменную другое значение.
