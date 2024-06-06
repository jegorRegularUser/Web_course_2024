#  1.История JavaScript

- JavaScript был создан в 1995 году Бренданом Айком, инженером в компании Netscape. Изначально он назывался Mocha, затем LiveScript, и, наконец, был назван JavaScript, с целью привлечения большего количества разработчиков из-за популярности java.
- В 1997 году разработчики устали от непонятности языка и повсеместным несвязанным обновлениям, из-за чего JavaScript был стандартизирован организацией ECMA International, и с тех пор появляются новые версии языка ecmascript(ES6, ES7, ES8 и т.д.).
- С течением времени JavaScript получил широкое распространение и стал основным языком веб-разработки.

### Роль JavaScript в веб-разработке

- JavaScript используется для добавления интерактивности и динамики на веб-страницы.
- Он позволяет изменять содержимое и стили HTML-элементов, реагировать на события (нажатия, наведение курсора и т.д.), отправлять HTTP-запросы и многое другое.
- JavaScript также используется для создания одностраничных приложений (SPA), серверных приложений с Node.js, мобильных приложений, игр и даже десктопных приложений.

### Основные применения JavaScript

- Клиентская разработка: создание интерактивных веб-страниц, SPA-приложений, обработка пользовательских взаимодействий.
- Серверная разработка: создание API, обработка HTTP-запросов, взаимодействие с базами данных с помощью Node.js.
- Разработка мобильных приложений: с использованием фреймворков, таких как React Native, NativeScript и др.
- Разработка игр и приложений: благодаря технологиям Canvas и WebGL.

# 1.5Синтаксические особенности

Перед тем как мы начнем работу я должен рассказать о некоторых синтаксических особенностях языка.

- Присвоение происходит через одно =.
- Все блоки кода разделяются точкой с запятой 

```javascript
Let a = 5;
If (a==5) {
a++};
```

- Все функции, классы, циклы требуют фигурных скоб 
``` javascript
 if(условие){код}; 
const a = function(аргументы){тело функции}
 ```

- Для вывода информации мы используем console.log(), подобный print() из Python или System.out.print() из Java.

# 2.Переменные, типы данных и операторы

### Объявление и присваивание переменных
Все объявление и присвоение идет в 4 этапа: ключевое слово + имя переменной + = + выражение//переменая
И есть всего три ключевых слов объявления
```javascript
// "var", до 2015 был единственным способом, но из-за проблем с var(рассказывается в лекции 3) сейчас так делать нельзя
var x = 5;
var name = "John";

// "let"
let age = 25;
age = 30;
age = 35; // изменяемая переменная
let isStudent = true;

// "const"
const PI = 3.14159; // неизменяемая константа
```

### Примитивные типы данных

- Число (number): 42, 3.14, -10
- Строка (string): "Hello", 'World'
- Логическое значение (boolean): true, false
- Null
- Undefined
- NaN (not a number, можно получить если условно разделить что-либо на 0)

### Ссылочные типы данных

- Объекты (object): { name: "John", age: 30 }
- Массивы (array): [1, 2, 3, 4, 5]
- Функции (function): function() { }, () => {}

### Преобразование типов

```javascript
let x = "5" + 2; // Результат: "52" (строковое конкатенирование)
let y = "5" - 2; // Результат: 3 (числовое вычитание)
let z = Number("42"); // Результат: 42 (преобразование в число)
```

### Арифметические и логические операторы

```javascript
let a = 10;
let b = 4;

// Арифметические(+, -, *, /, %)
console.log(a + b); // 14
console.log(a - b); // 6
console.log(a * b); // 40
console.log(a / b); // 2.5
console.log(a % b); // 2 (остаток от деления)

// Логические(==, >, >=, <, <=, !=, ===, !==, !, ||, &&)
console.log(a > b); // true
console.log(a <= b); // false
console.log(1 === 1); // true – тройное равно проверяет не только значение, но и тип данных
console.log("1" == 1); // true – 1==1
console.log("1" === 1); // false – 1==1, но строка != число
console.log(a !== b); // true
console.log(true && false); // лог и -- false

console.log(true || false); // лог или -- true
console.log(!true); // лог не – false
```

