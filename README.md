# Regular Expressions Documentation

### Содержание
+ [Создание регулярного выражения](#creating_ru)
+ [Спецсимволы](#symbols_ru)
+ [Квантификаторы](#quanti_ru)
+ [Альтернация](#alter_ru)
+ [Опережающие и ретроспективные проверки](#checks_ru)
+ [Диапазоны символов](#sets_ru)
+ [Якоря: начало и конце строки. Граница слова: /b](#anchor_ru)
+ [Флаги](#flags_ru)


<!-- Создание регулярного выражения - НАЧАЛО  -->

## <a name="creating_ru"></a> Создание регулярного выражения

Регулярное выражение может быть создано с помощью двух способов:

1) С помощью конструктора `new RegExp` - `new RegExp("шаблон", "флаги")`
2) С помошью литеральных конструкций (слешей `/`) - `/шаблон/флаги`

<!-- Создание регулярного выражения - КОНЕЦ  -->


<!-- Спецсимволы - НАЧАЛО  -->
## <a name="symbols_ru"></a> Спецсимволы

Спецсимволы - это символ, который обозначает набор определенных символов и соответствие набору этих символов. Проще говоря, символ, который внутри себя содержит группу других сиволов. Спецсимвол всегда начинаеться с обратного слеша `\спецсимвол`. Также существуют обратные спецсимволы, обозначаются как обычный спецсимволы только в верхнем регистре.

Примеры спецсимволов:
1) `\d` - означает набор символов от `0 до 9`
2) `\s` - означает семейство пробельных символов. Включает в себя символы: 
    + пробела
    + табуляции `\t`
    + перевода строки `\n`
    + другие символы `\v`, `\f`, `\r`
3) `\w` - означает буквы латинского алфавита `[a-zA-Z]`, цифра `[0-9]` и подчеркивание `_`
4) `.` - точка как символьный класс пишется без слеша, означает любой символ, кроме новой строки. Для того, чтобы найти точку как символ используется экранирование `\.`

Примеры обратных спецсимволов:
1) `\D` - означает набор всех символов, кроме как `0 до 9`
2) `\S` - означает набор всех символов, кроме семейства пробельных символов
3) `\W` - означает набор всех символов, кроме букв латинского алфавита `[a-zA-Z]`, цифер `[0-9]` и подчеркивания `_`. Русские буквы входят в этот символьный класс.


<!-- Спецсимволы - КОНЕЦ  -->



<!-- Квантификаторы - НАЧАЛО  -->
## <a name="quanti_ru"></a> Квантификаторы

Квантификатор указывает на количество повторений любого символа после которого он стоит. Самым простым квантификатором является число в фигурных скобках `{n}`.
Например, нужно найти 5 цифер - без квантификатора это делалось бы вот так `\d\d\d\d\d`, с квантификатором это выглядит вот так `\d{5}`. В данном случае ищется конкретное кол-во символов.

С помощью квантификаторов можно указывать диапазоны:
1) `{3, 5}` - данный квантификатор указывает на диапазон от трёх до пяти символов
2) `{1,}` - если не указывать верхний диапазон, тогда поиск будет происходить от одного символа и до бесконечности

Для самых популярных квантификаторов существуют сокращения:
1) `+` - тоже самое, что и диапазон `{1,}`. Пример, `\d{1,}` тоже самое, что и `\d+`
2) `?` - тоже самое, что и диапазон `{0,1}`. Пример, `\d{0, 1}` тоже самое, что и `\d?`. Практически, делает символ необязательным.
3) `*` - тоже самое, что и диапазон `{0,}`. Пример, `\d{0,}` тоже самое, что и `\d*`


Жадные и ленивые квантификаторы.
По умолчанию, регулярное выражение является жадным, то есть ищёт максимально возможное кол-во символов, которое удовлетворяет шаблон. Ленивый же квантификатор обозначается с помощью `?` после квантификатора и ищёт совпадение с шаблоном после каждого повторения квантификатора.

<!-- Квантификаторы - КОНЕЦ  -->


<!-- Альтернация - НАЧАЛО  -->
## <a name="alter_ru"></a> Альтернация
Альтернация - термин, которые под собой подразумевает логический оператор "ИЛИ". Обозначается с помощью прямого слеша `|`. `/первое_условие|второе_условие/`. Для применени альтернации к части шаблона нужно использовать скобки `(условия)`.
<!-- Альтернация - КОНЕЦ  -->


