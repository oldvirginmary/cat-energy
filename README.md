# Cat energy

## Требования и технологии
Строительство ведётся с использованием следующих технологий:
1. HTML
1. CSS (SCSS)
1. JavaScript

## Описание
![Превью](https://i.ibb.co/D7Xy95W/Annotation-2020-06-07-194251.png)  
[**Полистать его**](https://oldvirginmary.github.io/cat-energy/build/index.html)

### Сайт
Собирается вместе с графикой, стилями и прочим имуществом с помощью Gulp-скрипта в директорию **/build**.  
Вёрстка идёт с использованием **мобильные вперёд** парадигмы.

### Страницы
Страницы собираются из блоков, общих скриптов, общих стилей. Но HTML-разметка пока пишется вручную для каждой страницы.  
Именования классов по международному **БЭМ** (блок__элемент--модификатор). 

* `<head>` здесь подключаются стили, шрифты
* `<body>` здесь (в конце) подключаются скрипты

### Блоки
Каждый блок содержит в себе контент, относящийся только к нему самому:
1. Стили
1. Скрипты
1. Изображения

Стили блока, способного наследоваться, не будут содержать внешние отступы.  
Отступы для такого блока следует задавать в отдельном стилевом файле, именуемом **flow**.

### Стили
Бывают 4-х видов:
1. Неизменяемые (напр. **normalize.css**)
1. Общие
1. Блочные
1. Страничные

#### Неизменяемые
В отличие от других, подключаются напрямую в HTML-документ.  
Часто служат для упрощения разработки.

#### Общие
* **variables** – глобальные переменные
* **main** – общие для всего сайта стили, общие элементы (напр. шрифты, кнопки)
* **flow** – стили потока контента (напр. заголовки разделов, внешние отступы блоков)

#### Блочные
Каждый стилевой файл начинается с названия блока.  
Он может содержать в себе другие, более мелкие блоки.  
Сначала стилизуется общий блок, а затем, его мелкие части.  
Стилизация должна происходить по порядку: снаружи внутрь DOM-дерева, а затем вниз по строкам.

#### Страничные
Стили каждой страницы собираются из небольших кусочков в дедуктивном порядке (от общего к частному):
1. Общие стили: сначала подключаются **variables**, **main**, **flow**
1. Стили блоков, которые используются на странице
1. Уникальные стили, переопределяющие предыдущие

### Скрипты
1. **Общие** – могут влиять на всю страницу
1. **Блочные** – подключаются вместе с блоком и отвечают только за взаимодействие внутри него

Следует по необходимости использовать такие общие скрипты:
* **no** регулирует использование скриптов на странице, если они отключены, пользователь сможет видеть основной контент страницы, а также использовать навигацию (class="no-js" для `<body>`)
* **lazyload** позволяет распределять загрузку контента, с его помощью можно загружать большие файлы в последнюю очередь
* **svg4everybody** сделает доступным отображение SVG-изображений в старых браузерах

### Графика
Экспортируется и хранится в оригинальном качестве до попадания в **/build**.
* **svg** собирается в спрайт и вставляется на странице там, где это возможно с семантической и практической точки зрения
* **png** и **jpg** сжимаются

### Билд
Собирается с помощью **Gulp**.  
Задачи разбиваются по группам:
* **общие**
* **для строительства (префикс dev-)** 
* **для производства (префикс prod-)**

Примечание: билд в этом репозитории **для строительства**, чтобы вам было удобно.