Фактически, все, что существует, это true, а все, чего нет, это false. Так что любые числа, строки и тп это true, а undefined, NaN, null это false.

### Высший булин

Вы уже не маленькие, так что сразу же расскажу и о высшем булине

```javascript
Console.log(false || 'я существую!'')
```

Этот код выдаст true, так как строка это true? Нет, здесь не происходит динамического приведения типов, и из-за этого || будет выдавать первый же true объект, либо просто последний false, а && наоборот будет выдавать первый же false объект и последний true

```javascript
console.log( [] && 'я существую!') // []
console.log(false || 0 || undefined || 'я существую!' || NaN) // 'я существую!'
console.log('я существую!' && 2 && { key: ’value’ } && [1,2,3,4] && (() => {return 1}) && undefined && 3) // undefined
```

# 3. Функции и области видимости:

В js есть три способа задания функции:

```javascript
// Функциональное выражение
let greet = function (name) {
  console.log("Hello, " + name + "!");
};

// Стрелочная функция
let greetArrow = (name) => {
  console.log("Hello, " + name + "!");
};

// Объявление функции
function greetDefault(name = "stranger") {
  console.log("Hello, " + name + "!");
}
```

Ключевое слово return позволяет возвращать какое-либо значение из функции

```javascript
const a = (num) => {
  return num + 1;
};
console.log(a(5)); // 6
```

### Области видимости:

Всего можно выделить три области видимости – глобальная (Global Scope), локальная (Local Scope), представляет собой ограничения блоком функции, цикла и тп, и Блочная, которая представляет собой ограничения фигурными скобками, также переменные, объявленные с помощью let и const, имеют блочную область видимости.

```javascript
let globalVar = "I am global";

function outerFunction() {
  let localVar = "I am local";
  {
    let mes = "I in block";
  }
  console.log(globalVar); // I am global
  console.log(localVar); // I am local
  console.log(mes); // undefined
}
console.log(localVar); // undefined
```

И помните я говорил о var-проблеме?
Тогда предположите, что выдаст этот код

```javascript
{
  var a = 5;
}
console.log(a);
```

Undefined? К сожалению, нет. Переменные var пробивают область видимости, что приводит со временем к большому количеству ошибок, связанных с одинаковым неймингом.

### Контекст вызова (this):

```javascript
let person = {
  name: "John",

  greet: () => {
    console.log(Hello, my name is ${this.name}); // об подобной записи поговорим в 5 лекции
  }
};

person.greet(); // Выведет "Hello, my name is John"
```

# 4. Условные операторы и циклы:

## Условные операторы:

```javascript
let age = 18;
if (age >= 18) {
  console.log("You are an adult.");
} else {
  console.log("You are a minor.");
}
```

### Тернарный оператор

```javascript
let canDrive = age >= 18 ? "Yes" : "No";
console.log("Can you drive? " + canDrive);
```

## Циклы:

```javascript
// Цикл for
for (let i = 0; i < 5; i++) {
  console.log(i); // Выведет 0, 1, 2, 3, 4
}

// Цикл while
let count = 0;
while (count < 3) {
  console.log(count);
  count++;
}

// Цикл do-while
let num = 0;
do {
  console.log(num);
  num++;
} while (num < 3);
```

### Ключевое слово break заканчивает цикл, а continue перепрыгивает на следующий шаг итерации

# 5. Действия со строками

Для работы со строками в js есть большое количество методов:

