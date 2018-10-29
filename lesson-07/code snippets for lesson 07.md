
Урок 7. create-react-app и подробнее про state
=====================================================================

Всем привет. Мы продолжаем изучать React.

В этом курсе хочется охватить РАЗНЫЕ инструменты и среды для написания React-приложений. Так что после подхода в лоб с подключением в html скриптов реакта и бэйбела и подхода с написанием кода в среде CodePen, мы воспользуемся заготовкой под названием create-react-app.

Вот его репозиторий. В сущности, это все необходимое для того, чтобы сходу начать писать свое React-приложение.

И это инструмент именно для создания шаблона приложения, не сам шаблон. Поэтому, устанавливаем его через npm в систему, причем глобально. Для Windows-пользователей рекомендую поставить Git Bash (https://gitforwindows.org/) - тогда консоль станет намного более дружественной. ну и чтобы работала команда npm, надо поставить nodejs - она идет в комплекте.

Теперь, после того, как create-react-app стал доступен, перехожу на рабочий стол и выполняю там create-react-app react-lesson-07
Я получаю не только файлы шаблона, но и все npm-модули, перечисленные в списке зависимостей в package.json. Словом, теперь все готово для работы.

Перехожу в папку с проектом (cd react-lesson-07) и выполняю yarn start. Yarn это альтернатива npm, но можно и выполнить npm run start - получится то же самое.

start, на самом деле, это ссылка на последовательность действий, запускающих наш шаблон в dev-режиме, то есть в режиме для разработки. Все доступные задачи перечислены в файле package.json.

build это сборка на продакшен, то есть на уже готовый работающий сайт. Между dev'ом и prod'ом есть ряд важных различий, но сейчас мы на них подробно останавливаться не будем.

Давайте выполним команду eject. Подтверждаем, что хотим действие произвести.
Сейчас мы настройки сборки перенесли из папки node_modules/react-scripts в корень нашего проекта. откуда можем их изменить так как нам нужно, либо просто как минимум посмотреть как внутри все устроено. А это нам, безусловно интересно.

Итак, npm run start или yarn start и запустился локальный сервер с минимальным приложением. Отлично.
Посмотрим на его исходники - папка src.

index.js - точка входа в наше приложение - тут видим знакомую нам функцию ReactDOM.render. Она рисует компонент App на ноде с айдишником root. App же импортируется из той же папки, где находится index.js. В начале пишется точка (это текущая директория файла) именно для того, чтобы указать, где именно искать файл App.js. расширение .js можно обычно опускать.

В index.css находятся глобальные стилевые правила, хотя от них мы сейчас избавимся, удалив файл и импорт. Также удалим сервис-воркер для кэширования ресурсов. Он нам не нужен в наших уроках.

Вот этот импорт с React'ом должен быть почти в каждом файле, чтобы все работало.
Ну и импорт ReactDOM нужен для вызова функции render именно в этом файле.

Файл с тестами для App также удалим.

Теперь сам App. Удалим импорт логотипа и содержимое return. Вставим туда то, что было у нас в App в прошлом уроке. Не забудем прицепить стейт и метод newRandomAge.

Имеющиеся стили также очистим и добавим парочку своих.

```
* {
    box-sizing: border-box;
}

body {
    display: table;
    margin: 50px auto 0;
}
```

Для Profile же мы создадим отдельный одноименный файл и поместим туда его в виде презентационного компонента.

Теперь важно написать еще и экспорт, чтобы сказать, что из этого файла, как бы отдается наружу, при попытке его импорта. Это будет наш Profile. Далее в App мы его импортируем вот так.

Если мы сделаем экспорт без ключевого слова default, то нужно будет экспортировать и импортировать используя фигурные скобки. Так делают, если экспортируется не что-то одно, а несколько элементов.

То что было в CodePen, теперь у нас находится локально. При изменении всех файлов происходит автоматическая перезагрузка приложения - это касается как JS, так и CSS-файлов. И девтулзы работают как надо. То что нужно! Мы можем продолжать изучать Реакт в более удобных условиях.



Итак, вы уже, думаю, поняли что разбиение на файлы-компоненты значительно упрощает жизнь - работать с длинным полотном кода удовольствие из малоприятных. Хотя CodePen вещь очень крутая - Можно тренироваться в пару кликов из любого места, не ставя никакого софта на компьютер.

HTML-файл для нашего проекта лежит в папке public. Там также есть фавиконка и файл манифеста, где находится различная дополнительная информация.

А давайте теперь попробуем собрать проект на продакшн. При этом, я верну импорт логотипа в App - хочу кое-что показать.

Запускаем сборку на прод - yarn build. Появилась папка build. Вот именно ее-то мы и будем как готовый продукт выкладывать на всеобщее обозрение.

index.html тут минифицирован. Я его разверну для вас в нормальный вид.

Вот тут наши полностью собранные и минифицированне стили, а тут - скрипты. К ним прилагаются map-файлы, которые инструмента разработчика Хрома умеют подхватытвать и показывают благодаря этому исходные местоположения строк стилизации и кода. Иначе это называется сорс-мэпы.

Вот точка входа нашего приложения - вспоминаем содержимое index.js из папки src.

В папке static все наши файлы, в том числе и картинки. Имна у них уже не те что были в оригинале, но тут все уже перелинковано и работает как надо. Так что остается лишь пользоваться.



=== State

Что ж, с инструментом для нормальной работы локально, мы подразобрались. Теперь давайте подробнее поговорим про стейт, о котором уже не только шла речь, но который мы уже использовали для целей хранения новосгенерированного возраста.

Рассмотрим вполне хороший пример из документации React. Буду писать прямо в index.js. Первый вариант такой:

```
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

Здесь есть презентационый компонент Clock, который из пропсов берет объект даты и преобразует его в удобочитаемую строку с помощью метода toLocaleString().

Обновление же происходит каждую секунду за счет вызова метода ReactDOM.render ежесекундно с помощью нативного джаваскриптового setInterval. Дата передается в пропс date компонента. Однако это совсем не React-подход.

React подход заключался бы в том, чтобы всю логику изолировать в компоненте Clock и пусть он уже сам себя перерисовывает. Вот этот код:

```
class Clock extends React.Component {
  constructor(props) {
    console.log(1)

    super(props)
    this.state = { date: new Date() }
  }

  componentDidMount() {
    console.log(3)

    this.timerID = setInterval(
      () => this.tick(),
      1000
    )
  }

  componentWillUnmount() {
    console.log(4)

    clearInterval(this.timerID)
  }

  tick() {
    this.setState({
      date: new Date()
    })
  }

  render() {
    console.log(2)

    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    )
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
)
```

Тут ReactDOM.render просто рисует сам компонент, ничего ему через пропсы не передавая.

А уже внутри происходит магия, о которой мы говорили в прошлом уроке, разбирая методы жизненного цикла компонента.

В конструкторе Clock мы инициализируем стейт текущим объектом даты.

мы идем в порядке следования вызова методов. По очереди далее идет первый рендер. Стейт уже имеет значение даты и потому date.toLocaleTimeString возвращает корректную строку, которая и рисуется. Далее в componentDidMount задается интервал в одну секунду, и каждую эту одну секунду мы модифицируем стейт, записывая туда новый объект даты. А запись в стейт триггерует перерендер, что мы с вами сейчас и наблюдаем к своему великому удовольствию)

==

Есть несколько вещей про которые стоит помнить при работе со стейтом.

==
Первая - в него не стоит писать напрямую, потому что это не запустит очередной перерендер.
Надо использовать метод setState, в который передается объект с полями, которые надо обновить. вот как мы делали с датой.

А где можно писать в стейт напрямую, так это в конструкторе, при инициализации - опять же в примере выше ровно это и делалось.

==
Вторая вещь - это то, что запись в стейт может происходить не тогда, когда вы этого ожидаете, то есть асинхронно. Все из-за оптимизаций реакта, когда он может за раз сделать пакетом несколько setState'ов.

Если вам надо сделать что-то вроде такого:
```
this.setState({
  counter: this.state.counter + this.props.increment,
})
```

То есть если сложить текущий стейт и текущий пропс, то это может сработать совсем не так как может предполагаться.

Для этого используется другая запись, когда вместо объекта в setState передается функция-колбэк, которая принимает в качестве аргументов предыдущий стейт (обратите внимание на слово "предыдущий" - это важно) и текущие пропсы:

```
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}))
```

Так вы гарантированно работаете с предсказуемым стейтом.

Третье это то, что Реакт мерджит (от английского merge - сливать в единое, соединять) то что вы передали в setState с тем что есть в реальном стейте. Таким образом, если стейт был таким:

```
state = {
  messages: [{
    id: 1, text: 'Hi'
  }],
  calls: []
}
```

и вы сделали так:

```
this.setState((prevState) => ({
  calls: prevState.calls.push({
    id: 4, number: '+7 999 888 55 66'
  })
}))
```

То в результате получится так сказать умная сумма:

```
state = {
  messages: [{
    id: 1, text: 'Hi'
  }],
  calls: [{
    id: 4, number: '+7 999 888 55 66'
  }]
}
```

Как видно, переданный для сетСтейта объект не перезаписал весь стейт, а только обновил значения одноименных ключей. И это очень и очень удобно.



=== Однонаправленный поток

Ну и последний важный для этого ролика момент.

В Реакте поток данных идет сверху вниз, то есть от родительских компонентов к дочерним. Данные эти передаются через пропсы, с которыми вы уже знакомы. Однако, и дочерним компонентам тоже нужно передавать данные родительским в более-менее сложном приложении. Как же это делать?

Ответ - через те же пропсы, как ни странно. В чем именно подвох - будет рассказано в следующих уроках.

Пока же обращу ваше внимание, если вы еще не осознали, что компонент Реакта является изолированной единицей в плане данных внутри него и можно создавать сколько угодно экземпляров того же счетчика, что вы видели выше и они будут работать не мешая друг другу. Но независимым полностью компонент, как правило, не бывает, так как чаще всего зависит от пропсов, которые в него прокидываются сверху.