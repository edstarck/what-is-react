### Этапы создания своего фреймворка на подобии реакт:

```
1. Сделали простоую верстку на html
2. Переделали ее на динамическую -> сделали рендер через javascript
3. Поскольку сделали все одним потоком, делаем декомпозицию кода на компоненты,
   проще всего сделать функции которые будут возвращать элементы

   function App() {
        const app = document.createElement('div')
        app.className = 'app'
        app.append(Header())

        return app
    }
    const domRoot = document.getElementById('root')
    domRoot.append(App())
```

```
-- иденпатентная функция  -> функция которая ни имеет ни каких побочных эффектов
   при одних и тех же вызовах с одними и теми же аргументами будет получен один и тот же результат

   function Logo() {
        const logo = document.createElement('img')
        logo.classList.add('logo') // коллекция классов
        logo.src = 'logo.png'

        return logo
    }

    *** функция с сайд эффектом

    function Clock() {
        const clock = document.createElement('div')
        clock.className = 'clock'
        clock.innerText = state.time.toLocaleTimeString()

        return clock
    }

    потому что идет обращение к state.time.toLocaleTimeString() переделаем на чистую функцию
    function Clock(time) {
        ...
        clock.innerText = time.toLocaleTimeString()
        return clock
    }

    Clock(state.time)

    перепишем на

    app.append(Clock({time: state.time}))
    // Tell, Don`t ask -> передаем те данные которые нужны коду

    передаем не один аргумент, а структуру в случаи увеличении числа аргументов.

4. отделили все данные от представления и вынесли их в отдельную структуру... state

```
