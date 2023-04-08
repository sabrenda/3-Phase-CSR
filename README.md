# [3-Phase-CSR]

<div id="gear-menu"></div>

## ⚙️ Menu
  
| # | React Hooks/Components [#](#react-hooks) | link | React Router [#](#react-router) | link |
|:-:|:-----------------:|:------------------:|:-------------------:|:------------------:|
|1| **useState** | [#](#usestate) | ----------**BrowserRouter**---------- | [#](#1-browserrouter) |
|2| **useEffect** | [#](#useeffect) | --------------**Routes**-------------- | [#](#2-routes) |
|3| **useCallback** | [#](#usecallback) | ---------------**Route**--------------- | [#](#3-route) |
|4| **useMemo** | [#](#usememo) | ---------------**Outlet**--------------- | [#](#4-outlet) |
|5| **useContext** | [#](#usecontext) | -----------**Link / NavLink**----------- | [#](#5-link-navLink) |
|6| **useReducer** | [#](#usereducer) | -**Navigate / useNavigate / Redirect**- | [#](#6-navigate-redirect-usenavigate) |
|7| **React memo** | [#](#react-memo) | ------------**useParams**------------ | [#](#7-useparams) |

- **INIT** [🔽](#init)
- **Event handlers** [🔽](#event-handlers)
- **Примеры кода** [🔽](#примеры-кода)

**Доп библиотеки** [в процессе...]
1. Axios
2. Redux
3. Redux/toolkit
4. Redux/Saga
5. Prisma ORM

---
Документация по React
- **React.dev** | [link](https://react.dev/)
- **React Router** | [link](https://reactrouter.com/en/main)
- **w3schools** [link](https://www.w3schools.com/react/default.asp)
---

---
---
## Init
- `npx create-react-app client` | [Create React App](https://create-react-app.dev/)
- `npx create-react-app client --template typescript` | [on TypeScript](https://create-react-app.dev/)
- `npm i react-router-dom` | [React Router](https://reactrouter.com/en/main)
- `npm i redux react-redux @redux-devtools/extension @reduxjs/toolkit` | [redux](https://redux.js.org/) | [devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) | [toolkit](https://redux-toolkit.js.org/)

## 🧑‍🎨 Style 
- **MUI** | [перейти](https://mui.com/)
- **Tailwindcss** | [перейти](https://tailwindcss.com/docs/installation)
- **Reactstrap** | [перейти](https://reactstrap.github.io/?path=/story/home-installation--page)

---
---
# React Hooks

### [useState]
[**официальная документация**](https://react.dev/reference/react/useState)

**useState**  *— это хук (hook) в React, который позволяет добавлять локальное состояние в функциональные компоненты.* **useState** *принимает начальное значение состояния и возвращает массив из двух элементов: текущее состояние и функцию для обновления этого состояния.*

-  `initialState = []` | начальное состояние
-  `const [state, setState] = useState(initialState);` | state — текущее значение состояния
-  `setState((prev) => [...prev, 'hello']);` | setState — функция для обновления состояния. При вызове этой функции с новым значением состояние будет обновлено, а компонент перерендерится.

**[Пример кода](#useState)** | [Menu](#gear-menu)

---

### [useEffect]
[**официальная документация**](https://react.dev/reference/react/useEffect)

**useEffect** *— это хук (hook) в React, который позволяет выполнять побочные эффекты, такие как запросы к серверу, подписки на события или обновление DOM в функциональных компонентах.* **useEffect** *принимает функцию, которая выполняет побочные эффекты, и массив зависимостей, указывающий, при каких изменениях эффект должен повторно выполняться*
```js
useEffect(() => {  // Выполнение побочного эффекта
  
  return () => {     // Очистка побочного эффекта (необязательно)
  };
 
}, [dependencies]);  // Массив зависимостей (необязательно)
```
❗️**обязательный параметр**

**Функция**: функция, в которой выполняется побочный эффект

❗️**Опциональный**

**Массив зависимостей**: *Массив зависимостей, содержащий все переменные, от которых зависит функция. React будет вызывать функцию эффекта только тогда, когда значения зависимостей изменятся. Если массив зависимостей пуст, функция эффекта будет вызываться только при монтировании и размонтировании компонента.*

**Return** - *Функция эффекта может возвращать функцию очистки. Эта функция вызывается перед размонтированием компонента или когда какая-либо из зависимостей изменяется. Функция очистки используется для отмены действий, выполненных в функции эффекта, например, отписки от событий, очистки таймеров и т. д.*

**[Пример кода](#useEffect)** | [Menu](#gear-menu)

---

### [useCallback]
[**официальная документация**](https://react.dev/reference/react/useCallback)

**useCallback** *— это хук в React, который позволяет мемоизировать (кэшировать) функции-обработчики событий или другие функции внутри функционального компонента. Это полезно для оптимизации производительности, особенно при работе с компонентами, которые часто ререндерятся или имеют оптимизированных дочерних компонентов (например, обернутых в React.memo).*

**❗️обязательный параметр**

**Функция**: *Функция, которую нужно мемоизировать*

**❗️Опциональный**

**Массив зависимостей**: *Массив зависимостей, содержащий все переменные, от которых зависит функция*

**❗️️Return** - *useCallback возвращает мемоизированную версию переданной функции, которая изменяется только тогда, когда значения зависимостей изменяются. Это предотвращает создание новых ссылок на функции при каждом ререндере и, таким образом, предотвращает ненужные ререндеры дочерних компонентов.*

```js
import React, { useState, useCallback } from 'react';

const ExampleComponent = () => {
  const [count, setCount] = useState(0);

  const incrementCount = useCallback(() => {
    setCount((prevCount) => prevCount + 1);
  }, []);
  
  // Здесь мы можем использовать incrementCount, например, как обработчик событий для кнопки
};
```
*В этом примере, функция incrementCount мемоизируется с помощью useCallback. Зависимостей у функции нет, поэтому массив зависимостей пуст. Это означает, что incrementCount будет создана только один раз при первом рендере, а при последующих ререндерах будет использоваться мемоизированная версия функции.*

**[Пример кода](#useCallback)** | [Menu](#gear-menu)

---

### [useMemo]
[**официальная документация**](https://react.dev/reference/react/useMemo)

**useMemo** *- это хук в React, который используется для мемоизации вычисляемых значений, зависящих от некоторых зависимостей. Это позволяет избежать повторных вычислений при каждом рендере компонента, если зависимости не изменились. Коротко говоря useMemo запоминает выполнение функции.*

**❗️обязательный параметр**

**Функция**: *которая вычисляет значение, которое нужно мемоизировать. Эта функция вызывается только тогда, когда значения зависимостей изменяются.*

**❗️Опциональный**

**Массив зависимостей**: *Массив зависимостей, содержащий все переменные, от которых зависит функция*

**❗️️Return** - *useCallback возвращает мемоизированную версию переданной функции, которая изменяется только тогда, когда значения зависимостей изменяются.*

```js
import React, { useState, useMemo } from 'react';

const computeExpensiveValue = (a, b) => {
  // Здесь может быть дорогостоящая операция
  return a + b;
};

const ExampleComponent = () => {
  const [num1, setNum1] = useState(0);
  const [num2, setNum2] = useState(0);

  const expensiveValue = useMemo(() => {
    return computeExpensiveValue(num1, num2);
  }, [num1, num2]);

  // Здесь мы можем использовать expensiveValue, например, для отображения его значения или передачи другим компонентам
};
```

*В этом примере, функция incrementCount мемоизируется с помощью useCallback. Зависимостей у функции нет, поэтому массив зависимостей пуст. Это означает, что incrementCount будет создана только один раз при первом рендере, а при последующих ререндерах будет использоваться мемоизированная версия функции.*

**[Пример кода](#useMemo)** | [Menu](#gear-menu)

---

### [useContext]
[**официальная документация**](https://react.dev/reference/react/useContext)

**useContext** *- это хук в React, который позволяет функциональным компонентам подписываться на контекст и получать его значения. Контекст используется для передачи данных через дерево компонентов без необходимости передавать пропсы на промежуточных уровнях. Это особенно полезно для передачи глобальных данных, чтобы избежать пропс дриллинга.*

- *Для использования useContext, вам сначала нужно создать контекст с помощью функции React.createContext(): создаем файл в папке Context/Usercontext.jsx*

```js
import React from 'react';

const UserContext = React.createContext();
```
- *Затем вы можете использовать компонент UserContext.Provider для оборачивания частей дерева компонентов, которым должны быть доступны данные контекста:*
```js
import React from 'react';
import UserContext from './UserContext';

const App = () => {
  const [user, setUser] = React.useState();

  return (
    <UserContext.Provider value={user}>
      {Здесь ваше дерево компонентов, которым доступен контекст}
    </UserContext.Provider>
  );
};

export default App;
```

- *Теперь вы можете использовать хук useContext в функциональных компонентах для доступа к данным контекста:*

```js
import React, { useContext } from 'react';
import UserContext from './UserContext';

const UserComponent = () => {
  const user = useContext(UserContext);

  return <div>My name is {user}</div>;
};

export default UserComponent;
```

- *В этом примере мы импортируем контекст UserContext и используем хук useContext для получения текущей темы. Теперь компонент UserComponent может реагировать на изменение темы, не нуждаясь в пропсах для передачи данных о теме.*

**❗️обязательный параметр**

**Контекст** - *Это контекст, который был создан с помощью функции React.createContext(). Вы должны передать этот контекст в качестве аргумента при вызове useContext.*

**❗️️Return**:  *useContext возвращает текущее значение контекста для ближайшего Provider данного контекста в дереве компонентов. Если нет соответствующего Provider, то возвращается значение по умолчанию, которое было указано при создании контекста с помощью React.createContext().*

[Menu](#gear-menu)

---

### [useReducer]

[**официальная документация**](https://react.dev/reference/react/useReducer)

**useReducer** - *это хук в React, который позволяет управлять состоянием компонента с использованием понятия редуктора. Редуктор - это функция, которая принимает текущее состояние и действие, а затем возвращает новое состояние. useReducer особенно полезен для управления сложными состояниями или когда следующее состояние зависит от предыдущего.*

**useReducer** принимает два аргумента и один опциональный:

1. Редуктор: Это функция, которая принимает текущее состояние и действие, а затем возвращает новое состояние.
2. Начальное состояние: Это начальное значение состояния.
3. Инициализатор (опциональный): Это функция, которая принимает начальное состояние в качестве аргумента и возвращает начальное состояние, которое будет использоваться. Это может быть полезно, если вам нужно выполнить некоторые вычисления для определения начального состояния.

**useReducer** возвращает массив с двумя элементами:

1. Текущее состояние: Это текущее значение состояния, управляемое редуктором.
2. Функция dispatch: Эта функция используется для отправки действий, которые обрабатываются редуктором для обновления состояния.

Пример использования **useReducer**:

```js
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      <div>Count: {state.count}</div>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </>
  );
};

export default Counter;

```

В этом примере у нас есть начальное состояние { count: 0 } и редуктор, который обрабатывает два действия: increment и decrement. Мы используем useReducer с этим редуктором и начальным состоянием. Хук возвращает текущее состояние и функцию dispatch.

Кнопки вызывают функцию dispatch с соответствующими действиями. Редуктор обрабатывает эти действия и возвращает новое состояние. Обратите внимание, что состояние обновляется непосредственно в редукторе, и мы не вызываем setState или другой

[Menu](#gear-menu)

---

### [React memo]
[**официальная документация**](https://react.dev/reference/react/memo)

**memo** *— Это высокоуровневый компонент, который оборачивает функциональный компонент и предотвращает его ререндер, если пропсы (свойства) не изменились.* **React.memo** *сравнивает предыдущие и текущие пропсы с помощью поверхностного сравнения или кастомной функции сравнения. Если пропсы не изменились, React.memo предотвращает ререндер компонента и использует предыдущий результат рендеринга.* **React.memo** *полезен для оптимизации производительности функциональных компонентов, которые часто ререндерятся из-за изменения пропсов.*

**❗️обязательный параметр**

**Компонент**: Функциональный компонент, который вы хотите оптимизировать с помощью React.memo. React.memo оборачивает этот компонент и возвращает новый компонент с мемоизированным поведением.

**❗️(Опциональный)**
**Функция сравнения**: Функция, которая будет использоваться для сравнения предыдущих и текущих пропсов. Если функция сравнения не предоставлена, React.memo будет использовать поверхностное сравнение (shallow comparison). Функция сравнения принимает два аргумента – предыдущие пропсы и текущие пропсы – и должна вернуть true, если пропсы равны, и false, если они разные. Если функция возвращает true, React.memo не будет вызывать ререндер компонента.

**Пример кода:**

```js
import React, { useContext } from 'react';
import { Link } from 'react-router-dom';
import { UserContext } from '../../Context/User.context';

function PostListItem({ title, postId, userId, handleRemove }) {
  const { user } = useContext(UserContext);
  return (
    <div>
      <h4>{title}</h4>
      <Link to={`/post/${postId}`}>to details</Link>
      {user?.id === userId && <button type="button" onClick={() => handleRemove(postId)}>x</button>}
    </div>
  );
}
export default React.memo(PostListItem);
```

[Menu](#gear-menu)

---
---

### [React Router]
[**официальная документация**](https://reactrouter.com/en/main/start/tutorial)

**React-Router** - это библиотека маршрутизации, обеспечивает переход между различными компонентами React, когда пользователь взаимодействует с интерфейсом. react-router поддерживает маршрутизацию как на стороне клиента (client-side), так и на стороне сервера (server-side). **React-Router** предоставляет ряд компонентов и хуков, которые могут быть использованы для создания маршрутизации.

Некоторые из основных компонентов react-router включают:

---

### 1 BrowserRouter 

*Компонент-обёртка, который использует HTML5 History API для синхронизации UI с URL-адресом в браузере. Он обеспечивает базовую навигацию и должен быть помещен в корень вашего приложения, окружая все маршрутизируемые компоненты.*

---

### 2 Routes

используется для определения коллекции маршрутов в вашем приложении. Он предоставляет функциональность для выбора и отображения правильного маршрута на основе текущего URL.

**❗️обязательный параметр**

*children*: Обязательное свойство, определяющее дочерние маршруты, которые будут вложены в Routes. Обычно здесь размещаются компоненты *Route* для определения различных маршрутов

**❗️Опциональный**
*location*: Опциональное свойство, позволяющее передать собственный объект *location* для определения текущего маршрута. Это может быть полезно в редких случаях, когда вам нужно вручную контролировать местоположение вместо использования автоматического определения маршрута библиотекой react-router-dom.

[Пример кода](#route)

---

### 3 Route

пределяет сопоставление между URL-адресом и компонентом, который должен быть отображен при совпадении этого URL.

**❗️обязательный параметр**

*element* - Обязательное свойство, определяющее компонент, который будет отображаться при совпадении маршрута

**❗️Опциональный**

*path* - Опциональное свойство, определяющее путь URL, который будет сопоставлен с этим маршрутом. Путь может содержать параметры (например, :id). Если path не указан, маршрут будет считаться "пойманным всем" и будет рендериться, когда другие маршруты не совпадают.

*children* - свойство, используемое для определения дочерних маршрутов внутри родительского маршрута. Это полезно, когда вы хотите создать вложенную иерархию маршрутов.

*caseSensitive* - булево свойство, определяющее, будет ли маршрут учитывать регистр при сопоставлении путей. По умолчанию равно false, что означает, что маршрут будет сопоставляться без учета регистра.

*index* -  булево свойство, определяющее, будет ли данный маршрут считаться индексным маршрутом для своего родителя. Если true, маршрут будет отображаться, когда родительский маршрут точно совпадает с текущим маршрутом. По умолчанию равно false.

*strict* -  булево свойство, определяющее, будет ли маршрут точно сопоставляться с путем с учетом слеша / на конце. Если true, маршрут будет считаться совпадающим только в том случае, если слеш на конце пути будет соответствовать текущему маршруту. По умолчанию равно false.

[Пример кода](#route)

---

### 4 Outlet

используется для отображения дочерних маршрутов внутри родительского маршрута.

️Не имеет свойств.

---

### 5 Link NavLink

[ссылки]

####################################################################################

1. **[Link]** - Это базовый компонент для создания навигационных ссылок. Вместо использования тега <a>, используйте компонент Link с атрибутом to, указывающим на путь, куда должна вести ссылка.
  
❗️**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
  
❗️**Опциональный: ** "replace" или объект "state"
  
[Пример кода](#link)

####################################################################################

2. **[NavLink]** - похож на Link, но с дополнительной возможностью стилизации активных ссылок, автоматически применяет активный стиль или класс к ссылке, когда текущий маршрут соответствует маршруту, указанному в атрибуте to.
  
Это полезно для визуального отображения активных ссылок в вашем приложении.
  
❗️**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
  
❗️**Опциональный:** "replace", "activeClassName", "activeStyle", "exact",  или объект "state"
  
[Пример кода](#navlink)

####################################################################################

 ---
  
### 6 Navigate Redirect useNavigate

[перенаправление]

####################################################################################

1. **[Navigate]** - Это компонент, который автоматически перенаправляет пользователя на указанный маршрут при его рендеринге. Это полезно, когда вы хотите выполнить перенаправление внутри компонента на основе определенных условий. 
  
❗️**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
  
❗️**Опциональный:** "replace",  объект "state"
  
[Пример кода](#navigate)

####################################################################################

2. **[Redirect]** - Это компонент, который автоматически перенаправляет пользователя на другой маршрут при сопоставлении текущего URL. Redirect обычно используется внутри маршрутов для обработки ситуаций, когда пользователь не должен иметь доступ к определенной странице, или когда маршрут устарел и нужно перенаправить пользователя на новый маршрут.
  
❗️**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
  
❗️**Опциональный:** "from", "exact"
  
 [Пример кода](#redirect)

####################################################################################

3. **[useNavigate]** - Это хук, который предоставляет функцию для программной навигации. Эта функция может быть вызвана в ответ на различные действия пользователя, такие как нажатие кнопки, отправка формы или валидация данных. useNavigate дает вам более гибкий контроль над перенаправлением, поскольку позволяет вызывать функцию навигации в любом месте компонента.
  
❗️**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
  
❗️**Опциональный:** объект c "replace" или "state"
  
[Пример кода](#usenavigate)

####################################################################################

---

### 7 useParams

это хук, предоставляемый библиотекой react-router-dom, который позволяет получить доступ к параметрам из текущего URL-адреса в React-компоненте.

[Пример кода](#useparams)

[Menu](#gear-menu)

---
---
  
### [Event handlers]

1. События мыши:
- onClick: клик по элементу
- onDoubleClick: двойной клик по элементу
- onMouseDown: нажатие кнопки мыши над элементом
- onMouseMove: движение мыши над элементом
- onMouseOut: курсор мыши выходит за пределы элемента
- onMouseOver: курсор мыши наводится на элемент
- onMouseUp: отпускание кнопки мыши над элементом
  
2. События клавиатуры:
- onKeyDown: нажатие клавиши
- onKeyPress: нажатие и удержание клавиши
- onKeyUp: отпускание клавиши
  
3. События формы и элементов ввода:
- onChange: изменение значения элемента ввода *(например, `<input>`, `<textarea>` или `<select>`)*
- onSubmit: отправка формы
- onFocus: получение фокуса элементом
- onBlur: потеря фокуса элементом
  
4. События драг-н-дроп (перетаскивание):
- onDrag: перетаскивание элемента
- onDragEnd: завершение перетаскивания элемента
- onDragEnter: элемент-контейнер наведен на перетаскиваемый элемент
- onDragExit: элемент-контейнер потерял фокус перетаскиваемого элемента
- onDragLeave: перетаскиваемый элемент покидает элемент-контейнер
- onDragOver: перетаскиваемый элемент находится над элементом-контейнером
- onDragStart: начало перетаскивания элемента
- onDrop: сброс перетаскиваемого элемента в элемент-контейнер
  
5. События колесика мыши (скролла):
- onWheel: прокрутка колесика мыши над элементом
  
6. События сенсорного экрана:
- onTouchCancel: сенсорное событие отменено
- onTouchEnd: палец оторван от сенсорного экрана
- onTouchMove: движение пальцем по сенсорному экрану
- onTouchStart: касание сенсорного экрана пальцем
  
7. События пользовательского интерфейса:
- onScroll: прокрутка элемента
- onResize/resize: при изменении размеров окна браузера
  
8. События анимации:
- onAnimationStart: событие, возникающее при начале CSS-анимации элемента.
- onAnimationEnd: событие, возникающее при завершении CSS-анимации элемента.
- onAnimationIteration: событие, возникающее при завершении итерации CSS-анимации элемента (повтор анимации).

[Menu](#gear-menu)

---
---
  
# Примеры кода

---
  
### useState
 
```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Начальное значение состояния `count` равно 0

  const increment = () => {
    setCount(count + 1); // Обновление состояния `count` с перерендерингом компонента
  };

  return (
    <div>
      <p>Текущий счетчик: {count}</p>
      <button onClick={increment}>Увеличить</button>
    </div>
  );
}
```
---
  
### useEffect
  
```js
import React, { useState, useEffect } from 'react';

  useEffect(() => {
  // Запрос данных при монтировании компонента
    fetch('http://localhost:6622/api/post')
      .then((res) => res.json())
      .then((data) => {
        setPosts(data);
      })
      .catch(console.error);
    
    // Очистка ресурсов при размонтировании компонента
    return () => {
      console.log('unmount cause of user change');
    };
  }, [user]);
```
  
---
  
### useCallback
  
```js
import React, { useState, useCallback } from 'react';
import PostListItem from '../PostListItem/PostListItem';

function PostList({ posts, setPosts }) {
  const [text, setText] = useState('');

  console.log('render PostList');

  const handleRemove = useCallback((postId) => {
    fetch(`http://localhost:6622/api/post/${postId}`, {
      method: 'DELETE',
      credentials: 'include',
    })
      .then((res) => {
        if (res.ok) {
          setPosts((prevPosts) => prevPosts.filter((p) => p.id !== postId));
        }
      })
      .catch(console.error);
  }, []);
  
  return (
    <div>
      <input type="text" name="text" value={text} onChange={(e) => setText(e.target.value)} />
      {posts.map((post) => (
        <PostListItem
          key={post.id}
          title={post.title}
          userId={post.userId}
          handleRemove={handleRemove}
          postId={post.id}
        />
      ))}
    </div>
  );
}
export default PostList;
```
  
---
  
### useMemo
  
```js
import React, { useState, useMemo } from 'react';

function fibo(n) {
  if (n < 2) {
    return n;
  }
  return fibo(n - 2) + fibo(n - 1);
}

function UseMemoExample() {
  const [fiboInput, setFiboInput] = useState(5);
  const [boolean, setBoolean] = useState(false);

  const fiboResult = useMemo(() => fibo(fiboInput), [fiboInput]);

  return (
    <div>

      <p>{boolean ? 'true' : 'false'}</p>
      <button type="button" onClick={() => { setBoolean(!boolean); }}>boo</button>

      {fiboInput}
      |
      {fiboResult}
      <button type="button" onClick={() => { setFiboInput(fiboInput + 1); }}>+</button>
      <button type="button" onClick={() => { setFiboInput((prevState) => prevState - 1); }}>-</button>
    </div>
  );
}

export default UseMemoExample;

```
  
---
  
### Route
  
```js
import { BrowserRouter as Router, Routes, Route, Link } from 'react-router-dom';
import Home from './components/Home';
import About from './components/About';

const App = () => {
  return (
    <Router>
      <nav>
        <ul>
          <li>
            <Link to="/">Home</Link>
          </li>
          <li>
            <Link to="/about">About</Link>
          </li>
          <li>
            <Link to="/services">Services</Link>
          </li>
        </ul>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/services" element={<Services />} />
      </Routes>
    </Router>
  );
};

export default App;

```
  
---
  
### Outlet
  
```js
const ServicesLayout = () => {
  return (
    <div>
      <h1>Services</h1>
      <Outlet />
    </div>
  );
};
```
  
---
  
### Link
  
```js
import { Link } from 'react-router-dom';

const Navigation = () => {
  return (
    <nav>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
      <Link to="/contact">Contact</Link>
    </nav>
  );
};
```
---
  
### NavLink
  
```js
import { NavLink } from 'react-router-dom';

const Navigation = () => {
  return (
    <nav>
      <NavLink to="/" activeClassName="active" exact>
        Home
      </NavLink>
      <NavLink to="/about" activeClassName="active">
        About
      </NavLink>
      <NavLink to="/contact" activeClassName="active">
        Contact
      </NavLink>
    </nav>
  );
};
  
```
  
---
  
#### Navigate
  
```js
import { Navigate } from 'react-router-dom';

const RedirectToHome = () => {
  return <Navigate to="/" />;
};
```
---
#### Redirect
```js
import { Route, Routes, Redirect } from 'react-router-dom';
import Dashboard from './components/Dashboard';
import Login from './components/Login';
import isAuthenticated from './utils/isAuthenticated';

const AppRoutes = () => {
  return (
    <Routes>
      <Route path="/login" element={<Login />} />
      <Route path="/dashboard" element={isAuthenticated ? <Dashboard /> : <Redirect to="/login" />} />
    </Routes>
  );
};
```
  
---
  
#### useNavigate
  
```js
import { useNavigate } from 'react-router-dom';

const RedirectToHomeButton = () => {
  const navigate = useNavigate();

  const handleClick = () => {
    navigate('/');
  };
  return <button onClick={handleClick}>Go Home</button>;
};
```

---

#### useParams
  
*Создайте маршрут с динамическим параметром (например, :id) в вашем компоненте App:*
```js
import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
import MyComponent from './MyComponent';

const App = () => {
  return (
    <Router>
      <Switch>
        <Route path="/example/:id" component={MyComponent} />
      </Switch>
    </Router>
  );
};

export default App;
```
  
*В компоненте MyComponent, используйте хук useParams для доступа к значению параметра id:*

```js
import React from 'react';
import { useParams } from 'react-router-dom';

const MyComponent = () => {
  const { id } = useParams(); // Извлекаем значение параметра id из URL

  return <div>Значение параметра id: {id}</div>;
};

export default MyComponent;

```
  
*Теперь, когда пользователь переходит по URL-адресу, например, `/example/42`, компонент MyComponent будет отображать текст "Значение параметра id: 42". Значение параметра id будет доступно для использования внутри компонента через хук useParams.*

---
  
[Menu](#gear-menu)
