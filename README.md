# [Cheatsheet CSR]
- **Set up** [Перейти](#react-hooks)
- **React Hooks** [Перейти](#react-hooks)
1 useState
2 useEffect
3 useContext
4 useReducer
5 useCallback
6 useMemo

- **React Router** [Перейти](#react-router)
1 BrowserRouter
2 Routes
3 Route
4 Outlet
5 Link / NavLink
6 Navigate / useNavigate / Redirect
7 useParams

- **Event handlers** [Перейти](#event-handlers)


- **Redux/ReduxKit** [Перейти](#redux/reduxKit)
---
---
## 🆙 Set up
- `npx create-react-app client` | [Create React App](https://create-react-app.dev/)
- `npx create-react-app client --template typescript` | [on TypeScript](https://create-react-app.dev/)
- `npm i react-router-dom` | [React Router](https://reactrouter.com/en/main)
- `npm i redux react-redux @redux-devtools/extension @reduxjs/toolkit` | [redux](https://redux.js.org/) | [devtools](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd) | [toolkit](https://redux-toolkit.js.org/)

## 🧑‍🎨 OPTION 
- `npm install @mui/material @emotion/react @emotion/styled` | [MUI](https://mui.com/)
- `npm install react-bootstrap bootstrap` | [react-bootstrap](https://react-bootstrap.github.io/)
---
---
# React Hooks

### [useState]
*useState — это хук (hook) в React, который позволяет добавлять локальное состояние в функциональные компоненты. useState принимает начальное значение состояния и возвращает массив из двух элементов: текущее состояние и функцию для обновления этого состояния.*

-  `initialState = []` | начальное состояние
-  `const [state, setState] = useState(initialState);` | state — текущее значение состояния
-  `setState((prev) => [...prev, 'hello']);` | setState — функция для обновления состояния. При вызове этой функции с новым значением состояние будет обновлено, а компонент перерендерится.

пример:
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
### [useEffect]

*useEffect — это хук (hook) в React, который позволяет выполнять побочные эффекты, такие как запросы к серверу, подписки на события или обновление DOM в функциональных компонентах. useEffect принимает функцию, которая выполняет побочные эффекты, и массив зависимостей, указывающий, при каких изменениях эффект должен повторно выполняться*
```js
useEffect(() => {  // Выполнение побочного эффекта
  
  return () => {     // Очистка побочного эффекта (необязательно)
  };
 
}, [dependencies]);  // Массив зависимостей (необязательно)
```
- Первый аргумент - функция, в которой выполняется побочный эффект. 
Она будет вызываться после каждого рендеринга компонента.
- Второй аргумент - необязательный массив зависимостей. useEffect будет вызываться только при изменении значений в массиве зависимостей. Если массив пуст, useEffect вызывается только при монтировании и размонтировании компонента.
- Если первый аргумент возвращает функцию, она будет использоваться для очистки побочного эффекта. Эта функция вызывается при размонтировании компонента или перед выполнением следующего эффекта.

пример:
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
### [ReactRouterDom]

**React-Router** - это библиотека маршрутизации, обеспечивает переход между различными компонентами React, когда пользователь взаимодействует с интерфейсом. react-router поддерживает маршрутизацию как на стороне клиента (client-side), так и на стороне сервера (server-side).

**React-Router** предоставляет ряд компонентов и хуков, которые могут быть использованы для создания маршрутизации.
Некоторые из основных компонентов react-router включают:

1. **BrowserRouter**: Компонент-обёртка, который использует HTML5 History API для синхронизации UI с URL-адресом в браузере. Он обеспечивает базовую навигацию и должен быть помещен в корень вашего приложения, окружая все маршрутизируемые компоненты.

2. **Routes**: используется для определения коллекции маршрутов в вашем приложении. Он предоставляет функциональность для выбора и отображения правильного маршрута на основе текущего URL.
**❗️обязательный параметр**
*children*: Обязательное свойство, определяющее дочерние маршруты, которые будут вложены в Routes. Обычно здесь размещаются компоненты *Route* для определения различных маршрутов
**❗️Опциональный**
*location*: Опциональное свойство, позволяющее передать собственный объект *location* для определения текущего маршрута. Это может быть полезно в редких случаях, когда вам нужно вручную контролировать местоположение вместо использования автоматического определения маршрута библиотекой react-router-dom.
[Пример кода](#route)
3. **Route**: пределяет сопоставление между URL-адресом и компонентом, который должен быть отображен при совпадении этого URL. 
**❗️обязательный параметр**
*element* - Обязательное свойство, определяющее компонент, который будет отображаться при совпадении маршрута
**❗️Опциональный**
*path* - Опциональное свойство, определяющее путь URL, который будет сопоставлен с этим маршрутом. Путь может содержать параметры (например, :id). Если path не указан, маршрут будет считаться "пойманным всем" и будет рендериться, когда другие маршруты не совпадают.
*children* - свойство, используемое для определения дочерних маршрутов внутри родительского маршрута. Это полезно, когда вы хотите создать вложенную иерархию маршрутов.
*caseSensitive* - булево свойство, определяющее, будет ли маршрут учитывать регистр при сопоставлении путей. По умолчанию равно false, что означает, что маршрут будет сопоставляться без учета регистра.
*index* -  булево свойство, определяющее, будет ли данный маршрут считаться индексным маршрутом для своего родителя. Если true, маршрут будет отображаться, когда родительский маршрут точно совпадает с текущим маршрутом. По умолчанию равно false.
*strict* -  булево свойство, определяющее, будет ли маршрут точно сопоставляться с путем с учетом слеша / на конце. Если true, маршрут будет считаться совпадающим только в том случае, если слеш на конце пути будет соответствовать текущему маршруту. По умолчанию равно false.
[Пример кода](#route)
4. **Outlet**: используется для отображения дочерних маршрутов внутри родительского маршрута.
❗️Не имеет свойств.
5. **Link | NavLink** / ссылки
a. **Link** - Это базовый компонент для создания навигационных ссылок. Вместо использования тега <a>, используйте компонент Link с атрибутом to, указывающим на путь, куда должна вести ссылка.
**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
**Опциональный:** "replace" или объект "state"
[Пример кода](#link)
b. **NavLink** - похож на Link, но с дополнительной возможностью стилизации активных ссылок, автоматически применяет активный стиль или класс к ссылке, когда текущий маршрут соответствует маршруту, указанному в атрибуте to.
Это полезно для визуального отображения активных ссылок в вашем приложении.
**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
**Опциональный:** "replace", "activeClassName", "activeStyle", "exact",  или объект "state"
[Пример кода](#navlink)
6. **Navigate | Redirect | useNavigate** / перенаправление
a. **Navigate** - Это компонент, который автоматически перенаправляет пользователя на указанный маршрут при его рендеринге. Это полезно, когда вы хотите выполнить перенаправление внутри компонента на основе определенных условий. 
**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
**Опциональный:** "replace",  объект "state"
[Пример кода](#navigate)
b. **Redirect** - Это компонент, который автоматически перенаправляет пользователя на другой маршрут при сопоставлении текущего URL. Redirect обычно используется внутри маршрутов для обработки ситуаций, когда пользователь не должен иметь доступ к определенной странице, или когда маршрут устарел и нужно перенаправить пользователя на новый маршрут.
**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
**Опциональный:** "from", "exact"
 [Пример кода](#redirect)
c. **useNavigate** - Это хук, который предоставляет функцию для программной навигации. Эта функция может быть вызвана в ответ на различные действия пользователя, такие как нажатие кнопки, отправка формы или валидация данных. useNavigate дает вам более гибкий контроль над перенаправлением, поскольку позволяет вызывать функцию навигации в любом месте компонента.
**обязательный параметр:** "to" или объект с данными "pathname, search и hash"
**Опциональный:** объект c "replace" или "state"
[Пример кода](#usenavigate)
7. **useParams** - это хук, предоставляемый библиотекой react-router-dom, который позволяет получить доступ к параметрам из текущего URL-адреса в React-компоненте.


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
- onChange: изменение значения элемента ввода (например, <input>, <textarea> или <select>)
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


# Примеры кода

### BrowserRouter
```js
```
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
#### Navigate
```js
import { Navigate } from 'react-router-dom';

const RedirectToHome = () => {
  return <Navigate to="/" />;
};
```
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
