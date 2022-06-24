## Продвинутый Python. Часть 1: анализ данных.  
<details>
  <summary>Numpy и Pandas</summary>
  <details>
    <summary>Задание - импорт данных</summary>
    
Возьмите данные по вызовам пожарных служб в Москве за 2015-2019 годы. Получите из них фрейм данных (таблицу значений). По этому фрейму вычислите среднее значение вызовов пожарных машин в месяц в одном округе Москвы, округлив до целых.  
    
  </details>
  
[Решение:](6_python_advaced/1_analysis/task1.ipynb)
1. Из csv файла загружаем необходимые столбцы.
2. Проверяем названия округов и оставляем только 1е слово в нижнем регистре.
3. Для исправлений опечаток названий округов составляем словарь, где ключ-опечатка, а значения-правильные названия.
4. Исправляем оставшиеся опечатки, путем поиска опечаток в ключах словаря и замены их на значения.
5. Т.к. у нас одна запись за один месяц(не нужно отдельно считать количество месяцов), вычисляем среднее стандартной агрегатной функцией mean() по сгруппированным по округам данным. Получаем среднее количество вызовов в месяц(за все время ведения статистики) для каждого округа.
6. Среднее количество вызовов в месяц для одного(случайного) округа получаем путем усреднения из предыдущего пункта. 
  
</details>
 
  
 
<details>
  <summary>Индексы и объединение фреймов</summary>
  <details>
    <summary>Задание - данные из нескольких источников</summary>
    
Получите данные по безработице в Москве. Объедините эти данные индексами (Месяц/Год) с данными из предыдущего задания (вызовы пожарных) для Центральный административный округ. Найдите значение поля UnemployedMen в том месяце, когда было меньше всего вызовов в Центральном административном округе.
    
  </details>
  
[Решение:](6_python_advaced/1_analysis/task2.ipynb)
1. Из csv файлов загружаем необходимые столбцы.
2. Переиндексируем датафреймы и мержим их по индексам.
3. Оставляем данные только по ЦАО.
4. Прреиндексируем данные по количеству выховов и сортируем по ним.
5. Находим значение UnemployedMen для минимального индекса. 
  
</details>
 
<details>
  <summary>Фильтрация и изменение данных</summary>
  <details>
    <summary>Задание - выделение данных</summary>
    
Получите данные по безработице в Москве. Найдите, с какого года процент людей с ограниченными возможностями (UnemployedDisabled) среди всех безработных (UnemployedTotal) стал меньше 2%.
    
  </details>
  
[Решение:](6_python_advaced/1_analysis/task3.ipynb)
1. Из csv файла загружаем необходимые столбцы.
2. В датафрейм Years отбираем те записи, в которых доля безработных людей с ограниченными возможностями < 2%.
3. Находим минимальное значения года в датафрейме Years. 
  
</details>
 
<details>
  <summary>Линейная регрессия</summary>
  <details>
    <summary>Задание - предсказание на 2020 год</summary>
    
Возьмите данные по безработице в городе Москва. Сгруппируйте данные по годам, и, если в году меньше 6 значений, отбросьте эти годы. Постройте модель линейной регрессии по годам среднего значения отношения UnemployedDisabled к UnemployedTotal (процента людей с ограниченными возможностями) за месяц и ответьте, какое ожидается значение процента безработных инвалидов в 2020 году при сохранении текущей политики города Москвы?
    
  </details>
  
[Решение:](6_python_advaced/1_analysis/task4.ipynb)
1. Из csv файла загружаем необходимые столбцы.
2. Удалим года, по которым мало измерений и создадим массив вида год:доля безработных людей с ограниченными возможностями.
3. Создадим массивы с годами и доля безработных людей с ограниченными возможностями с формой подходящей для тренировки модели.
4. Построим линейную регрессию исходя из подготовленных данных и сделаем предсказание на 2020 год.
5. Построим график(scatter) известных данныи и на нем же отбразим полюченную регрессию. 
  
</details>
 
## Продвинутый Python. Часть 2: импорт и парсинг данных  
<details>
  <summary>Импорт данных</summary>
  <details>
    <summary>Задание - получение данных по API</summary>
    
Изучите API Геокодера Яндекса и получите ключ API для него в кабинете разработчика. Выполните запрос к API и узнайте долготу точки на карте (Point) для города Самара.
    
  </details>
  
