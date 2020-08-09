# Django_project
(HOW TO CREATE A PERSONALBLOG USING DJANGO)
CREATING A VIRTUAL ENVIRONMENT:
----------------------------------------------------------
To create a personal blog you have to create a virtualenvironment
To create a virtual environment you have to install pip3

--->pip3 install virtualenv

this command install virtual evnvironment of latest version
---------------------------------------------------------
after installing VE select any destination where you want your VE and

>cd desktop
C:users\RDX\Desktop>virtualenv myvenv

this command creates VE in your desktop in the name of myvenv
--------------------------------------------------------- 
After this you have to activate your VE 

>myvenv\Scripts\activate

this activates your VE.....
--------------------------------------------------------------
to deactivate this VE

>myvenv\Scripts\deactivate
----------------------------------------------------------
to start a project in your virtual env

>django-admin startproject myportfolio
------------------------------------------------------------
>cd myportfolio
>py manage.py runserver

if the above command doesn't work this means you dont have django installed in your VE therefore 
you have to install django
>pip install django==3.1

after this check the django framework is set up by using the server url :127.0.0.1:8000
----------------------------------------------------------------------------
.gitignore.io file :
`````````````````````
->this file contains the files which are to be ignored by git 
->this means if there is a file which contains secret information this information is protected 
by this gitignore by not uploading the files inside it.

so how to create this gitignore file using cmd

(myvenv)C:users\RDX\Desktop\myportfolio\myportfolio>notepad .gitignore.io

this creates a .gitignore file of format-io
after this search in the browser-> .gitignore.io django->copy paste the contents in the file shown 
in the browser. 

example :.gitignore.io django file 

# Created by https://www.toptal.com/developers/gitignore/api/django
# Edit at https://www.toptal.com/developers/gitignore?templates=django

### Django ###
*.log
*.pot
*.pyc
__pycache__/
local_settings.py
db.sqlite3
db.sqlite3-journal
/media          #add
/static		#add

save this file
---------------------------------------------------------------------------------------------------
HOW TO ADD FILES TO THE GIT USING CMD:
first we have to initialize the git (if git is not installed install git )

>cd..
(myvennv)c:users\RDX\Desktop\myportfolio>git init

(myvennv)c:users\RDX\Desktop\myportfolio>git status  
this command shows which files are not send to git in order to add files to my repository

(myvennv)c:users\RDX\Desktop\myportfolio>git add -A
this command adds all file to the git after this step save the files using commit

(myvennv)c:users\RDX\Desktop\myportfolio>git commit -m "This is my first commit"
"" inside colon is the comment for the project
----------------------------------------------------------------------------------------------------
APP CREATION IN DJANGO 
TO create the project portfolio two apps are created which are complete different webpages which 
can also be used in other projects the two app names are blog and jobs

(myvennv)c:users\RDX\Desktop\myportfolio>py manage.py startapp blog
(myvennv)c:users\RDX\Desktop\myportfolio>py manage.py startapp jobs

this command creates two apps under the project myportfolio
after this save the apps to git 
(myvennv)c:users\RDX\Desktop\myportfolio>git add -A
(myvennv)c:users\RDX\Desktop\myportfolio>git commit -m "apps are saved"
---------------------------------------------------------------------------------------------------
MODELS:
Models are like information about your app. It contains the essential fields and behaviors 
of the data you’re storing. Generally, each model maps to a single database table.

The basics:

Each model is a Python class that subclasses django.db.models.Model.
Each attribute of the model represents a database field.
With all of this, Django gives you an automatically-generated database-access API; see Making queries.

refer Django docs for more information
-----------------------------------------------------------------------------------------------------
jobs\model.py
```````````````
from django.db import models

# Create your models here.
class Job(models.Model):
    image = models.ImageField(upload_to='images/')
    summary = models.CharField(max_length=200)
    
this model.py file create a class and add the fields you are going to include in your app 
the above class contains image field to fit the photo and character field to say some lines about me
in the app.
------------------------------------------------------------------------------------------------------
after this -> in project portfolio settings.py include the app you have created and add media variable 

myportfolio\settings.py:(changes to be done in settings.py)
````````````````````````
# Application definition