```javascript
let a = 'Люблю нртк'
   - length - получение длины строки.
console.log(a.length) //10
   - charAt() - получение символа по индексу.
console.log(a.charAt(2)) // 'б'
   - indexOf() - поиск подстроки в строке.
console.log(a.indexOf('б')) // 2
   - slice() - извлечение части строки.
console.log(a.slice(0, 5)) // 'Люблю'
   - substring() - извлечение части строки (аналогично slice()).
console.log(a.substring(0, 5)) // 'Люблю'
   - substr() - извлечение части строки (с длиной).
console.log(a.substr(2, 2))// ' бл'
   - replace() - замена подстроки в строке.
console.log(a.replace('Л', 'Не л')) // 'Не люблю нртк'
   - toUpperCase() - преобразование в верхний регистр.
   - toLowerCase() - преобразование в нижний регистр.
   - trim() - удаление пробельных символов в начале и конце строки.
   - split() - разделение строки на массив по заданному разделителю.
console.log(a.split(' ')) // ["Люблю", "нртк"]
   - concat() - объединение строк.
```

Также есть литеральная запись строки, благодаря которой можно записывать переменные в строке напрямую
Обычный способ:

```javascript
console.log("Тебя зовут " + name + "?");
```

Литеральный способ:

```javascript
console.log(`Тебя зовут ${name}?`);
```

Для него нужно обязательно использовать обратные кавычки и для переменной придется писать ${}.


# 6. Объекты и массивы:
## Объекты
### 1. Создание объектов
   - Литеральная нотация:
``` javascript
  const person = {      
  name: 'John Doe',       
  age: 30,        
  occupation: 'Software Engineer'      };  
```    
   - Использование конструктора Object():
``` javascript
   const person = new Object();  
    person.name = 'John Doe'; 
    person.age = 30; 
    person.occupation = 'Software Engineer'; 
```     
### 2. Доступ к свойствам объекта
   - Точечная нотация:
``` javascript
     console.log(person.name); // 'John Doe'    
```  
   - Нотация с использованием скобок:
``` javascript
     console.log(person['occupation']); // 'Software Engineer'   
```
 этот подход полезен если нам нужно получать значение из объекта по переменной, или если ключ имеет сложную или строковую запись ``` (person[`salary-in-${ currency }`]  ```
### 3. Добавление, изменение и удаление свойств
   - Добавление:
``` javascript
       person.city = 'New York';  
```    
   - Изменение:
``` javascript
        person.age = 31;   
```   
   - Удаление:
``` javascript
         delete person.occupation; 
```     

### 4. Перебор свойств объекта
   - Цикл for...in:
``` javascript
for (const prop in person) {
       console.log(`${prop}: ${person[prop]}`); 
}      
```
### 5. Методы работы с объектами
   - Object.keys():
``` javascript
     const keys = Object.keys(person);      
     console.log(keys); // ['name', 'age', 'city'] 
```     
   - Object.values():
``` javascript
     const values = Object.values(person);      
     console.log(values); //  ['John Doe', 31, 'New York']  
```    
   - Object.entries():
``` javascript
     const entries = Object.entries(person);      
console.log(entries);      // [['name', 'John Doe'], ['age', 31], ['city', 'New York']]  
```    

### 6. Опциональная цепочка (optional chain)
В разработке часто будет встречаться подобное
``` javascript
Const a = {
b: {
c : {
d: {…}  …}  …}  …}
```
И в данном случае можно делать промежуточные переменные
``` javascript
Let b = a.b
Let c = b.c
Let d = c.d
```
Но согласитесь, что это крайне неудобно и достаточно мусорно, поэтому на это есть решение в виде цепочки
``` javascript
Let d = a.b.c.d 
```
Особенно это полезно при использовании методов
``` javascript
Let hiEgor = ‘Привет, Егор’
Let hiVlad = hiEgor.replace(‘Егор’, ‘Влад’).concat(‘!’) // ‘Привет, Влад!’
```

## Массивы:
``` javascript
let numbers = [1, 2, 3, 4, 5];
console.log(numbers[2]); // 3
```
И перед тем как я начну рассказывать про методы массивов нужно сделать одно уточнение, в качестве аргументов методы могут получать что угодно, в том числе и функции, которые при такой передаче называются callback функции. И в среде разработчиков js устаканилось, передавать только стрелочную функцию из-за ее компактности
``` javascript
someArr.map(function(element){ return element})
someArr.map(element=>element) //Согласитесь, такая запись куда приятней глазу
``` 