[Решение:](6_python_advaced/2_import_and_parsing/task1.ipynb)
1. Введем api-ключ геокодера.
2. Выполним запрос к геокодеру вида 'Россия,+город+Самара&format=json'.
3. Проверим код ответа геокодера и преобразуем ответ в словать.
4. Получим из словаря код страны и название города.
5. Проверим, что код страны и название города - те что мы ищем и возьмем координаты этого объекта.
6. Выведем долготу.
  
</details>

<details>
  <summary>Парсинг данных</summary>
  <details>
    <summary>Задание - получение котировок акций</summary>
    
Получите данные по котировкам акций и найдите, по какому тикеру был максимальный рост числа сделок (в процентах) за 1 ноября 2019 года.
    
  </details>
  
[Решение:](6_python_advaced/2_import_and_parsing/task2.ipynb)
1. Выполним запрос к бирже и распарсим html ответа при помощи bs4.
2. Найдем таблицы по классу и отбросим лишние.
3. Создадим из таблицы датафрейм, в столбце с процентным изменением сделок исправим тире на знак '-' и уберем символ '%'.
4. Преобразуем этот столбец к float, найдем строку с максимальным значение в этом же столбце и выведим тикер. 
  
</details>

<details>
  <summary>Веб-скрепинг</summary>
  <details>
    <summary>Задание - парсинг интернет-магазина</summary>
    
Используя парсинг данных с маркетплейса beru.ru, найдите, на сколько литров отличается общий объем холодильников Саратов 263 и Саратов 452?
    
  </details>
  
[Решение:](6_python_advaced/2_import_and_parsing/task3.ipynb)
1. Создадим список с интересующими нас товарами.
2. Преобразуем этот список к списку регулярных выражений для поиска товаров в коде. Создадим регулярное выражение для поиска общего объема на странице товара. 
3. Создадим функцию get_link, которая принимает bs-объект(страница с товарами) и regexp(шаблон поиска товара) и возвращает относительную ссылку на товар. Если ссылка не найдена - возвращаем пустую строку.
4. Создадим функцию get_total_volume, которая принимает bs-объект(страница товара) и regexp(шаблон поиска объема) и возвращает объем или 0, если объем не найден.
5. Полючаем список локальных ссылок на все товары функцией get_link в цикле, не пустые значения ссылок преобразуем к абсолютным.
6. Прерходим по полученным ссылкам, парсим их, и находим объемы функцией get_total_volume.
7. Считаем разницу объемов. 
  
</details>

<details>
  <summary>Работа с SQL</summary>
  <details>
    <summary>Задание - загрузка результатов в БД</summary>
    
Соберите данные о моделях холодильников Саратов с маркетплейса beru.ru: URL, название, цена, размеры, общий объем, объем холодильной камеры. Создайте соответствующие таблицы в SQLite базе данных и загрузите полученные данные в таблицу beru_goods.
    
  </details>
  
[Решение:](6_python_advaced/2_import_and_parsing/task4.ipynb)
1. Создадим список c шаблонами(regexp) для поиска товаров.
2. Создадим функцию get_link, которая принимает bs-объект(страница с товарами) и regexp(шаблон поиска товара) и возвращает относительную ссылку на товар. Если ссылка не найдена - возвращаем пустую строку.
3. Создадим функцию get_features, которая принимает bs-объект(страница с товаром) и возвращает список характеристик.
4. Полючаем список локальных ссылок на все товары функцией get_link в цикле, преобразуем к абсолютным.
5. Для каждого найденного товара получим его характеристики функцией get_features.
6. Подключимся к БД и создадим таблицу.
7. Запишим в БД характеристики товаров.
8. Проверим, что данные записались в БД корректно, выполнив заррос на вывод всей таблицы.
  
</details>

## Продвинутый Python. Часть 3: визуализация данных.  
  
<details>
  <summary>Основы Matplotlib</summary>
  <details>
    <summary>Задание - типы визуализации данных</summary>
    
Загрузите данные по ЕГЭ за последние годы, выберите данные за 2018-2019 учебный год. Выберите тип диаграммы для отображения результатов по административному округу Москвы, постройте выбранную диаграмму для количества школьников, написавших ЕГЭ на 220 баллов и выше. Выберите тип диаграммы и постройте ее для районов Северо-Западного административного округа Москвы для количества школьников, написавших ЕГЭ на 220 баллов и выше.
    
  </details>
  
