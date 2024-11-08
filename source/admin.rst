.. sectionauthor:: Дмитрий Барышников <dmitry.baryshnikov@nextgis.ru>

.. _ngfv_admin:

Административный интерфейс
===========================

.. warning:: Больше не поддерживается

Что это такое
------------------------

Комплекс состоит из трёх программ: 

1. Серверное программное обеспечение.
2. Мобильное приложение "Лесной инспектор".
3. Мобильное приложение "Сохрани лес". 

На этой странице описаны операции с серверным программным обеспечением. Оно хранит 
данные и обменивается ими с мобильными приложениями.

Для администрирования вам потребуется:

1. URL сервера.
2. Логин и пароль.

Описание слоёв на сервере
----------------------------------------

* Геоданные
* * Лесоделение - эти данные передаются в приложение "Лесной инспектор".
* * Общедоступное
* * * Сообщения граждан - данные, поступающие из приложения "Сохрани лес".
* * * Точки лесонарушений - места, в которых были зафиксированы лесонарушения гражданами, 
      работниками лесного хозяйства или при помощи автоматизированной обработки ДДЗ.
* * Ограниченное - эти данные передаются в приложение "Лесной инспектор".

Процедура добавления нового инспектора
-----------------------------------------

Процедура регистрации нового инспектора в базе состоит из добавления пользователя в 
базу серверного ПО и присвоения ему географического полигона работы.

1. Зайдите в раздел Панель управления --> Пользователи --> Список.
2. Проверьте, нет ли в списке уже этого пользователя.
3. Нажмите Пользователи --> Создать.
4. Заполните поля, придумайте логин и пароль для этого пользователя, укажите группу 
   Инспекторы. Запишите логин и пароль, нажмите кнопку Создать. 
5. С главной страницы зайдите Сервисы --> WFS сервис --> WFS сервис. На экране выведется адрес, 
   вроде http://dev.nextgis.com/fv/api/resource/10/wfs. Скопируйте этот адрес в буфер.
6. Запустите программу NextGIS QGIS. 
7. Для добавления базовой карты: Нажмите Интернет --> QuickMapServices. Выберите подложку, 
   например OSM Mapnik.

.. note:: Eсли под текущую операционную систему нет сборки NextGIS QGIS, воспользуйтесь программой QGIS и установите в ней плагин QuickMapServices.

8. Нажмите Слой --> Добавить слой --> Добавить слой WFS.
9. В открывшемся окне "Добавление слоя WFS" нажмите "Создать". В открывшемся окне введите: 
   Название - Пользователи системы Лесной инспектор, адреc - URL из шага 5. Логин и пароль - те, 
   под которым вы работаете в серверном ПО. 
   (см. так же http://docs.nextgis.ru/docs_ngqgis/source/map.html#wfs).

10. Затем нажмите Подключиться. В списке появятся слои, выберите слой "Инспекторы", 
    нажмите кнопку "Добавить". 
11. Выделите слой "Инспекторы" в списке слоёв, включите режим редактирования, найдите на 
    панели кнопку "Добавить объект". Нарисуйте на карте область, нажмите правую кнопку мыши.
12. В открывшемся окне укажите **login**: логин нового инспектора, **pass_id** - номер удостоверения нового 
    инспектора или б/н, **user** - имя инспектора в формате фамилия и инициалы, **user_desc** - полное имя инспектора с указанием должности. 
    **Login** должен совпадать с параметрами пользователя, которые вы добавили в пункте 4.
13. Нажмите Ok, затем - Сохратить правки слоя или Выйти из режима редактирования.

Добавление инспектора закончено.

Процедура увольнения инспектора
-----------------------------------------

Процедура увольнения инспектора состоит из отключения пользователя в административном 
интерфейсе серверного ПО.

1. Зайдите в раздел Панель управления --> Пользователи --> Список.
2. Найдите пользователя в списке. Нажмите на его кнопку редактирования.
3. В открывшемся окне включите поле Отключён.

Процедура отключения пользователя
------------------------------------------------

Процедура отключения пользователя состоит из отключения пользователя 
в административном интерфейсе серверного ПО.

1. Зайдите в раздел Панель управления --> Пользователи --> Список.
2. Найдите пользователя в списке. Нажмите на его кнопку редактирования.
3. В открывшемся окне включите поле Отключён.

Процедура проверки работоспособности 
------------------------------------------------

Для проверки работоспособности приложения следует выполнить следующую последовательность шагов:

1. Зайдите в слой Геоданные --> Ограниченные --> Документы. Откройте Таблицу Атрибутов.
2. В таблице атрибутов вы должны видеть те данные, которые отправляются из приложения 
   "Лесной инспектор".


Для мобильного приложения "Лесной инспектор" адреса серверов берутся из файла, который 
хранится на нашем сервере. В нем прописаны регионы и адреса ваших серверов с данными. 
Пользователь мобильного приложения "Лесной инспектор" при первом запуске видит этот 
список и выбирает свой регион. 