## Методы Массивов
### - Изменение исходного массива:
``` javascript
- array[index] = newValue - изменяет значение элемента по указанному индексу.
push(element1, element2, ..., elementN) - добавляет один или несколько элементов в конец массива.
unshift(element1, element2, ..., elementN) - добавляет один или несколько элементов в начало массива.
pop() - удаляет последний элемент массива и возвращает его.
shift() - удаляет первый элемент массива и возвращает его.
splice(start, deleteCount, item1, item2, ...) - удаляет элементы из массива и (если предоставлено) вставляет новые.
reverse() - меняет порядок элементов в массиве на обратный
sort(function) - сортирует элементы массива на месте и возвращает отсортированный массив
```
### -Создание нового массива
``` javascript
map(callback(currentValue, index, array) - создает новый массив с результатами вызова указанной функции для каждого элемента вызывающего массива:
  let numbers = [1, 2, 3, 4, 5];
  let doubledNumbers = numbers.map(num => num * 2);
  console.log(doubledNumbers); // [2, 4, 6, 8, 10]
filter(callback(currentValue, index, array) - создает новый массив со всеми элементами, прошедшими проверку, реализованную в передаваемой функции:
  let evenNumbers = numbers.filter(num => num % 2 === 0);
  console.log(evenNumbers); // [2, 4]
slice(start, end) - возвращает новый массив, содержащий копию части исходного массива
concat() - объединяет два или более массива и возвращает новый массив:
```
### Содержит ли массив
``` javascript
includes(searchElement) - проверяет, содержится ли в массиве указанный элемент, и возвращает true или false
every(callback(currentValue, index, array) - проверяет, удовлетворяют ли все элементы массива условию, заданному в callback-функции:
  let allEven = numbers.every(num => num % 2 === 0);
  console.log(allEven); // false
some(callback(currentValue, index, array), thisValue) - проверяет, удовлетворяет ли хотя бы один элемент массива условию, заданному в callback-функции:
  let hasEven = numbers.some(num => num % 2 === 0);
  console.log(hasEven); // true
find(callback(currentValue, index, array) и findIndex(callback(currentValue, index, array)) - возвращают первый элемент массива, удовлетворяющий условию, заданному в callback-функции, или его индекс:
  let num = numbers.find(n => n  % 2);
  console.log(num); //  2
  let index = numbers.findIndex(n => n % 2);
  console.log(index); // 1. 
```
### Новая строка
``` javascript
join(separator) - преобразует массив в строку, разделяя элементы указанным разделителем:
  let fruits = ['apple', 'banana', 'orange'];
  let str = fruits.join(' - ');
console.log(str); // "apple - banana - orange"
```
### Преобразование в значение
``` javascript
reduce(callback(accumulator, currentValue, currentIndex, array), initialValue) - применяет функцию редукции к каждому элементу массива, возвращая единое значение:
  let sum = numbers.reduce((acc, num) => acc + num, 0);
  console.log(sum); // 15
  let max = numbers.reduce((acc, num) => (num > acc ? num : acc), 0);
  console.log(max); // 5
```
## Итерация массива
``` javascript
- for - классический цикл для перебора элементов:
  for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
  }
- for...of - цикл для перебора значений элементов:
  for (let fruit of fruits) {
    console.log(fruit);
  }
- forEach() - метод для перебора элементов с использованием callback-функции:
fruits.forEach(fruit => console.log(fruit));
```

for === for…of === forEach

## Деструктуризация
Деструктуризация в JavaScript - это удобный способ извлечения значений из объектов и массивов и присваивания их переменным. Она позволяет получить доступ к определенным свойствам объекта или элементам массива в более компактном и читаемом виде.
### Деструктуризация объектов:
1. Базовый синтаксис:
``` javascript
const { property1, property2 } = object;
```
Здесь property1 и property2 будут соответствовать одноименным свойствам объекта object.
2. Переименование свойств:
``` javascript
const { property1: newName1, property2: newName2 } = object;
```
В этом случае newName1 и newName2 будут соответствовать property1 и property2 объекта object.