[Решение:](6_python_advaced/3_visualization/task1.ipynb)
1. Загрузим данные.
2. Выберем только интересные нам годы(2018-2019) и столбцы(округа, отличники), сгруппируем по адм. округам.
3. Построим bar-график количества отличников по округам.
4. Выберем только интересные нам годы(2018-2019) и столбцы(районы СЗАО, отличники), сгруппируем по районам.
5. Построим bar-график количества отличников по районам СЗАО.
  
</details>  
  
<details>
  <summary>Визуализация зависимостей</summary>
  <details>
    <summary>Задание - результаты марафона</summary>
    
Загрузите данные по итогам марафона. Приведите время половины и полной дистанции к секундам.  Найдите, данные каких серии данных коррелируют (используя диаграмму pairplot в Seaborn).  Найдите коэффициент корреляции этих серий данных, используя scipy.stats.pearsonr.  Постройте график jointplot для коррелирующих данных.
    
  </details>
  
[Решение:](6_python_advaced/3_visualization/task2.ipynb)
1. Загрузим данные, приведем результаты полумарафона и марафона к секундам.
2. Построим pairplot для данных, обнаружим положительную корреляцию между результатами полумарафона и марафона.
3. Коэффициент корреляции Пирсона между полумарафоном и марафоном.
4. Построим joinplot и просмотрим плотность распределений коррелирующих параметров.
  
</details>

<details>
  <summary>Временные ряды</summary>
  <details>
    <summary>Задание - скользящие средние на биржевых графиках</summary>
    
Используя данные индекса РТС за последние годы постройте отдельные графики закрытия (Close) индекса по дням за 2017, 2018, 2019 годы в единой оси X.  Добавьте на график экспоненциальное среднее за 20 дней для значения Max за 2017 год.  Найдите последнюю дату, когда экспоненциальное среднее максимального дневного значения (Max) в 2017 году было больше, чем соответствующее значение Close в 2019 году (это последнее пересечение графика за 2019 год и графика для среднего за 2017 год).
    
  </details>
  
[Решение:](6_python_advaced/3_visualization/task3.ipynb)
1. Загрузим данные индекса РТС за последние годы, приведем дату к типу datetime, обогатим данные номером дня в году.
2. Создадим холст и оси, где по X-порядковый номер дня в году. 
3. Отобразим уровни закрытия индекса РТС за 2017-2019г от номера дня в году(все 3 графика на одном и том же отрезке по X).
4. Посчитаем скользящее среднее за 20 дней в 2017г. и отобразим его рядом с остальными графиками.
5. Найдем последнюю дату, когда скользящее среднее 20 дней в 2017г. было меньше уровня закрытия в 2019г
  
</details>

<details>
  <summary>Гео-данные и картограммы</summary>
  <details>
    <summary>Задание - объекты культурного наследия России</summary>
    
Изучите набор данных по объектам культурного наследия России (в виде gz-архива) и постройте фоновую картограмму по количеству объектов в каждом регионе России, используя гео-данные. Выведите для каждого региона количество объектов в нем.  Посчитайте число объектов культурного наследия в Татарстане.
    
  </details>
  
[Решение:](6_python_advaced/3_visualization/task4.ipynb)
1. Установим geopandas.
2. Прочитаем геоданные и приведем их к проекции у которой нет проблем с регионами РФ в западном полушарии(epsg:5940).
3. Прочитаем данные по объектам культурного наследия, оставим только необходимые столбцы.
4. Создадим новые стобцы Area(по ним будем сливать датафреймы), в которых будут названия регионов в нижнем регистре.
5. Проверим не совпадающие названия регионов между датафреймами(посчитаем разности множеств).
6. Подготовим словарь исправлений, где ключ-'не правильное' название, а значение 'правильное', для столбца Area датафрейма с геоданными.
7. Исправим значения Area датафрейма с геоданными и убедимся в полном совпадении уникальных значений с этим же столбцом датафрейма культурных объектов.
8. Смерджим эти датафреймы по столбцам Area в датафрей data.
9. Построим фоновую градиентную картограмму количества объектов культурного наследия по субьектам РФ и выведим соответствующее количество в центре субьекта.
10. В датафрейме data найдем запись с республикой Татарстан и получим из нее количество объектов в Татарстане. 
  
</details>

## Продвинутый Python. Часть 4: отчеты и автоматизация.  
<details>
  <summary>Работа с PDF</summary>
  <details>
    <summary>Задание - сборка PDF документа</summary>
    
Используя данные по посещаемости библиотек в районах Москвы постройте круговую диаграмму суммарной посещаемости (NumOfVisitors) 20 наиболее популярных районов Москвы. Создайте PDF отчет  используя файл как первую страницу. На второй странице выведите итоговую диаграмму, самый популярный район Москвы и число посетителей библиотек в нем.
    
  </details>
  
