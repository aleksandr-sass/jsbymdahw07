# Домашняя работа к седьмому занятию
## Задачи:
I. Добавить крестик на ```<div class="modal__body">```.
II. При помощи механизма делегирования реализовать возможность закрытия модального окна с корзиной выбранных товаров (```<div class="modal">```).
III. Устранить "баг", который проявлялся в том, что (ранее) модальное окно (см. пункт №2 этого задания) закрывалось также и при нажатии на ```<div class="modal__body">``` (чего категорически не должно было бы быть!!!).
IV. Реализовать поиск товаров из каталога: написать необходимый js-код, который обеспечит поиск товаров по их названию, хранящемуся в массиве cards. Результаты поиска следует отобразить в ```<div class="shop__content">```. Примеры запросов и результатов поиска:
* "100" => отобразить все пакеты кофе по 100 грамм;
* "ETHIOPIA" => отобразить все пакеты кофе с типом "ETHIOPIA";
* "COFFEE" => отобразить все 12 пакетов кофе из массива сards
* "белиберда" или "" => либо оставить ```<div class="shop__content">``` без изменений, либо убрать из ```<div class="shop__content">``` все пакеты кофе (то есть, очистить его).

## Решение:
### I. Добавить крестик:
a. путь к картинке с крестиком: img/delete.png
b. HTML:
```
<div class="modal__body">
	<div class="close"></div>
</div>
```
c. CSS:
```
.modal__body {
    width: 60%;
    height: 60%;
    background-color: bisque;
    position: relative;
}
.close {
    background-image: url(img/delete.png);
    background-size: cover;
    width: 64px;
    height: 64px;
    position: absolute;
    top: -32px;
    right: -32px;
    border-radius: 50%;
    cursor: pointer;
}
```
### II. Закрытие модального окна:
a. JS:
```
const modal = document.querySelector('.modal');
const closeDiv = document.querySelector('.close');

modal.addEventListener('click', (e)=> {
    e.preventDefault();
    if ((e.target == modal)||(e.target == closeDiv)) {
        modal.style.display = 'none';
    }    
});
```
b. **Все готово:** теперь модальное окно закрывается при клике непосредственно на ```<div class="modal">``` ```(if (e.target == modal)``` либо при клике непосредственно на "крестик" ```(if (e.target == closeDiv)```.
### III. Устранить "баг":
a. **Все готово:** теперь модальное окно НЕ закрывается при клике непосредственно на <div class="modal__body"> (что наблюдалось ранее).
### IV. Реализация функции поиска:
a. HTML (уже было написано при работе в классе):
```
<li>
	<form action="">
		<input class="form__input" name="form-input" type="text" autocomplete="on">
		<input class="form__btn" type="button" value="НАЙТИ">
	</form>
</li>
```
b. JS (реализуем требуемую функциональность - поиск товара по подстроке):
```
const formInput = document.querySelector('.form__input');
const formBtn = document.querySelector('.form__btn');

formBtn.addEventListener('click', substringSearch);

function substringSearch() {
    const STR = formInput.value.toUpperCase();
    const validCards = cards
        .filter((el) => el
            .name
            .toUpperCase()
            .includes(STR));
    if ((validCards.length == 0) || (STR == '')) {
        alert(`Ничего не найдено. Побробуйте найти кофе из Кении -> введите "Kenya"`);
    } else {
        paintCards(validCards);
    }    
}
```
c. **Все готово:** реализован поиск товара по подстроке.