1. Установка значений по умолчанию:
``` javascript
const { property1 = 'default value', property2 } = object;
```
Если property1 объекта object не существует или равно undefined, то property1 будет равно 'default value'.
1. Вложенные объекты:
``` javascript
const { nestedObject: { nestedProperty1, nestedProperty2 } } = object;
```
Здесь nestedProperty1 и nestedProperty2 будут соответствовать свойствам вложенного объекта nestedObject в объекте object.

### Деструктуризация массивов:
1. Базовый синтаксис:
``` javascript
const [element1, element2] = array;
```
Здесь element1 и element2 будут соответствовать первому и второму элементам массива  
2. Пропуск элементов:
``` javascript
const [, element2, element3] = array;
```
В этом случае element2 и element3 будут соответствовать второму и третьему элементам массива  
3. Использование остаточного оператора rest:
``` javascript
const [element1, ...restElements] = array;
```
Здесь element1 будет соответствовать первому элементу массива array, а restElements будет являться массивом, содержащим все остальные элементы.
4. Деструктуризация вложенных массивов:
``` javascript
const [[element1, element2], [element3, element4]] = nestedArray;
```
В данном примере element1 и element2 будут соответствовать первому и второму элементам первого подмассива, а element3 и element4 - первому и второму элементам второго подмассива.
5. Использование оператора Spread
Spread это обратный оператору rest, если rest “собирает” массив, то spread наоборот его разбирает, деструктуризирует.
Имеет такой же синтаксис 3 точек
``` javascript
Console.log(…[1,2,3,4,5]) //1 2 3 4 5
```



## Встроенные объекты:
``` javascript
console.log(Math.PI); // 3.141592653589793
console.log(Math.max(5, 10, 3)); // 10
let currentDate = new Date();
console.log(currentDate.toISOString()); // Формат даты и времени
```
Работа с регулярными выражениями:
``` javascript
let emailRegex = /\S+@\S+\.\S+/;
let email = "john@example.com";
console.log(emailRegex.test(email)); // true
```
# 7. Работа с DOM:
DOM (Document Object Model) - это программный интерфейс для веб-страниц, который позволяет программам и скриптам динамически получать доступ и обновлять содержимое, структуру и стиль документа. Другими словами, DOM представляет структуру HTML-документа в виде объектной модели - дерева, которое можно программно использовать и изменять. Каждый элемент HTML-документа (тег, текст, атрибут и т.д.) является узлом в этом дереве. Узлы связаны между собой родительско-дочерними отношениями, образуя древовидную структуру.
Доступ к DOM-элементам:
``` javascript
let heading = document.getElementById("main-heading");
let paragraphs = document.getElementsByTagName("p");
let boxes = document.querySelectorAll(".box");
```
### Манипуляция с DOM:
``` javascript
heading.textContent = "New Heading";
heading.style.color = "blue";

let newParagraph = document.createElement("p");
newParagraph.textContent = "This is a new paragraph.";
document.body.appendChild(newParagraph);
```

### Обработка событий:
``` javascript
let button = document.getElementById("my-button");
button.addEventListener("click", function() {
  console.log("Button was clicked!");
});
```
# 8. ООП
JavaScript, в отличие от того же Java, является прототипно-ориентированным языком, что означает, что объекты создаются напрямую, а не с использованием классов.

## Прототипное наследование
В программировании мы часто хотим взять что-то и расширить.

Например, у нас есть объект user со своими свойствами и методами, и мы хотим создать объекты admin и guest как его слегка изменённые варианты. Мы хотели бы повторно использовать то, что есть у объекта user, не копировать/переопределять его методы, а просто создать новый объект на его основе.

Прототипное наследование — это возможность языка, которая помогает в этом.

В JavaScript объекты имеют специальное скрытое свойство [[Prototype]], которое либо равно null, либо ссылается на другой объект. Этот объект называется «прототип»:

Прототип даёт нам немного «магии». Когда мы хотим прочитать свойство из object, а оно отсутствует, JavaScript автоматически берёт его из прототипа. Это называется «прототипным наследованием».

Свойство [[Prototype]] является внутренним и скрытым, но есть много способов задать его.

Одним из них является использование __proto__:

```js
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};
rabbit.__proto__ = animal;
```
Если мы ищем свойство в rabbit, а оно отсутствует, JavaScript автоматически берёт его из animal.

```js
let animal = {
  eats: true
};
let rabbit = {
  jumps: true
};
rabbit.__proto__ = animal; 
// теперь мы можем найти оба свойства в rabbit:
console.log( rabbit.eats ); // true (**)
console.log( rabbit.jumps ); // true
```

## Функции-конструкторы
 И изначально js отрицал саму идею ооп и продвигал функциональную парадигму:
``` javascript
// Литерал объекта
const person = {
    name: "John"
}; //Просто обычный объект
// Функция-конструктор
function Person(name) {
    this.name = name;
} // А это уже является классом
const person = new Person("John");
```
## ES6 Классы
Синтаксис функций-конструкторов не дружелюбен к разработчику из-за чего после серии бунтов и волнений в среде разработчиков в 2015 году ecma представили Классы ES6, которые не вносили сильных изменений в движок языка, но при этом добавляли “синтаксический сахар”  поверх функций-конструкторов, делающий их крайне похожими на классы java и более удобными для использования.
``` javascript
class Person {
    constructor(name) {
        this.name = name;
    }
    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}

class Employee extends Person {
    constructor(name, salary) {
        super(name);
        this.salary = salary;
    }
    set salary(s) {
this._salary = s}
    get salary() {
        return this._salary ;
    }
}
const employee = new Employee("John", 50000);
employee.greet(); // Hello, my name is John
employee.salary; // 50000 - getter
employee.salary = 100; // 50000 - setter
employee.salary; // 100 - getter
```
Но как я и упоминал, класс в js это обертка функции-конструктора, но давайте разберем это подробней.
``` js
class User {
  constructor(name) { this.name = name; }
  sayHi() { alert(this.name); }
}
```
Вот что на самом деле делает конструкция class User {...}:

Создаёт функцию с именем User, которая становится результатом объявления класса. Код функции берётся из метода constructor (она будет пустой, если такого метода нет).

Сохраняет все методы, такие как sayHi, в User.prototype.

При вызове метода объекта new User он будет взят из прототипа, как описано в главе F.prototype. Таким образом, объекты new User имеют доступ к методам класса.

### Доступ к свойствам и методам
В Java доступ к полям и методам класса регулируется модификаторами доступа, таких как public, private и protected. В JavaScript нет встроенной поддержки модификаторов доступа, но можно использовать различные паттерны для достижения того же эффекта.
``` javascript
class Person {
    #name; // Private field (ES2022)
    static thing = ‘something’; //статическое поле доступное только для класса
    constructor(name) {
        this.#name = name;
    }
    setName(name) {
        this.#name = name;
    }
    getName() {
        return this.#name;
    }
}
```
В ES2022 был введен синтаксис для приватных полей, обозначаемых #. Это позволяет достичь того же эффекта, что и private модификатор доступа в Java.
# 9. Асинхронное программирование: Promise, async/await:
Асинхронное программирование в JavaScript необходимо для выполнения операций, которые могут занять продолжительное время, не блокируя основной поток выполнения кода. Это важно, чтобы обеспечить плавность работы приложения и отзывчивость пользовательского интерфейса.
Колбэки
Изначально для организации асинхронных операций использовались колбэк-функции:
``` javascript
getData(function(a) {
  getMoreData(a, function(b) {
    getMoreData(b, function(c) {
      getMoreData(c, function(d) {
        getMoreData(d, function(e) {
          // Чето делается с данными
        });
      });
    });
  });
});
```
Нравится зрелище? Вот и программистам не нравилось и они дали соответствующие название "callback hell" - вложенность колбэков, оно затрудняло понимание и поддержку кода. 

