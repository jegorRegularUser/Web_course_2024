# Введение в React.js

## Что такое React.js?

React.js — это библиотека JavaScript для создания пользовательских интерфейсов, разработанная Facebook. Она позволяет разработчикам создавать многоразовые компоненты, которые могут управлять своим состоянием и эффективно обновлять интерфейс при изменении данных. React использует виртуальный DOM, что обеспечивает высокую производительность при обновлении интерфейса.

## Основные особенности React.js:

- **Компонентная архитектура**: React позволяет разбивать интерфейс на независимые компоненты, что упрощает разработку и повторное использование кода.

- **Однонаправленный поток данных**: Данные в React передаются сверху вниз, что облегчает понимание структуры приложения и управление состоянием.

- **Хуки**: React предоставляет хуки, которые позволяют использовать состояние и другие функции без написания классов.

- **Виртуальный DOM**: React создает виртуальное представление DOM, что позволяет минимизировать количество операций с реальным DOM и улучшить производительность.

## Установка React приложения

Для начала работы с React необходимо установить Node.js и npm. После установки можно создать новое React приложение с помощью Create React App. 

1. Установите Node.js с [официального сайта](https://nodejs.org/en).
2. Откройте терминал и выполните команду:

```bash
   npx create-react-app project-name
```

После для перехода в эту папку прописывайте 
``` bash
  cd project-name
```
Для установки всех зависимостей и создания папки node_modules - откуда будут браться все функции и объекты, необходимые для разработки
 ``` bash
  npm install
```
И наконец для запуска вашего проекта vue на сайте
``` bash
  npm run start
```

# Основы react(функциональные компоненты, состояния, пропсы)
## Структура
Посмотрев в папку проекта, мы увидем следующее:
![alt text](./assets/structure.png)
Давайте немного расскажу об этом
#### Папка public
Используется для добавления каких-то публичных данных, обычно для иконки сайта ![alt text](./assets/image-3.png)
#### Папка src
Здесь будут находится главное содержание вашего проекта, а именно
#### Папка assets
Здесь добавляются все изображения, иконки и тому подобные ресурсы.
#### Папка components
Здесь будут добавляться ваши компоненты, и я сразу же хочу обсудить этот момент. В среде разработчиков принято писать все понятно и не кидать все яйца в одну корзину, так что, если вы хотите делать большой проект, то начните с прописи иерархии: если у вас есть обширная страница home, то создайте для нее отдельную папку, если в ней есть повторяющиейся код - вынесите его в отдельный компонент и создайте для таких компонетов отдельную папку и тд.
#### App.css
Просто кастомный файл для стилей компонента App.
#### App.js
Главный компонент в который в последствии мы будем добавлять собственные.
#### App.test.js
Файл для unit-тестов.
#### index.css
root файл стилей.
#### index.js
Файл иницилирующий js часть.

### Файл Package.json
И последним важным для нас этот файл, здесь вы можете поменять имя своего проекта, прописать все зависимости и также посмотреть с помощью каких команд вы можете запустить ваш сайт в браузере(start)

## Функциональные компоненты
В react существует для вида компонентов классовые(устаревшие) и функциональные, о первых я рассказывать не буду, так как в сравнении с функциональными работы с ними идет сложнее и дольше, и в следствии этого сейчас никто уже и не пользуется классовыми компонентами.

Обычный вид компонента:
``` js
import "./styles.css";

export default function App() {
  return (
    <div className="App">
      <h1>Hello world!</h1>
    </div>
  );
}

```

Главной частью является функция, одноименная с названием файла, она возвращается jsx код - синтаксический сахар для функции React.createElement(type, props, ...children)

Альтернативой без JSX послужил бы подобный вырвеглазныый код:
``` js
function UserProfile() {
return React.createElement('div', null,
React.createElement('h1', null, user.name),
React.createElement('p', null, user.status),
React.createElement('img', {
src: user.avatar, width: '50', height: '50', alt: user.name +
' avatar'
}),
);
}
```

### JSX: ключевые моменты
1. JSX — не HTML, все теги нужно закрывать
2. При использовании JSX обязательно импортировать React
3. В JSX можно использовать переменные(expassions), если обернуть их в фигурные скобки
4. Нельзя использовать if, циклы, можно — тернарный оператор и map
5. Для css-классов свойство className
6. JSX на верхнем уровне может содержать только один элемент

и давайте покажу все это на примере:

``` js
function App() {
  const selected = "Portfolio";
  const btns = ["Portfolio", "Layouts"].map((el, index) => {
    return (
      <button
        className={el === selected ? "btn styled" : "btn"}
        onClick={()=>{console.log(el)}}
        key={index}
      >
        {el}
      </button>
    );
  });
  return (
    <div className="App">
      <div className="tollbar">{btns}</div>
      {selected==="Portfolio" ? <Portfolio />:''}
      {selected==="Layouts" ? <Store/> :''}
    </div>
  );
}
export default App;
```
### Кастомные компоненты
Все что нужно сделать для собственного компонента это создать отдельный файл YourComponent.js(все компоненты принято пистаь с большой буквы) и внутри него создать функцию
``` js
function YourComponent() {
  return (
     <div>Твой компонент</div> 
  );
}
export YourComponent
```
И поздравляю, после этого нужно будет лишь прописать в том компоненте, куда мы хотим добавить YourComponent:
``` js
import YourComponent from "./путь-к-YourComponent/YourComponent.js";
function App() {
  return(
 <YourComponent/>
  )
}
export default App;
```

### Events(события)
И я хочу начать с самого легкого - взаимодействия с элементами.
Покажу это на примере кнопки, в jsмы добавляли логику кнопке вот так:
``` js
document.querySelector('btn').addEventListener('click',()=>{console.log()})
```
В react же это делать теперь проще, потому что событие и реакцию на него мы будет прописывать сразу же в теге кнопки
``` js
function App() {
  return (
     <button onClick={()=>{console.log('Ты на меня нажал!')}} >
        Нажми меня
      </button>
  );
}
export default App;
```
У каждого элемента теперь есть события в виде аттрибутов, и также можно вместо стрелочной функции просто писать название уже созданной.
``` js
function App() {
   const  clickOnMeBtnHandler = () =>{console.log('Ты на меня нажал!')}
  return (
     <button onClick={clickOnMeBtnHandler} >
        Нажми меня
      </button>
  );
}
export default App;
```
И в среде разработчиков принято, не считая общей понятности названий, добавлять к функциям, которые будут использоваться при нажатии кнопок, приписку Handler.

Самих событий бесчисленное множество и каждое событие как и в js возвращает соответсвующий event.
![alt text](./assets/eventAmountExample1.png)
![alt text](./assets/eventAmountExample2.png)

### State(состояния)

Основным преимуществом фреймворков является реактивность - способность изменять dom сайта без обновления страницы, в react это можно реализовать за счет использвоания специальных функций - хуков, а конкретней хука useState.

сам по себе это хук возвращает массив, имеющий изменяемое состояние stateName и функцию его изменяющее setStateName, но лучше все показать на примере:
``` js
import { useState } from "react";
function App() {
  const [count, setCount] = useState(0);// дефолтным значением count является 0, так как мы вложили это в useState
  
  return (
    <div>
      <button onClick={setCount(count+1)}>Нажимая на меня ты увеличиваешь число {count}</button>
    </div>
  );
}
```
И данный пример выдаст ошибку, потому что при изменении count происходит перестройка dom, но, так-как мы вложили button setCount с аргументом, то эта функция сразу же вызывается, что обновляет dom, что обновляет button, что вызывает функцию setCount, что обновляет dom... И чтобы это решить нужно либо вынести все в отдельную функцию, либо сразу же вложить setCount в стрелочную функцию прямо в button
``` js
import { useState } from "react";
function App() {
  const [count, setCount] = useState(0);
  
  return (
    <div>
      <button onClick={()=>{setCount(count+1)}}>Нажимая на меня ты увеличиваешь число {count}</button>
    </div>
  );
}
```
![alt text](./assets/btnstateexample.png)
И вот, теперь мы можем добавлять реактивность на сайт


### Props
Все это, конечно, хорошо, но что делать с ситуацией, когда нам нужно передать данные по компонентам? 
Рrops выступит решением, потому что это аргументы создаваемых функций, пример:

``` js
//App.js
import "./App.css";
import ShopItem from "./components/ShopItem";

const item = {
  brand: "Tiger of Sweden",
  title: "Leonard coat",
  description: "Minimalistic coat in cotton-blend",
  descriptionFull:
    "Men's minimalistic overcoat in cotton-blend. Features a stand-up collar, concealed front closure and single back vent. Slim fit with clean, straight shape. Above-knee length.",
  price: 399,
  currency: "£",
};

function App() {
  return (
    <div className="container">
      <img className="image" src={img} alt="." />
      <div className="window">
          <ShopItem item={item} /> //здесь мы передаем данные в компонент
      </div>
    </div>
  );
}

export default App;

``` 

``` js
//ShopItem.js
function ShopItem(props) {//здесь мы получаем данные в виде объекта props
  const { brand, title, description, descriptionFull, price } = props.item; //props имеет поля - те самые аттрибуты, в которые мы передавали необходимые данные
  return (
    <div class="main-content">
      <h2>{brand}</h2>
      <h1>{title}</h1>
      <h3>{description}</h3>
      <div class="description">{descriptionFull}</div>
      <div class="divider"></div>
      <div class="purchase-info">
        <div class="price">£{price.toFixed(2)}</div>
        <button>Добавить в корзину</button>
      </div>
    </div>
  );
}

export default ShopItem;
```
![alt text](./assets/propsExample.png)
Как вы видите из примера, для передачи данных нам нужно прописать в родительском компоненте некий аттрибут для дочернего и присвоить ему необходимые данные
``` js
//App.js
   ...
   <ShopItem  item={item} />//ShopItem-дочерний, item-аттрибут, item(который справа)-данные
   ...
```
И уже в самом компоненте мы принимаем props как аргумент функции и он имеет в качестве полей эти самые аттрибуты.
Также можно поступить легче, если у нас много аттрибутов и деструктиризировать props сразу на приемке
``` js
//ShopItem.js
function ShopItem( { item } ) {
  const { brand, title, description, descriptionFull, price } = item;
  return (
    ...
  );
}
export default ShopItem;
```
`
Props предназначены только для чтения.
Ни в каком случае не следует их изменять!
`
#### Поднятие данных в родительский компонент
И после того как мы передали данные вниз в дочерний компонент, возникает вопрос: а как тогда их поднять наверх?
Так как props нельзя менять, мы можем просто создать функцию, которая и будет принимать в себя необходимые данные:
``` js
function App() {
const getDataFromShopItem = (data)=>{
  console.log('Из ShopItem мы получили: ', data)
}
  return (
    <div>
      <ShopItem getData={getDataFromShopItem}/>
    </div>
  );
}

export default App;
```
``` js
function ShopItem({getData}) {
    const data = 'данные из ShopItem'
    getData(data);
    return (
      <div>
      </div>
    );
  }
  export default ShopItem;
  
```
![alt text](./assets/propsConsoleLog.png)

#### Атрибуты без значений
Также мы можем писать аттрибуты без значения, они автоматически будут принимать значение true:
``` js
function App() {
  return (
    <>
    <ShopItem colored/>
    <ShopItem colored={true}/>
    <ShopItem colored={false}/>
    </>
  );
}
export default App;
```
``` js
function ShopItem({colored}) {
    return (
      <div style={{color:`${colored? 'blue': 'black'}`}}>
        {`${colored}`}
      </div>
    );
  }
  export default ShopItem;
```
![alt text](./assets/noValueAttributeProppsExample.png)

#### defaultProps
Свойство компонента defaultProps позволяет задать значения атрибутов по умолчанию.
Для этого достаточно присвоить объект в это свойство компонента, где ключ будет именем атрибута, а значение — значением, которое будет передаваться в props компонента, если атрибут не задан.
``` js
function UserInfo({ name, img }) {
  return (
    <div className="card">
      <img src={img} className="card-img-top" alt="..." />
      <div className="card-body">
        <h6 className="card-title">{name || "Гость"}</h6>
      </div>
    </div>
  );
}

UserInfo.defaultProps = {
  img: "https://dummyimage.com/100x100/000/ffffff&text=default",
};
export default UserInfo;
```

### Некоторые безтемные примеры 
#### Списки
Списки достаточно часто используемый элемент, имеющий особенность в jsx, а именно необходимость индетификации каждого элемента списка с помощью аттрибута key:
``` js
<ul>
  <li key="1">Ларичев Иван</li>
  <li key="2">Морозов Алексей</li>
  <li key="3">Бурмистров Роман</li>
</ul>
<ul>
  <li key="1">Болдырева Анастасия</li>
  <li key="2">Чичев Александр</li>
  <li key="3">Егоров Николай</li>
</ul>
```
И бывают ситуации, когда мы имеем массив данных и нам нужно превратить его в список, для этого мы спокойно можем использовать метод map:
``` js
function ShopItem() {
  const arrOfData = [
    "Ларичев Иван",
    "Морозов Алексей",
    "Иванова Анна",
    "Сидоров Николай",
    "Петрова Светлана",
    "Кузнецов Роман",
    "Федорова Екатерина",
    "Смирнов Сергей",
    "Романов Дмитрий",
    "Зайцева Юлия",
  ];
  const listOfNames = arrOfData.map((el) => {
    return 
    <li key={el + Math.random()}> // Люди, знающие метод map, могут заметить, что можно было бы использовать index
      {el}                       // Однако это плохая практика - это может помешать нормальной работе алгоритма сопоставления в React(и в других фреймворках)
    </li>;                      // Лучше всего использовать собственные текстовые id
  });

  return (
    <ul >
     {listOfNames}
    </ul>
  );
}
export default ShopItem;

```
#### Тернарный оператор
Тернарным оператором вы будете пользоваться постоянно, из-за того, что jsx допускает только expressions:
Переключение стилей:
``` js
    return (
      <div style={{color:`${colored? 'blue': 'black'}`}}>
        {`${colored}`}
      </div>
    );
    ...
    <button
			className={`enter ${players.length < 5 ? 'noDisplay' : ''}`}
			onClick={startGame}
		>
			Начать игру
		</button>
```
Переключение компонентов(или их не включение):
``` js
function App() {
  const selected = "Portfolio";
  const btns = ["Portfolio", "Layouts"].map((el, index) => {
    return (
      <button
        className={el === selected ? "btn styled" : "btn"}
        onClick={()=>{console.log(el)}}
        key={index}
      >
        {el}
      </button>
    );
  });
  return (
    <div className="App">
      <div className="tollbar">{btns}</div>
      {selected==="Portfolio" ? <Portfolio />:''}
      {selected==="Layouts" ? <Store/> :''}
    </div>
  );
}
export default App;
```
#### Использование высшего булина
Последний пример с 'не включением компонентов' можно сделать по-умнее, буквально используя логику:
``` js
function App() {
  const selected = "Portfolio";
  const btns = ["Portfolio", "Layouts"].map((el, index) => {
    return (
      <button
        className={el === selected ? "btn styled" : "btn"}
        onClick={()=>{console.log(el)}}
        key={index}
      >
        {el}
      </button>
    );
  });
  return (
    <div className="App">
      <div className="tollbar">{btns}</div>
      {selected==="Portfolio" && <Portfolio />} // при условии, что нам не нужно иметь альтернативу при false значении
      {selected==="Layouts" && <Store/> }
    </div>
  );
}
export default App;
```
#### input, ref
В будущих обновлениях: как работать с input, формы, роутер, использование вместе с typescript(по сути здесь просто рассказать, что можно использовать typescript и разграничить приложение с примерами на хуках и функциях)