<!-- Опережающие и ретроспективные проверки - НАЧАЛО  -->
## <a name="checks_ru"></a> Опережающие и ретроспективные проверки
Опережающие и ретроспективные проверки нужны для того, чтобы найти соответствия шаблону, но только те ПЕРЕД которыми или ПОСЛЕ которых идет другой шаблон. Такие проверки всегда идут в скобках `()`.

Опережающая проверка нужна для того, чтобы проверить то, что идёт **ПОСЛЕ** шаблона.
Ретроспективная проверка нужна для того, чтобы проверить то, что идёт **ПЕРЕД** шаблоном.

Примеры:
1) Синтаксис **позитивной опережающей** проверки: `X(?=Y)`. Он означает: найди `X` при условии, что за ним следует `Y`.
2) Синтаксис **негативной опережающей** проверки: `X(?!Y)`. Он означает: найди `X` при условии, что за ним **НЕ** следует `Y`.
3) Синтаксис **позитивной ретроспективной** проверки: `(?<=Y)X`. Он означает: найди `X` при условии, что перед ним есть `Y`.
4) Синтаксис **негативной ретроспективной** проверки: `(?<!Y)X`. Он означает: найди `X` при условии, что перед ним **НЕТ** `Y`.

В данных примерах условие проверки не будет включено в результат, который будет найден. Для того, чтобы проверка была включена в результат нужно условие проверки обернуть скобками `X(?=(Y))`.


<!-- Опережающие и ретроспективные проверки - КОНЕЦ  -->

<!-- Диапазоны символов - НАЧАЛО  -->
## <a name="sets_ru"></a> Диапазоны символов
Диапазоны символов обозначаются квадратными скобками `[символы]` и внутри них идёт перечисление символов по которым происходит поиск.
К примеру, нужной найти число 20, 21, 22 и 23. Можно все сделать с помощью альтернации `2(0|1|2|3)`, но выглядит громоздко и не читаемо, особенно если кол-во символов будет большое, в данном случае можно использовать диапазон `2[0-3]`, означает он тоже самое, но выглядит короче и читабельнее.

Также диапазоны можно делать **исключающими**. Они обозначаются символом каретки `^` и соответствуют любому символу за исключением заданных в диапазоне. Пример: `2[^4-9]` - означает, что после двойки может идти любой символ, кроме как диапазон от 4 до 9.

Также в квадратных скобках такие символы, как `.`, `+`, `()`, `-`, `^` не нуждаются в экранировании, в квадратных скобках они теряют силу символьных классов.


<!-- Диапазоны символов - КОНЕЦ  -->

<!-- Якоря: начало и конце строки. Граница слова: /b - НАЧАЛО  -->
## <a name="anchor_ru"></a> Якоря: начало и конце строки. Граница слова: /b

Якорями начала и конца строки называют такие символы:
+ Начало строки `^`
+ Конец строки `$`

Также можно использовать якоря вместе `^шаблон$` для того, чтобы узнать совпадает ли строка с шаблоном полностью.

Граница слова `\b` – проверка, как `^` и `$`. Данный символ проверяет, что позиция в строке является границей слова.

<!-- Якоря: начало и конце строки. Граница слова: /b - КОНЕЦ  -->

<!-- Флаги - НАЧАЛО  -->
## <a name="flags_ru"></a> Флаги

Флаг - это символ, которые пишется после регулярного выражения `/шаблон/флаги` (либо же вторым аргументом, если регулярное выражение создается через конструктор `new RegExp("шаблон", "флаги")`) и влияет на поиск.

В JS есть всего шесть флагов:
1) `g` - данный флаг означает, что шаблон будет искать все совпадения в строке, без данного флага шаблон ищёт только первое совпадение.
2) `i` - данный флаг означает, что поиск по строке не зависит от регистра, то есть разницы между строчной и заглавной буквы не будет.
3) `m` - флаг многострочного режима, позволяет искать указанный шаблон в строках, где есть перевод строки.
4) `s` - флаг, который нужен для того, чтобы универсальный символ точки `.` мог включать в себя символ перевода строки `/n`.
5) `u` - флаг включает поддержку юникода и корректно обрабатывает суррогатные пары, которые используются в смайликах, к примеру.
6) `y` - флаг для поиска по заданной позиции. [(Смотреть документацию по флагу `y`)][yFlag-repo]
<!-- Флаги - КОНЕЦ  -->



[yFlag-repo]: https://learn.javascript.ru/regexp-sticky
