# Обзор 
Цель этой книги - предоставить Вам практическое руководство по веб-разработке с использованием *Django* и *Python*. Эта книга предназначена в первую очередь для студентов и представляет собой пошаговое руководство, которое, шаг за шагом, вводит Вас в процесс создания и запуска веб-приложения с помощью Django.

Эта книга стремиться дополнить как [официальное Руководство Django](https://docs.djangoproject.com/en/1.9/intro/tutorial01/), так и множество других прекрасных обучающих материалов доступных в интернете. Аккумулируя всю информацию в одном месте, эта книга заполняет многие пробелы в официальной документации Django, предоставляя основанный на примерах подход к изучению фреймворка Django. Более того, данная книга содержит введение ко многим аспектам разработки пррофессиональных веб-приложений (т.е. HTML, CSS, JavaScript и т.д.).

## Зачем работать с этой книгой?
**Эта книга сэкономит вам время.** Нам частенько приходилось видеть, как одаренные студенты застревали, проводя многие часы в бесплодной борьбе с Django и прочими аспектами веб-разработки. Чаще всего, проблема заключалась в том, что какая-то важная часть информации не была объяснена или была не до конца понятна. Хотя такие случайные остановки обычно занимают не более 10-15 минут, иногда на их решение может уйти множество часов. Поэтому, мы попытались устранить как можно больше таких препятствий. Это значит, что вы сможете продолжить разработку своего приложения вместо того, чтобы спотыкаться на каждом шагу.

**Эта книга снизит кривую обучения.** Фреймворки веб-приложений могут сэкономить Вам кучу сил и времени. При условии, что Вы умеете ими пользоваться, конечно же! Чаще всего кривая обучения выглядит как крутой холм. Эта книга поможет вам идти по нему - и идти быстро, на примере показывая, как все части подходят друг к другу.

**Эта книга позволит улучшить ваш рабочий процесс.** Используя фреймворки для разработки веб-приложений, Вы вынужденны работать с определенным шаблоном проектирования - а именно заполнять некоторые фрагменты информацией, в отведенных для этого местах. После работы со множеством студентов, мы встретились с многочисленными жалобами на процесс использования таких фреймворков - преимущественно на то, что они отбирают управление у программистов (см. [Инверсия управления](https://ru.wikipedia.org/wiki/Инверсия_управления)). Что бы вам помочь, мы создали ряд *рабочих процессов*, фокусируя ваш процесс разработки так, что Вы сможете восстановить свое ощущение управления процессом и дисциплинированно создать Ваше веб-приложение.

**Эта книга предназначена не для чтения.**Что бы Вы ни делали, *НЕ ЧИТАЙТЕ ЭТУ КНИГУ!* Это практическое руководство по созданию веб-приложения на Django. Одного чтения тут не достаточно. Что бы увеличить количество получаемого вами опыта от этой книги, просто создайте свое приложение в процессе чтения. Во время программирования не пользуйтесь трюком *копировать\вставить*. Пишите все руками, думайте над тем что делает ваш код, потом прочтите написанное нами обьяснение, чтобы описать, что происходит. И если вам по прежнему будет непонятно, , то обратитесь к официальной документации Django или отправляйтесь на [Stack Overflow](http://stackoverflow.com/questions/tagged/django), или на любой другой полезный ресурс, что заполнит пробелы в ваших знаниях. И если даже после этого вам что-то будет не понятно, то свяжитесь с нами, что бы мы могли улучшить нашу книгу - мы уже получили множество предложений по улучшению от [других наших читателей](#chapter-acks)!

## Что Вы узнаете
В данной книге мы пользуемся основанным на примерах подходом к обучению. Мы покажем Вам как разработать веб-приложение под названием  *Rango* ([см. Коротко о дизайне](#overview-design-brief-label)). По пути мы покажем вам, как выполнять следующие ключевые задачи.

* **Как настроить среду разработки** - включая использование терминала (командной строки), виртуального окружения, установщика `pip`, как работать с Git, и прочее.
* **Установить Django проект** и создать базовое приложение Django.
* **Настроить Django проект** для обслуживания статичных и других медиа файлов.
* Работать с шаблоном проектирования Django *Модель-Вид-Шаблон*.
* **Создавать модели базы данных** и использовать функциональность [*объектно-реляционного отображения (ORM)*](https://ru.wikipedia.org/wiki/ORM) предоставляемого нам Django.
* **Создавать формы**, использующие модели базы данных для создания динамически генерируемых веб-страниц.
* Использовать сервисы **аутентификации пользователей** предоставляемые нам Django.
* Включать в состав своего Django приложения **внешние сервисы**.
* Включать в свое приложение *Каскадные таблицы стилей (CSS)* и *JavaScript*.
* **Применять CSS** так, что бы ваше приложение имело профессиональный внешний вид.
* Работать с **файлами cookie и сессиями** в Django.
* Включать в свое приложение более продвинутые функции, такие как *AJAX*.
* **Развертывать приложения** на веб-сервере с помощью *PythonAnywhere.*

В конце каждой главы, мы добавили несколько упражнений спецально созданных для того, что бы мотивировать вас и посмотреть чему вы смогли научиться. В последних главах книги, будут представлены несколько упражнений со свободным процессом решения, а так же код решений задач с обьяснениями.

X> ### Упражнения будут выделены, вот таким образом!
X> К каждой главе мы добавили несколько задач что бы прроверить ваши знания и навыки.
X>
X> *Вам надо выполнить эти упражнения, так как последующие главы опираются на них.*
X>
X> Не волнуйтесь если вы застряли, поскольку Вы всегда можете подсмотреть наше решение ко всем задачам в нашем [репозитории *GitHub*](https://github.com/leifos/tango_with_django_19).


{pagebreak}

## Технологии и Сервисы
В ходе этой книги мы будем использовать различные технологии и внешние сервисы, такие как:

* Язык программирования [Python](http://www.python.org);
* [Менеджер пакетов Pip](http://www.pip-installer.org);
* [Django](https://www.djangoproject.com);
* Система контроля версий [Git](http://git-scm.com);
* [GitHub](https://github.com);
* [HTML](http://www.w3.org/html/);
* [CSS](http://www.w3.org/Style/CSS/);
* Язык программирования [JavaScript](https://www.javascript.com/);
* Библиотека [JQuery](http://jquery.com);
* Фреимворк [Twitter Bootstrap](http://getbootstrap.com/);
* [Webhose API](https://webhose.io/) (предоставляет нам *API поиска*); и
* Хостинг [PythonAnywhere](https://www.pythonanywhere.com);

Мы выбрали эти технологии и сервисы, поскольку они не только являются ключивыми для веб-разработки, но и позволяют нам приводить примеры того, как интегрировать в ваше веб-приложение CSS инструментарий наподобии *Twitter Bootstrap*, как использовать внешние сервисы, подобные тем, которые предоставляются * Webhose API * и как развернуть ваше веб-приложение быстро и удобно с помощью *PythonAnywhere*.  

{pagebreak}

## Rango: Первоначальный дизайн и спецификации {#overview-design-brief-label}
Эта книга сфокусирована на разработке приложения под названием *Rango*. И по мере его создания, будет охватыватся все больше ключевых компонентов, необходимых для построения любых веб-приложений. Если вы хотите увидеть итоговый результат в действии, то вы можете посетить наш [сайт How to Tango with Django](http://www.tangowithdjango.com/).

### Коротко о дизайне
Ваш клиент хочет создать веб-сайт под названием *Rango*, который позволит пользователям просматривать определяемые пользователями категории и посещать сайты, закрепленные за этими категориями. В [Испанском языке, слово rango](https://www.vocabulary.com/dictionary/es/rango) обозначает *"лига ранжированная по качеству"* или *"позиция в социальной иерархии"*.

* На **главной странице (main page)** сайта Rango, ваш клиен хочет что бы, посетители могли видеть:
	* *пятерку самых просматриваемых страниц*;
	* *пятерку самых просматриваемых (или rango-вых) категорий*; и
	* *какой то способ для посетителей удобно просматривать и искать* категории.
* Когда пользователь смотрит на **страницу категории**, клиент хочет что бы Rango показывал:
	* *имя категории, количество посещений, количество лайков*, а так же список связанных с этой категорией страниц (их названиие и ссылку); и
	* *какую либо поисковую систему (реализованную поисковым API)* предназначенную для поиска других страниц, которые могут относиться к данной категории.
* Для каждой категории, клиент хочет видеть: *имя категории*; *количество посещений каждой страницы категории*; и как много пользователей *кликнула на кнопку "like"* (т.е. страница становится rango-вой, и движется вверх в социальной иерархии).
* *Каждая категория должна быть доступна через удобочитаемый URL* - например, `/rango/books-about-django/`.
* Только * зарегестрированные пользователи будут способны искать в категориях и добовлять туда страницы*. Посетители сайта, так же должны иметь способность зарегистрировать аккаунт.

At first glance, the specified application to develop seems reasonably straightforward. In essence, it is just a list of categories that link to pages. However, there are a number of complexities and challenges that need to be addressed. First, let's try and build up a better picture of what needs to be developed by laying down some high-level designs.

X> ### Упражнения
X> Before going any further, think about these specifications and draw up the following design artefacts.
X>
X> * An **N-Tier or System Architecture** diagram.
X> * **Wireframes** of the main and category pages.
X> * A series of **URL mappings** for the application.
X> * An [***Entity-Relationship (ER)***](https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model) diagram to describe the data model that we'll be implementing.
X>
X> Try these exercises out before moving on - even if you aren't familiar with system 
X> architecture diagrams, wireframes or ER diagrams, how would you explain and describe what 
X> you are going to build.

{pagebreak}

### N-уровневая архитектура

Высокоуровневая архитектура большинства web приложений представляет собой *3-уровневую архитектуру.* Rango будет представителем этой архитектуры, поскольку он взаимодействует с внешними службами.

{id="fig-ntier"}
![Обзор 3-уровневой системной архитектуры для нашего приложения Rango.](images/rango-ntier-architecture.png)

Since we are building a web application with Django, we will use the following technologies for the following tiers.

* The **client** will be a Web browser (such as *Chrome*, *Firefox*, and *Safari*) which will render HTML/CSS pages.
* The **middleware** will be a *Django* application, and will be dispatched through Django's built-in development Web server while we develop.
* The **database** will be the Python-based *SQLite3* Database engine.
* The **search API** will be the search API.

For the most part, this book will focus on developing the middleware. It should however be quite evident from the [system architecture diagram](#fig-ntier) that we will have to interface with all the other components.

### Каркасы страниц
Wireframes are great way to provide clients with some idea of what the application should look like when complete. They save a lot of time, and can vary from hand drawn sketches to exact mockups depending on the tools that you have at your disposal. For our Rango application, we'd like to make the index page of the site look like the [screenshot below](#fig-index-page). Our category page is also [shown below](#fig-cat-page).

{id="fig-index-page"}
![The index page with a categories search bar on the left, also showing the top five pages and top five categories.](images/ch1-rango-index.png)

{id="fig-cat-page"}
![The category page showing the pages in the category (along with the number of views). Below, a search for *Python* has been conducted, with the results shown underneath.](images/ch1-rango-cat-page.png)

### Сопоставления страниц и URL-адресов
From the specification, we have already identified two pages that our application will present to the user at different points in time. To access each page we will need to describe URL mappings. Think of a URL mapping as the text a user will have to enter into a browser's address bar to reach the given page. The basic URL mappings for Rango are shown below.

* ``/`` или ``/rango/`` ведет на главную / index страницу.
* ``/rango/about/`` ведет на страницу о проекте.
* ``/rango/category/<category_name>/`` ведет на страницу категории с именем ``<category_name>``, где категорией может быть:
	* games (игры);
	* python-recipes (python-рецепты); или
	* code-and-compilers (код-и-компиляторы).

As we build our application, we will probably need to create other URL mappings. However, the ones listed above will get us started and give us an idea of the different pages. Also, as we progress through the book, we will flesh out how to construct these pages using the Django framework and use its [Model-View-Template](https://docs.djangoproject.com/en/1.9/) design pattern. However, now that we have a gist of the URL mappings and what the pages are going to look like, we need to define the data model that will house the data for our Web application.

### Диаграмма сущность-связь {#overview-er}
Given the specification, it should be clear that we have at least two entities: a *category* and a *page*. It should also be clear that a *category* can house many *pages*. We can formulate the following ER Diagram to describe this simple data model.

{id="fig-rango-erd"}
![The Entity Relationship Diagram of Rango's two main entities.](images/rango-erd.png)

Note that this specification is rather vague. A single page could in theory exist in one or more categories. Working with this assumption, we could model the relationship between categories and pages as a [many-to-many relationship](https://en.wikipedia.org/wiki/Many-to-many_(data_model)). This approach however introduces a number of complexities, so we will make the simplifying assumption that *one category contains many pages, but one page is assigned to one category.* This does not preclude that the same page can be assigned to different categories - but the page would have to be entered twice, which is not ideal.

D> ### Take Note!
D> Get into the habit of noting down any working assumptions that you make, just like the one-to-many relationship assumption that we assume above. You never know when they may come back to bite you later on! By noting them down, this means you can communicate it with your development team and make sure that the assumption is sensible and that they are happy to proceed under such an assumption.

With this assumption, we then produce a series of tables that describe each entity in more detail. The tables contain information on what fields are contained within each entity.  We use Django `ModelField` types to define the type of each field (i.e. `IntegerField`, `CharField`, `URLField` or `ForeignKey`). Note that in Django *primary keys* are implicit such that Django adds an `id` to each Model, but we will talk more about that later in the Models and Database chapter.


#### Модель Категория

| Field   | Type            |
|---------|-----------------|
| `name`  | `CharField`     | 
| `views` | `IntegerField`  |
| `likes` | `IntegerField`  |

#### Модель Страница

| Field      | Type           |
|------------|----------------|
| `category` | `ForeignKey`   | 
| `title`    | `CharField`    |
| `url`      | `URLField`     |
| `views`    | `IntegerField` |

We will also have a model for the `User` so that they can register and login. We have not shown it here, but shall introduce it later in the book when we discuss User Authentication. In the following chapters, will we see how to instantiate these models in Django and how to use the built-in ORM to connect to the database.

## Итог
These high level design and specifications will serve as a useful reference point when building our Web application. While we will be focusing on using specific technologies, these steps are common to most database driven websites. It's a good idea to become familiar with reading and producing such specifications and designs so that you can communicate your designs and ideas with others. Here we will be focusing on using Django and the related technologies to implement this specification.


T> ### Стиль программирования "Вырезать/Вставить"
T>
T> As you progress through the tutorial, you'll most likely be tempted to cut and paste the code from the book to your code editor.
T> **However, it is better to type in the code.** We know that this is a hassle, but it will help you to remember the process better and the commands that you will be using later on.
T>
T> Furthermore, cutting and pasting Python code is asking for trouble. Whitespace can end up being interpreted as spaces, tabs or a mixture of spaces and tabs. This will lead to all sorts of weird errors, and not necessarily indent errors. If you do cut and paste code be wary of this. Pay particular attention to this if you're using Python 3 - inconsistent use of tabs and spaces in your code's indentation will lead to a `TabError`.
T> 
T> Most code editors will show the whitespace and whether it is tabs or spaces. If so, turn it on and save yourself a lot of confusion.

