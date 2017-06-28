#AJAX в Django с использованием JQuery {#chapter-ajax}
AJAX представляет собой комбинацию технологий, которые, объединяясь вместе, уменьшают количество загрузок страницы. Вместо перезагрузки страницы целиком, перезагружается только часть страницы или ее данные. Если вы не использовали AJAX раньше или вы хотите узнать о технологи больше, то посетите [ресурсы посвященые AJAX на вебсайте Mozilla](https://developer.mozilla.org/en-US/docs/AJAX).

Для упрощения AJAX запросов, мы будем использовать библиотеку JQuery. Обратите внимание, что если вы используете набор Twitter CSS Bootstrap, то JQuery уже добавлена в проект. Мы используем [JQuery 3-й версии](https://ajax.googleapis.com/ajax/libs/jquery/3.0.0/jquery.min.js). В противном случае, скачайте библиотеку JQuery и включите ее в свой проект, т.е. сохраните файл в директории `static/js/` вашего проекта.

## AJAX Функциональность 
Давайте модернизируем наше приложение и добавим ряд функций, которые будут использовать AJAX, например:

- добавим кнопку "Like", что бы зарегистрированные пользователи могли "лайкнуть" понравившуюся категорию;
- добавим выпадающие предложения для категорий - что бы когда пользователь вводил название категории, он мог видеть все категории подходящие под введеные слова; и
- добавим кнопку "Add", что бы зарегистрированные пользователи могли легко и быстро добавлять Страницы в Категории при выполнении поиска.

Создадим новый фаил, назовем его `rango-ajax.js` и сохраним его в папке `static/js/`. Затем, дополним *базовый* шаблон:

{lang="html",linenos=off}
	<script src="{% static "js/jquery.min.js" %}"></script>
	<script src="{% static "js/rango-ajax.js" %}"></script>

Здесь мы предполагаем, что вы загрузили версию библиотеки JQuery, но можете просто прямо ссылаться на нее:

{lang="html",linenos=off}
	<script 
	    src="https://ajax.googleapis.com/ajax/libs/jquery/3.0.0/jquery.min.js">
	</script>

If you are using Bootstrap, then scroll to the bottom of the template code, You will see the JQuery library being imported at the end.
You can then add a link to `rango-ajax.js` after the JQuery library import.

Теперь, когда мы установили JQuery и подготовились к размещению AJAX кода на стороне клиента,теперь мы можем модифицировать Rango.

## Добавление кнопки Like
It would be nice to let users, who are registered, denote that they *"like"* a particular category. In the following workflow, we will let users "like" categories, but we will not be keeping track of what categories they have "liked". A registered user could click the like button multiple times if they refresh the page. If we wanted to keep track of their likes, we would have to add in an additional model, and other supporting infrastructure, but we'll leave that as an exercise for you to complete.

### Рабочий процесс
Что бы позволить пользователям "лайкать" конкретные категории, выполните следующий рабочий процесс.

- В шаблон `category.html`:
	- Добавить кнопку "Like" с `id="like"`.
	- Добавить в шаблон тэг для отображения колличества лайков: `{{ category.likes }}`
	- Поместить его внутрь тэга `div` с `id="like_count"`, т.е. `<div id="like_count">{{ category.likes }} </div>`
	- Это позволит шаблону принимать "лайки" и отображать их колличество для категорий.
	- Note, since the `category()` view passes a reference to the category object, we can use that to access the number of likes, with `{{ category.likes }}` in the template
- Create a view called, `like_category` which will examine the request and pick out the `category_id` and then increment the number of likes for that category.
	- Don't forgot to add in the url mapping; i.e. map the `like_category` view to `rango/like_category/`. The GET request will then be `rango/like_category/?category_id=XXX`
	- Instead of returning a HTML page have this view will return the new total number of likes for that category.
- Now in `rango-ajax.js` add the JQuery code to perform the AJAX `GET` request.
	- If the request is successful, then update the `#like_count` element, and hide the like button.

### Обновление Шаблона Категории
To prepare the template, we will need to add in the "like" button with `id="like"` and create a `<div>` to display the number of likes `{{% category.likes %}}`. To do this, add the following `<div>` to the *category.html* template after the `<h1>{{ category.name }}</h1>` tag.

{lang="html",linenos=off}
	<div>
	<strong id="like_count">{{ category.likes }}</strong> people like this category
	{% if user.is_authenticated %}
	    <button id="likes" data-catid="{{category.id}}" 
	        class="btn btn-primary  btn-sm" type="button">
	        Like
	    </button>
	{% endif %}
	</div>

### Create a Like Category View
Create a new view called, `like_category` in `rango/views.py` which will examine the request and pick out the `category_id` and then increment the number of likes for that category.

{lang="python",linenos=off}
	from django.contrib.auth.decorators import login_required
	
	@login_required
	def like_category(request):
	    cat_id = None
	    if request.method == 'GET':
	    cat_id = request.GET['category_id']
	    likes = 0
	    if cat_id:
	        cat = Category.objects.get(id=int(cat_id))
	        if cat:
	            likes = cat.likes + 1
	            cat.likes =  likes
	            cat.save()
	    return HttpResponse(likes)

On examining the code, you will see that we are only allowing authenticated users to even access this view because we have put a decorator `@login_required` before our view. 

Note that the view assumes that a variable `category_id` has been passed to it via a `GET` request so that we can identify the category to update. In this view, we could also track and record that a particular user has "liked" this category if we wanted - but we are keeping it simple to focus on the AJAX mechanics.

Don't forget to add in the URL mapping, into `rango/urls.py`. Update the `urlpatterns` by adding in:

{lang="python",linenos=off}
	url(r'^like/$', views.like_category, name='like_category'),

### Создание запроса AJAX
Теперь в "rango-ajax.js" вам надо добавить немного кода JQuery  что бы выполнить AJAX `GET` запрос. Добавте нижеследующий код:

{lang="javascript",linenos=off}
	$('#likes').click(function(){
	    var catid;
	    catid = $(this).attr("data-catid");
	    $.get('/rango/like/', {category_id: catid}, function(data){
	        $('#like_count').html(data);
	            $('#likes').hide();
	    });
	});

This piece of JQuery/JavaScript will add an event handler to the element with id `#likes`, i.e. the button. When clicked, it will extract the category ID from the button element, and then make an AJAX `GET` request which will make a call to `/rango/like/` encoding the `category_id` in the request. If the request is successful, then the HTML element with ID `like_count` (i.e. the `<strong>` ) is updated with the data returned by the request, and the HTML element with ID `likes` (i.e. the `<button>`) is hidden.

There is a lot going on here, and getting the mechanics right when constructing pages with AJAX can be a bit tricky. Essentially, an AJAX request is made given our URL mapping when the button is clicked. This invokes the `like_category` view that updates the category and returns the new number of likes. When the AJAX request receives the response, it updates parts of the page, i.e. the text and the button. The `#likes` button is hidden.

##Adding Inline Category Suggestions
It would be really neat if we could provide a fast way for users to find a category, rather than browsing through a long list. To do this we can create a suggestion component that lets users type in a letter or part of a word, and then the system responds by providing a list of suggested categories, that the user can then select from. As the user types a series of requests will be made to the server to fetch the suggested categories relevant to what the user has entered.

### Рабочий процесс
To do this you will need to do the following.

- Create a parameterised function called `get_category_list(max_results=0, starts_with='')` that returns all the categories starting with `starts_with` if `max_results=0` otherwise it returns up to `max_results` categories.
	- The function returns a list of category objects annotated with the encoded category denoted by the attribute, `url`
- Create a view called *suggest\_category* which will examine the request and pick out the category query string.
	- Assume that a GET request is made and attempt to get the *query* attribute.
	- If the query string is not empty, ask the Category model to get the top 8 categories that start with the query string.
	- The list of category objects will then be combined into a piece of HTML via template.
	- Instead of creating a template called `suggestions.html` re-use the `cats.html` as it will be displaying data of the same type (i.e. categories).
	- To let the client ask for this data, you will need to create a URL mapping; let's call it *suggest*.

With the URL mapping, view, and template in place, you will need to update the `base.html` template to provide a category search box, and then add in some JavaScript/JQuery code to link up everything so that when the user types the suggested categories are displayed.

In the `base.html` template modify the sidebar block so that a div with an id="cats" encapsulates the categories being presented. The JQuery/AJAX will update this element. Before this `<div>` add an input box for a user to enter the letters of a category, i.e.:

{lang="html",linenos=off}
	<input  class="input-medium search-query" type="text" 
	     name="suggestion" value="" id="suggestion" />

With these elements added into the templates, you can add in some JQuery to update the categories list as the user types.

- Associate an on keypress event handler to the *input* with `id="suggestion"`
- `$('#suggestion').keyup(function(){ ... })`
- On keyup, issue an ajax call to retrieve the updated categories list
- Then use the JQuery `.get()` function i.e. `$(this).get( ... )`
- If the call is successful, replace the content of the `<div>` with id="cats" with the data received.
- Here you can use the JQuery `.html()` function i.e. `$('#cats').html( data )`

X> ###Упражнения
X> - Update the population script by adding in the following categories: `Pascal`, `Perl`, `PHP`, `Prolog`, `PostScript` and `Programming`. 
X> These additional categories will make the demo of the inline category suggestion functionality more impressive.

### Параметризация `get_category_list()`
In this helper function, we use a filter to find all the categories that start with the string supplied. The filter we use will be `istartwith`, this will make sure that it doesn't matter whether we use uppercase or lowercase letters. If it on the other hand was important to take into account whether letters was uppercase or not you would use `startswith` instead.

{lang="python",linenos=off}
	def get_category_list(max_results=0, starts_with=''):
	    cat_list = []
	    if starts_with:
	        cat_list = Category.objects.filter(name__istartswith=starts_with)
	    
	    if max_results > 0:
	        if len(cat_list) > max_results:
	            cat_list = cat_list[:max_results]
	    return cat_list

### Create a Suggest Category View
Используя функцию `get_category_list()`, we can now create a view that returns the top eight matching results as follows:

{lang="python",linenos=off}
	def suggest_category(request):
	    cat_list = []
	    starts_with = ''
	    
	    if request.method == 'GET':
	        starts_with = request.GET['suggestion']
	    cat_list = get_category_list(8, starts_with)
	    
	    return render(request, 'rango/cats.html', {'cats': cat_list })

Заметьте, здесь мы повторно используем шаблон `rango/cats.html`.

### Mapping the View to URL
Добавьте следующий код к `urlpatterns` в `rango/urls.py`:

{lang="python",linenos=off}
	url(r'^suggest/$', views.suggest_category, name='suggest_category'),

### Updating the Base Template
В базовом шаблоне, в боковой колонке `<div>`, добавьте нижеследующую HTML разметку:

{lang="html",linenos=off}
	<ul class="nav nav-list flex-column">
	    <li class="nav-item">Type to find a category</li>
	    <form>
	    <li class="nav-item"><input class="search-query form-control" type="text"
	        name="suggestion" value="" id="suggestion" />
	    </li>
	    </form>
	</ul>
	<hr>
	<div id="cats">
	</div>

Here, we have added in an input box with `id="suggestion"` and div with `id="cats"` in which we will display the response. We don't need to add a button as we will be adding an event handler on keyup to the input box that will send the suggestion request.

Далее удалите следующие строки из шаблона:

{lang="html",linenos=off}
	{% block sidebar_block %}
	    {% get_category_list category %}
	{% endblock %}

### Add AJAX to Request Suggestions
Добавьте следующий код JQuery в `js/rango-ajax.js`:

{lang="javascript",linenos=off}
	$('#suggestion').keyup(function(){
	    var query;
	    query = $(this).val();
	    $.get('/rango/suggest/', {suggestion: query}, function(data){
	        $('#cats').html(data);
	    });
	});

Здесь, we attached an event handler to the HTML input element with `id="suggestion"` to trigger when a keyup event occurs. When it does, the contents of the input box is obtained and placed into the `query` variable. Then a AJAX `GET` request is made calling `/rango/category_suggest/` with the `query` as the parameter. On success, the HTML element with `id="cats"` (i.e. the `<div>`) is updated with the category list HTML.
	
{id="fig-exercises-suggestion"}
![An example of the inline category suggestions. Notice how the suggestions populate and change as the user types each individual character.](images/exercises-suggestion.png)
	


X> ###Упражнения
X> To let registered users quickly and easily add a Page to the Category put an "Add" button next to each search result.
X> - Update the `category.html` template:
X> 		- Add a small button next to each search result (if the user is authenticated), garnish the button with the title and URL data, so that the JQuery can pick it out.
X>		- Put a `<div>` with `id="page"` around the pages in the category so that it can be updated when pages are added.
X> - Remove that link to `add` button, if you like.
X> - Create a view `auto_add_page` that accepts a parameterised `GET` request ``(title, url, catid)`` and adds it to the category.
X> - Map an URL to the view `url(r'^add/$', views.auto_add_page, name='auto_add_page'),`
X> - Add an event handler to the add buttons using JQuery - when added hide the button. The response could also update the pages listed on the category page, too.

We have included the following code fragments to help you complete the exercises above. The HTML template code for `category.html` that inserts a button, and crucially keeps a record of the category that the button is associated with.

{lang="html",linenos=off}
	{% if user.is_authenticated %}
	    <button data-catid="{{category.id}}" data-title="{{ result.title }}"
	        data-url="{{ result.link }}" 
	            class="rango-add btn btn-info btn-sm" type="button">Add</button>
	{% endif %}

Код JQuery, который добавляет обработчик события `click` к каждой кнопке с классом` rango-add`:
 
{lang="javascript",linenos=off}
	$('.rango-add').click(function(){
	    var catid = $(this).attr("data-catid");
	    var url = $(this).attr("data-url");
	    var title = $(this).attr("data-title");
	    var me = $(this)
	    $.get('/rango/add/', 
	        {category_id: catid, url: url, title: title}, function(data){
	            $('#pages').html(data);
	            me.hide();
	        });
	    });  

The view code that handles the adding of a link to a category:

{lang="python",linenos=off}
	@login_required
	def auto_add_page(request):
	    cat_id = None
	    url = None
	    title = None
	    context_dict = {}
	    if request.method == 'GET':
	        cat_id = request.GET['category_id']
	        url = request.GET['url']
	        title = request.GET['title']
	        if cat_id:
	            category = Category.objects.get(id=int(cat_id))
	            p = Page.objects.get_or_create(category=category, 
	                title=title, url=url)
	            pages = Page.objects.filter(category=category).order_by('-views')
	            # Adds our results list to the template context under name pages.
	            context_dict['pages'] = pages
	    return render(request, 'rango/page_list.html', context_dict)

Разметка HTML шаблона для нового шаблона `page_list.html`:

{lang="html",lineos=off}
	{% if pages %}
	<ul>
	    {% for page in pages %}
	    <li><a href="{% url 'goto' %}?page_id={{page.id}}"\>{{ page.title }}</a></li>
	    {% endfor %}
	</ul>
	{% else %}
	    <strong>No pages currently in category.</strong>
	{% endif %}

Наконец, не забудте добавить in the URL mapping:  `url(r'^add/$', views.auto_add_page, name='auto_add_page'),`.

И если, как мы надеемся, у вас все получится, Rango будет выглядеть как на нижеследующих скриншотах. Но не останавливайтесь сейчас, переходите к следующим главам и узнайте как развернуть ваш проект на сервере!


{id="fig-exercises-main"}
![The main index page of the Rango application.](images/exercises-main.png)

{id="fig-exercises-results"}
![The category page with the Add Button feature.](images/exercises-results.png)