## Promises
Для решения этой проблемы была введена концепция Promises. Promises представляют собой объекты, которые представляют результат асинхронной операции. Они имеют три состояния: 
1. Pending - начальное состояние, когда асинхронная операция еще не завершена.
2. Fulfilled - асинхронная операция успешно завершена, и Promise содержит результат.
3. Rejected - асинхронная операция завершилась с ошибкой, и Promise содержит причину ошибки.
Создание Promise
Promises создаются с помощью конструктора new Promise(). Конструктор принимает функцию-исполнитель, которая получает два аргумента - resolve и reject:
``` javascript
const myPromise = new Promise((resolve, reject) => {
  // Выполняем асинхронную операцию
  setTimeout(() => {
    if (/* условие успеха */) {
      resolve('Success!');
    } else {
      reject('Failure!');
    }
  }, 2000);
});
```
### Использование Promise
``` javascript
myPromise
  .then(result => {
    console.log(result); // 'Success!'
  })
  .catch(error => {
    console.error(error); // 'Failure!'
  });
```
Метод .then() позволяет обрабатывать успешное завершение Promise, а .catch() - обрабатывать ошибки
### Цепочки Promise
``` javascript
getData()
  .then(a => getMoreData(a))
  .then(b => getMoreData(b))
  .then(c => getMoreData(c))
  .then(d => getMoreData(d))
  .then(e => {
    // Чето делается с данными
  })
  .catch(error => {
    // Ловим ошибки  });
```
А что насчет этого вида? Сразу понятно, что из чего идет и куда заходит. Использование Promises позволяет избежать "callback hell" и делает код более читаемым и понятным.
### async/await и Обработка ошибок 
Для дальнейшего упрощения работы с асинхронными операциями в JavaScript были введены ключевые слова async и await. Функции, помеченные как async, могут использовать await для ожидания завершения асинхронных операций, представленных Promises. И вместе с этим правильная обработка ошибок в асинхронном коде очень важна. Для этого можно использовать конструкцию try/catch в сочетании с async/await или методы catch() для Promises.
``` javascript
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}
getData();
await ожидает завершения Promise, а async гарантирует, что функция вернет Promise.
Использование async/await делает асинхронный код более последовательным и простым для понимания.
```
### Параллельное выполнение
Иногда необходимо выполнять несколько асинхронных операций параллельно, чтобы повысить производительность. Для этого можно использовать методы Promise.all(), Promise.race() и Promise.allSettled().
``` javascript
async function getData() {
  try {
    const [a, b, c] = await Promise.all([
      getData1(),
      getData2(),
      getData3(),
    ]);
    // чето делаем с данными
  } catch (error) {
    // ошибки
  }
}
getData();
```
В этом примере три асинхронные операции (getData1(), getData2() и getData3()) выполняются параллельно, а результаты помещаются в массив [a, b, c] после завершения всех операций.