INSTALLED_APPS = [
    'jobs.apps.JobsConfig',      # refer apps.py and copy the class name after jobs.apps.(Classname)
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
scroll to last and add

MEDIA_ROOT = BASE_DIR / 'media'

MEDIA_URL = '/media/'
-----------------------------------------------------------------------------------------------------
after this make migrations in order to save your django projects untill you have done

C:.. /myportfolio>py manage.py migrate

after you made any changes after migrate use this command to migrate

C:.. /myportfolio>py manage.py makemigration

Note:
* in order for the imageField to work pillow is asked to install use pip to install pillow
pip install pillow
after installing pillow make migration again to save the changes
------------------------------------------------------------------------------------------------------
In order to view databases admin login has to be created so to create admin

C:.. /myportfolio>py manage.py createsuperuser

this command ask user name and the password which we have to give
Username:nivi
password:Exotion@05 (Ecaps)
my admin login is created
----------------------------------------------------------------------------------------------------
Admin.py in Jobs app:
````````````````````````
admin.py is file is used when we want to show something in admin page for that we have created login
in order to do that open admin.py and make these changes:

from django.contrib import admin
from .models import Job
# Register your models here.
admin.site.register(Job)

after this save your file refresh the server and see the changes a job is created in the admin login
if we click the job the image and character field is shown and we can insert a image and 
some lines describing the image.
save that and tada the object is created...we can also edit and save that object

**remember the one you want to show in the admin page are to be included in admin.py**
-------------------------------------------------------------------------------------------------------
after the creation of object in the admin page the image cannot be views due to the url is not 
liked to the project in order to do that 
open urls.py in myportfolio and make the changes

from django.contrib import admin
from django.urls import path
from django.conf import settings #change1
from django.conf.urls.static import static # change2

urlpatterns = [
    path('admin/', admin.site.urls),
]+ static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT) #change3

this static fun link the url of image to the variable declared in settings.py
Now the image can be viewed in the admin page.
------------------------------------------------------------------------------------------------------
install postgred sql in your system for db:
```````````````````````````````````````````
https://www.youtube.com/watch?v=e1MwsT5FJRQ->installation procedure

To access postgred sql in cmd:
`````````````````````````````
copy paste the  following path in your system environmental variables:PATH under system variable 
add the two path with the existing path.
1.C:\Program Files\PostgreSQL\12\bin
2.C:\Program Files\PostgreSQL\12\lib

open cmd
1-> psql -U postgres postgres  # the second postgres is the database name
2-> enter the username and password... username is postgres by default in all systems
3-> password saved when installing postgres.
db is logged in tadaaa then do your sql command..
commom commands:
\dt ->displays if there is any relation
\du ->displays the number of users (now just 1)
-------------------------------------------------------------------------------------------------------
after the postgresql installation create a new database -> CREATE DATABASE portfoliodb;
open settings.py and change the database:

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'portfoliodb',
        'USER':'postgres',
        'PASSWORD':'********',
        'HOST':'localhost',
        'PORT':'5432',
    }
}
save the file and then make migrations ->py manage.py runserver.

error will be shown which ask you to install a package for db connection 
pip install psycopg2-binary
install psycopg then run

now if we run the server the it will show error due to the change of database if db is changed new 
admin user have to be created therefore
>py manage.py createsuperuser
username :nivi
password:********

now re run server and open admin page the job model will be shown but the object is deleted due to the 
db change. but the image path created will exist and it will not be stored in new db  but  it can be 
viwed...
----------------------------------------------------------------------------------------------------------
CREATING MODEL FOR bLOG :
``````````````````````````
The blog requires title,date,body,image they can be created using model class as 
blog/models.py:
``````````````
from django.db import models #create class named Blog and specify the fields needed.

class Blog(models.Model):
    title = models.CharField(max_length=255)
    pub_date = models.DateTimeField()
    body = models.TextField()
    image = models.ImageField(upload_to = 'images/')

After this add the app to myportfolio/settings.py

INSTALLED_APPS = [
    'blog.apps.BlogConfig', #refer the apps.py in blog app and mention the class name
    'jobs.apps.JobsConfig',
......]

Finally to add this app to admin page-> blog/Admin.py

from django.contrib import admin
from .models import Blog

admin.site.register(Blog)

register the model in admin 

save all files and makemigrations and migrate
>py manage.py makemigrations
>py manage.py migrate

now run the server-> py manage.py runserver

go to the admin page and save the object like we did for job apps

Finally Blog model is created...
---------------------------------------------------------------------------------------------------------
upto now we have only created the apps and their models  their webpages haven't created..
CREATE WEBPAGE FOR JOBS:

```````````````````````
create a new folder templates under jobs app 
>cd jobs
>mkdir templates
>cd template
>mkdir jobs
>notepad home.html

now a empty html page is created inside jobs/template/jobs/home.html
in order for the webpage to run create a view in jobs/views.py

from django.shortcuts import render

def home(request):
    return render(request,'jobs/home.html')

Add the view to the project myportfolio/urls.py

from django.contrib import admin
from django.urls import path
from django.conf import settings
from django.conf.urls.static import static
import jobs.views # importing views.py file from app in order to view the webpage in server.

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',jobs.views.home,name = 'home' ),# if there is no string after localhost then home.html is viewed 
]+ static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)

save and run web page can be viewed ....
---------------------------------------------------------------------------------------------------------
BOOTSTRAP:
````````````
Bootstrap is very useful for web developers to make the website easily using bootstrap tools 

www.getbootstrap.com-> refer the docs for more info.

in the above website->examples->albums->rightclick->view page source->copy paste the code in home.html

in the webset go to home page->scroll to bootstrap CDN copy past the css and Javascript code and past in the home.html

you can change the webpage to your requirements. the changes made in home.html are 
->nav bar is added (docs->search navbar copy paste the code in header)
->Footer the copyright and year is added. The year is upto date with the use of python
in footer->&copy Nivetha {% now "Y" %} the code within curlybraces give the current year (its cool right!)
->change the intro section - change the button to email me and add mailto:nivinataliya@gmail.com to href 
->del all the photocards except one photocard del rem 8
-> make a for loop :

{% for job in jobs.all %}
      # jobs.all refers to the objects created in the admin login   
<div class="col-md-4">
          
<div class="card mb-4 shadow-sm">
            
<img class="card-img-top" src="{{job.image.url}}"/>
 # image is the property created in the model.py         
 <div class="card-body">
             			# url is the link of the image
 <p class="card-text">{{job.summary }}</p>
 # summary refers to the property in model.py            
</div>
            
</div>
          
</div>
        
</div>
        
{% endfor %}

by this loop the photocard is displayed in times of the object created in the admin

->you can change the class right or left ,dark or light etc only you have to know the correct term 
for that learn bootstrap.
 
save and run the server and tata the job app's home page is displayed.
-------------------------------------------------------------------------------------------------------
CREATING BLOG :
````````````````
Create a new folder template/blog/allblogs.html
copy paste the code like we done in home.html and make the changes
<main role="main">  
    <div class="container">
      <h1 class="text-centre pt-3">Welcome to my Blog</h1>
	  <br/>
	  <br/>
	  <h2 class="text-left"> Latest Post</h2>
	  <hr/>
	  {% for blog in blogs.all %}
		<a href="http://localhost:8000/"><h3>{{blog.title}}</h3></a>
		{{blog.pub_date_pretty}}
		<br/>
		<img  class="img-fluid" src="{{blog.image.url}}" height=200 width=400/>
		<br/>
		<p>{{blog.summary}}</p>	
        
      {% endfor %}
   </div>
 </main>

we can change the date format by creating a fun in model.py
  def pub_date_pretty(self):
        return self.pub_date.strftime('%b %e %y') 

refer the fun insted of pub_date in html

we limit the description for the blog by creating a fun in model.py
def summary(self):
        return self.body[:100] 

refer the fun insted of body property in html

create a new fun in view.py for blog title link

def detail(request,blog_id):
    detailblog = get_object_or_404(Blog,pk=blog_id)#pk refers to the primary key in the database
    return render(request,'blog/detail.html',{'blog':detailblog})

add this path to urls.py

path('<int:blog_id>/',views.detail,name='detail')# this blog_id is the variable to primary key in integer
-------------------------------------------------------------------------------------------------------
STATIC FILES:
The files that require for web developement is called static files images,css,js,fonts etc are static files

create a new folder static under myportfolio/myportfolio/static->save image,resume

in settings .py add STATIC_ROOT and STATICFILES_DIR
STATICFILES_DIRS=[BASE_DIR / 'myportfolio/static']
STATIC_ROOT = BASE_DIR / 'static' 

in cmd ->py manage.py collectstatic->new static folder is created at the project myportfolio
where the image and resume pdf are stored.

in html files at the top-> {% load static %} this loads all the static files
add the link for resume as->{% static 'resume.pdf' %}
the image link can also be given as->{% static 'photo.jpg' %}

-----------------------------------------------------------------------------------------------------------
FINAL TOUCHUP :
to make the website more responsive complete the links which are unrefered
->copy paste the allblogs.html and make the changes inside main

<main role="main">  
    <div class="container">
	<h3 class="text-center">{{blog.title}}</h3>
	<br/>
	<br/>
	<p class="text-center">{{blog.pub_date_pretty}}</p>
	<img  class="img-fluid" src="{{blog.image.url}}" />
	<br/>
	<br/>
	<p>{{blog.body}}</p>	
    </div>
</main>

->give the linkedin link 
->for  blog  in nav bar->href-> {% url 'allblogs' %} in all html pages
-> for nivetha in nav bar->href->{% url 'home' %} in all html pages
->change the title to {{blog.title}}

->allblogs.html-><a href="{% url 'detail' blog.id %}"><h3>{{blog.title}}</h3></a> 
the above link in href takes you to the respective blog posts(detail/1,detail/2)etc
save the above and run ->tadaaaa project is completed.
----------------------------------------------------------------------------------------------------------


    









