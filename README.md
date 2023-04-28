# Vue Art Gallery

## Первый запуск
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```


### Функционал 


1. Строка поиска
   При вводе текста в строке поиска происходит поиск по названиям позиций. Лишние карточки исчезают/скрываются.

2. Кнопка "купить"
   При нажатии на кнопку "купить":

она меняет состояние на 2 секунды, на "обрабатывается"
после "обрабатывается" переходит в состояние "в корзине"
Отображение состояний визуально оформлено, например, "preloader icon", "purchase icon", "checked icon" и т. д. Дизайн/стиль продуман самостоятельно.

3. Сохранение состояния позиций
   После перезагрузки страницы состояния позиций (в корзине или нет) сохраняются.

4. Подробное описание позиции
   При клике на название/изображение товара открывается модальное окно с карточкой товара. В карточке есть:

краткое описание позиции
цена
слайдер, содержащий 2-4 изображения
Дизайн модального окна продуман самостоятельно.

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