# 9. Модули в JavaScript:
В программировании проектов больших нежели чем какой-то калькулятор, а также во всех фреймворках используются модули – т.е. разбиение кода на логические части и вынесение их на отдельные файлы. 
В ранних версиях JavaScript не было встроенной поддержки модульной структуры. Разработчики использовали различные подходы, такие как глобальные пространства имен или объекты-синглтоны, для организации своего кода. Однако, по мере того как проекты становились все более сложными, возникла потребность в более структурированном и масштабируемом способе управления зависимостями и разделения кода.
## CommonJS-модули:
Для решения этой проблемы была разработана спецификация CommonJS, которая определяет механизм импорта и экспорта модулей. В CommonJS, каждый файл представляет собой отдельный модуль, и для доступа к другим модулям используется require() функция.
``` javascript
// Файл: math.js
exports.add = (a, b) => a + b;
exports.subtract = (a, b) => a - b;
// Файл: app.js
const math = require('./math');
console.log(math.add(5, 3)); // 8
console.log(math.subtract(10, 4)); // 6
```
Изредка используется, но по большей части забытый синтаксис
## ECMAScript-модули:
В столь прекрасном 2015 ecma также обновили модульную систему. ES-модули используют ключевые слова import и export для управления зависимостями.
``` javascript
// Файл: math.js
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
// Файл: app.js
import { add, subtract } from './math';  //пример деструктуризации
console.log(add(5, 3)); // 8
console.log(subtract(10, 4)); // 6
```
### Импорт и экспорт по умолчанию
В дополнение к именованным экспортам, ES-модули также поддерживают экспорт и импорт по умолчанию.
``` javascript
// file1.js
export default {
    message: "Hello, world!"
};
// file2.js
import myModule from './file1';
console.log(myModule.message); // "Hello, world!"
```
### Динамический импорт
ES2020 добавил поддержку динамического импорта, которая позволяет импортировать модули по запросу, а не при загрузке приложения.
``` javascript
async function loadModule() {
    const module = await import('./file1');
    console.log(module.message);
}
loadModule(); // "Hello, world!"
```
# JS фреймворки
В современном мире веб-разработки простого "ванильного" JavaScript уже недостаточно для создания сложных, интерактивных и динамических пользовательских интерфейсов. Разработчики сталкиваются с необходимостью решать множество повторяющихся задач, таких как управление состоянием приложения, оптимизация производительности, маршрутизация и многое другое.

Это именно то, где на помощь приходят JavaScript-фреймворки. Они предлагают готовую инфраструктуру и инструменты, значительно упрощающие и ускоряющие разработку. Фреймворки также обеспечивают последовательность и поддерживаемость кода, что особенно важно в крупных проектах с командой разработчиков.

Давайте теперь рассмотрим три наиболее популярных JavaScript-фреймворка - React, Vue.js и Angular

## react
Начнем с React - детища Фейсбука, появившегося на свет в 2013 году. React сразу же покорил сердца разработчиков своим уникальным подходом к построению интерфейсов. Вместо использования традиционного HTML, React предлагает JSX - специальный синтаксис, который позволяет писать код, похожий на HTML, прямо внутри JavaScript. 
HelloWorld.js
``` js
function HelloWorld() {
  return (
    <div>
      <h1>Hello, World!</h1>
    </div>
  );
}
```
Реакт сейчас использует функциональный подход, где каждый компонент — это функция.
Так это функция HelloWorld в дальнейшем может использоваться как тег <HelloWorld / > 
## vue
А что насчет Vue.js? Этот фреймворк появился годом позже, в 2014-м, и сразу же стал отличной альтернативой React. Vue.js использует собственный шаблонный синтаксис, который выглядит более знакомо для разработчиков, привыкших к традиционному HTML. 
HelloWorld.vue
``` javascript
<template>
  <div>
    <h1>Hello, {{ name }}!</h1>
  </div>
</template>
<script>
name = ref(‘world!’);
</script>
```
Простота и интуитивность Vue.js делают его отличным выбором для разработчиков, которым нужно быстро изучить синтаксис и сразу начать писать код.
## angular
И наконец, давайте обратимся к Angular - мощному фреймворку, созданному компанией Google. Первая версия Angular появилась в 2010 году, а в 2016-м вышел Angular 2+, который радикально отличался от предыдущей версии. Angular использует TypeScript - надстройку над JavaScript, которая добавляет статическую типизацию и другие полезные возможности. Вот пример компонента на Angular:
``` javascript
import { Component } from '@angular/core';

@Component({
  selector: 'app-hello-world',
  template: `
    <h1>Hello, {{ name }}!</h1>
  `
})
export class HelloWorldComponent {
  name = 'World';
}
```
Angular, в отличие от React и Vue.js, является полноценным фреймворком, предоставляющим всю необходимую инфраструктуру для разработки крупных enterprise-приложений. Его сложность может быть барьером для новичков, но опытные разработчики ценят мощь и гибкость этого инструмента.

Каждый из этих фреймворков имеет свои сильные и слабые стороны. React отличается высокой производительностью и гибкостью, Vue.js - простотой и интуитивностью, а Angular - мощностью и комплексностью.
