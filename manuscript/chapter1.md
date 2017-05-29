# Обзор 
Цель этой книги - предоставить Вам практическое руководство по веб-разработке с использованием *Django* и *Python*. Эта книга предназначена в первую очередь для студентов и представляет собой пошаговое руководство, которое, шаг за шагом, вводит Вас в процесс создания и запуска веб-приложения с помощью Django.

Эта книга стремиться дополнить как [официальное Руководство Django](https://docs.djangoproject.com/en/1.9/intro/tutorial01/), так и множество других прекрасных обучающих материалов доступных в интернете. Аккумулируя всю информацию в одном месте, эта книга заполняет многие пробелы в официальной документации Django, предоставляя основанный на примерах подход к изучению фреймворка Django. Более того, данная книга содержит введение ко многим аспектам разработки пррофессиональных веб-приложений (т.е. HTML, CSS, JavaScript и т.д.).

## Зачем работать с этой книгой?
**Эта книга сэекономит вам время.** Нам частенько приходилось видеть, как одаренные студенты застревали, проводя многие часы в бесплодной борьбе с Django и прочими аспектами веб-разработки. Чаще всего, проблема заключалась в том, что какая-то важная часть информации не была объяснена или была не до конца понятна. Хотя такие случайные остановки обычно занимают не более 10-15 минут, иногда на их решение может уйти множество часов. Поэтому, мы попытались устранить как можно больше таких препятствий. Это значит, что вы сможете продолжить разработку своего приложения вместо того, чтобы спотыкаться на каждом шагу.

**Эта книга снизит кривую обучения.** Фреймворки веб-приложений могут сэкономить Вам кучу сил и времени. При условии, что Вы умеете ими пользоваться, конечно же! Чаще всего кривая обучения выглядит как крутой холм. Эта книга поможет вам идти по нему - и идти быстро, на примере показывая, как все части подходят друг к другу.

**Эта книга позволит улучшить ваш рабочий процесс.** Using web application frameworks requires you to pick up and run with a particular design pattern - so you only have to fill in certain pieces in certain places. After working with many students, we heard lots of complaints about using web application frameworks - specifically about how they take control away from them (i.e. [inversion of control](https://en.wikipedia.org/wiki/Inversion_of_control)).  To help you, we've created a number of *workflows* to focus your development process so that you can regain that sense of control and build your web application in a disciplined manner.

**Эта книга предназначена не для чтения.** Whatever you do, *do not read this book!* It is a hands-on guide to building web applications in Django. Reading is not doing. To increase the value you gain from this experience, go through and develop the application. When you code up the application, *do not just cut and paste the code.* Type it in, think about what it does, then read the explanations we have provided to describe what is going on. If you still do not understand, then check out the Django documentation, go to [Stack Overflow](http://stackoverflow.com/questions/tagged/django) or other helpful websites and fill in this gap in your knowledge. If you are really stuck, get in touch with us, so that we can improve this resource - we've already had contributions from [numerous other readers](#chapter-acks)!

## Что Вы узнаете
In this book, we will be taking an exampled-based approach. The book will show you how to design a web application called *Rango* ([see the Design Brief below](#overview-design-brief-label)). Along the way, we'll show you how to perform the following key tasks.

* **Как настроить среду разработки** - включая как использовать терминал (командную строку), виртуальное окружение, установщик `pip`, как работать с Git, и прочее.
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

At the end of each chapter, we have included a number of exercises designed to push you harder and to see if you can apply what you have learned. The later chapters of the book provide a number of open development exercises along with coded solutions and explanations.

X> ### Exercises will be clearly delineated like this!
X> In each chapter we have added a number of exercises to test your knowledge and skill.
X>
X> *You will need to complete these exercises as the subsequent chapters are dependent on them.*
X>
X> Don't worry if you get stuck, though, as you can always check out our solutions to all the exercises on our [*GitHub* repository](https://github.com/leifos/tango_with_django_19).


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

We've selected these technologies and services as they are either fundamental to web development, and/or enable us to provide examples on how to integrate your web application with CSS toolkits like *Twitter Bootstrap*, external services like those provided by the *Webhose API* and deploy your application quickly and easily with *PythonAnywhere*.

{pagebreak}

## Rango: Первоначальный дизайн и спецификации {#overview-design-brief-label}
The focus of this book will be to develop an application called *Rango*. As we develop this application, it will cover the core components that need to be developed when building any web application. To see a fully functional version of the application, you can visit the [How to Tango with Django website](http://www.tangowithdjango.com/).

### Коротко о дизайне
Your client would like you to create a website called *Rango* that lets users browse through user-defined categories to access various web pages. In [Spanish, the word rango](https://www.vocabulary.com/dictionary/es/rango) is used to mean *"a league ranked by quality"* or *"a position in a social hierarchy"*.

* For the **main page** of the Rango website, your client would like visitors to be able to see:
	* the *five most viewed pages*;
	* the *five most viewed (or rango'ed) categories*; and
	* *some way for visitors to browse or search* through categories.
* When a user views a **category page**, your client would like Rango to display:
	* the *category name, the number of visits, the number of likes*, along with the list of associated pages in that category (showing the page's title, and linking to its URL); and
	* *some search functionality (via the search API)* to find other pages that can be linked to this category.
* For a particular category, the client would like: the *name of the category to be recorded*; the *number of times each category page has been visited*; and how many users have *clicked a "like" button* (i.e. the page gets rango'ed, and voted up the social hierarchy).
* *Each category should be accessible via a readable URL* - for example, `/rango/books-about-django/`.
* Only *registered users will be able to search and add pages to categories*. Visitors to the site should therefore be able to register for an account.

At first glance, the specified application to develop seems reasonably straightforward. In essence, it is just a list of categories that link to pages. However, there are a number of complexities and challenges that need to be addressed. First, let's try and build up a better picture of what needs to be developed by laying down some high-level designs.

X> ### Exercises
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
![Overview of the 3-tier system architecture for our Rango application.](images/rango-ntier-architecture.png)

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

* ``/`` or ``/rango/`` will point to the main / index page.
* ``/rango/about/`` will point to the about page.
* ``/rango/category/<category_name>/`` will point to the category page for ``<category_name>``, where the category might be:
	* games;
	* python-recipes; or
	* code-and-compilers.

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