[Решение:]6_python_advaced/4_reports%20and%20automation/task1.ipynb)
1. Скачаем титульную страницу, шрифт и установим необходимые модули.
2. Загрузим данные, отбросим не нужные столбцы.
3. Создадим поле District с легкочитабельным названием района.
4. Сгруппируем данные по названиям районов, проссумируем посетителей по группам, отсортируем по суммам посетителей, возьмем топ-20 районов.
5. Построим pie-диаграмму по 20 самым 'читающим' районам с указанием % доли для каждого района и сохраним ее в файл.
6. Создадим PDF страницу с диаграммой и сохраним ее в файл.
7. Создадим список из отдельных PDF для слияния, добавим метаданные, сольем страницы и сохраним как отдельный PDF файл.
  
</details>

<details>
  <summary>Базовые отчеты</summary>
  <details>
    <summary>Задание - геральдические символы Москвы</summary>
    
Сгенерируйте PDF документ из списка флагов и гербов районов Москвы. На каждой странице документа выведите название геральдического символа (Name), его описание (Description) и его изображение (Picture). 
    
  </details>
  
[Решение:](6_python_advaced/4_reports%20and%20automation/task2.ipyn)
1. Скачаем, шрифт и установим необходимые модули.
2. Создадим функцию add_page, которая создает новую страницу и размещает там название, герб и его описание. Эта функция скачивает герб с сайта op.mos.ru через http прокси.
3. Создадим функцию split_line, которая нарезает описание на строки нужной длины(чтобы они не вылезли за края PDF документа), в зависимости от размера шрифта.
4. Создадим служебные функции line_len и line_offset как вспомогательные для split_line.
5. Загружаем данные, создаем титульный лист(PDF).
6. К титульнуму листу добавляем страницы создаваемые функцией add_page.
7. Сохраняем многостраничный PDF целиком.
  
</details>

<details>
  <summary>Генерация отчетов</summary>
  <details>
    <summary>Задание - многостраничный отчет</summary>
    
Используя данные по активностям в парках Москвы создайте PDF отчет, в котором выведите:      Диаграмму распределения числа активностей по паркам, топ10 самых активных;      Таблицу активностей по всем паркам в виде Активность-Расписание-Парк.
    
  </details>
  
[Решение:](6_python_advaced/4_reports%20and%20automation/task3.ipynb)
1. Установим wkhtmltopdf и pdfkit.
2. Составим html шаблон отчета.
3. Загрузим данные по паркам, отбросим лишние столбцы, извлечем названия парков.
4. Построим bar и line диаграммы активностей по паркам.
5. Преобразуем диаграмму в ascii.
6. Отрендерим html шаблон вставив туда картинку и таблицу полученную из датафрейма.
7. Создадим из html документа PDF и сохрание его.
  
</details>

<details>
  <summary>Отправка email и интеграция</summary>
  <details>
    <summary>Задание - объекты культурного наследия России</summary>
    
Соберите отчет по результатам ЕГЭ в 2018-2019 году и отправьте его в HTML формате по адресу support@ittensive.com, используя только Python.  В отчете должно быть:      общее число отличников (учеников, получивших более 220 баллов по ЕГЭ в Москве),     распределение отличников по округам Москвы,     название школы с лучшими результатами по ЕГЭ в Москве.  Диаграмма распределения должна быть вставлена в HTML через data:URI формат (в base64-кодировке).  Дополнительно: приложите к отчету PDF документ того же содержания (дублирующий письмо).
    
  </details>
  
[Решение:](6_python_advaced/4_reports%20and%20automation/task4.ipynb)
1. Установим wkhtmltopdf.
2. Составим html шаблон отчета.
3. Загрузим данные по ЕГЭ, оставим нужные нам поля и годы.
4. Посчитаем число отличников, найдем лучшую школу.
5. Сгруппируем отличников по административным округам, на основе этих данных построим pie-диаграмму с % долями отличников.
6. Сохраним диаграмму в ascii.
7. Отрендерим шаблон, вставив туда диаграмму и данные по отличникам и лучшей школе.
8. Подключимся к почтовому серверу.
9. Сформируем заголовки письма и его текстовую часть из отрендеренного шаблона.
10. Создадим PDF из отрендеренного шаблона и добавим этот файл как вложение.
11. Отправим письмо.
  
</details>
