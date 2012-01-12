Disclaimers
###########

.. image:: /_static/warning.jpg
   :scale: 40%

.. raw:: pdf

    PageBreak


Ligne de commande
-----------------

.. image:: /_static/cli_fear.jpg


.. raw:: pdf

    PageBreak

Veille technologique
--------------------

.. image:: /_static/forever_alone.jpg

.. raw:: pdf

    PageBreak

Documentation
-------------

.. image:: /_static/rtfm.jpg
   :scale: 180%

.. raw:: pdf

    PageBreak


Typage Statique
---------------

.. image:: /_static/BurnTheWhitch.jpg
   :scale: 130%

.. raw:: pdf

    PageBreak

Django: le logo
---------------

.. image:: /_static/django-pony.jpg
   :scale: 65%



.. raw:: pdf

    PageBreak

Références
----------

+ Google

+ Bitbucket

+ WashingtonPost

+ curse.com (connu des gamers, > 14 millons visiteurs uniques/mois)

+ Gymglish

.. raw:: pdf

    PageBreak

L'architechture logicielle
##########################

.. image:: /_static/mtv.jpg

.. raw:: pdf

    PageBreak

Signification
-------------

+------------+----------+------------+
|  *MVC*     | *Django* | Couches    |
+============+==========+============+
| Model      | Model    | Donnée     |
+------------+----------+------------+
| View       | Template | HTML       |
+------------+----------+------------+
| Controler  | View     | Calculs    |
+------------+----------+------------+

.. raw:: pdf

    PageBreak

Parcour de la requête
---------------------

.. digraph:: G

    graph [fontsize=10];
    edge  [fontsize=9];
    node  [fontsize=9];
    rankdir="LR"
    ranksep = 0.2;
    nodesep = .2;
    size = "3.5,5.5"
    edge [style="setlinewidth(1)"];
    node [style="setlinewidth(1)"];
    subgraph cluster_server{
        label="site django";
        Core [shape=doublecircle];
        Modèle [shape=folder];
        Template [shape=note];
        Core -> URL_conf [label=URL];
        URL_conf -> Core [label=Vue];
        Core -> Vue [label=request];
        Vue -> Modèle [dir=both];
        Vue -> Template [dir=both];
        Vue -> Core [label=responce];
    }
    Client -> Core  [label=HTTP, dir=both];

.. raw:: pdf

    PageBreak

RAPPEL PYTHON
#############


.. image:: /_static/octocat_py.jpg
   :scale: 150%


.. raw:: pdf

   PageBreak

Gestion du projet
#################

Keep It Stupid Simple

::

    django-admin.py startproject <project_name>

.. raw:: pdf

    PageBreak

Base
----

::

    - projet
      |# __init__.py
      |# manage.py
      |# settings.py
      |# local_settings.py // optionnel
      |# urls.py
      |- template
      | \
      |  |# base.html
      |  |+ sub_app

.. raw:: pdf

    PageBreak

Modules
-------

::

    - project
      |- sub_app
      | \
      |  |# __init__.py
      |  |# admin.py  // optionnel
      |  |# models.py
      |  |# tests.py  // optionnel
      |  |# urls.py
      |  |# forms.py  // optionnel
      |  |# views.py
      |  |- static
      |  |- template
      |  | \
      |  |  |+ sub_app

.. raw:: pdf

    PageBreak

Media
-----

::

    - project
      |+ media
      |- static_root
      |- static_common
      | \
      |  |+ javascript
      |  |+ css
      |  |+ images

::

    ./manage.py collectstatic

.. raw:: pdf

    PageBreak

Demo initialisation
-------------------

.

.. image:: /_static/bonaldi.jpg
    :scale: 65%

::

    django-admin.py startproject <project_name>

.. raw:: pdf

    PageBreak


Configuration
-------------

.. image:: /_static/settings.jpg

.. raw:: pdf

    PageBreak

settings.py
-----------

::

    DEBUG
    DATABASES
    {MEDIA/STATIC}_ROOT
    {MEDIA/STATIC}_URL
    INSTALLED_APPS
    ROOT_URLCONF
    SECRET_KEY
    MIDDLEWARE_CLASSES
    TEMPLATE_CONTEXT_PROCESSORS
    TEMPLATE_DIRS
    LOGGING

.. raw:: pdf

    PageBreak

urls.py
-------

::

    from django.conf.urls.defaults import patterns, include, url
    from django.conf import settings

    urlpatterns = patterns('',
        url(r'^my_module$', include('my_module.urls')),)

    if settings.DEBUG:
        urlpatterns += patterns('',
            url(r'^media/(?P<path>.*)$', 'django.views.static.serve', { #*
                'document_root': settings.MEDIA_ROOT,})
        from django.contrib.staticfiles.urls import staticfiles_urlpatterns
        urlpatterns += staticfiles_urlpatterns()

.. raw:: pdf

    PageBreak

manage.py
---------

::

    ./manage.py startapp <app_name>  # Nouveau dossier d'application
    ./manage.py runserver  # lance server de dev
    ./manage.py shell  # shell python local
    ./manage.py syncdb  # génère la DB à partir des classes
    ./manage.py inspectdb  # génère des classes à partir de la DB
    ./manage.py dbshell  # shell SQL
    ./manage.py help

.. raw:: pdf

    PageBreak


les Modèles
###########

.

.. image:: /_static/django-model.jpg

.. raw:: pdf

    PageBreak

Les Backends
------------

::

    - PostgreSQL

    - SQLite

    - MySQL

    - Oracle

.. note::

    Tant que les regex et le SQL brut ne sont pas utilisés, les backends sont
    interchangeables

.. raw:: pdf

    PageBreak

La philosophie
--------------

  - ``django.conf.settings.DATABASES -> databases``
  - ``django.db.models.Model -> DB Table``
  - ``django.db.models.Field -> Column``
  - ``django.db.models.Manager -> QuerySet``

.. raw:: pdf

    PageBreak

Les fields
----------

  - BooleanField

  - CharField

  - DateTimeField

  - FileField

  - IntegerField

  - ForeignKey

  - OneToOneField

  - ManyToManyField

`Documentation <https://docs.djangoproject.com/en/dev/ref/models/fields/#field-types>`_

.. raw:: pdf

    PageBreak

Les fields: paramètres
----------------------

  - verbose_name
  - default
  - null/blank
  - help_text
  - choices
  - validators
  - db_column

.. raw:: pdf

    PageBreak

Les métadatas
-------------

  - db_table
  - permissions
  - verbose_name
  - app_label
  - ordering
  - abstract
  - proxy

.. raw:: pdf

    PageBreak

Example
-------

::

    from django.db import models

    class Item(models.Model):
        """
        >>> Item.object.create(value=2, name="first")
        >>> Item.object.create(value=1, name="second")
        >>> print unicode(Item.object.get(name="first"))
        first(2)
        """
        name = models.CharField(unique=True, blank=False)
        value = models.IntegerField()

        def __unicode__(self):
            return u"%s(%s)" % (self.name, self.value)


.. raw:: pdf

    PageBreak

Démo
----
.

.. image:: /_static/bonaldi.jpg
    :scale: 65%

::

    ./manage.py shell

.. raw:: pdf

    PageBreak

Vue
###

.. image:: /_static/views.jpg
   :scale: 50%

.. raw:: pdf

    PageBreak

Les fonctions views
-------------------

::

    from django.shortcuts import render
    from django.contrib.auth.decorators import login_required

    import models as local_models

    def my_view(request, max):
        items = local_models.Item.objects.filter(value__lte=max)
        return render(request, "/local_app/my_template.html",
                      {'item': item})

.. raw:: pdf

    PageBreak

L'objet request
---------------

::

    request.POST
    request.GET
    request.COOKIES
    request.META
    request.session
    request.user

.. raw:: pdf

    PageBreak


Template
#########

.. image:: /_static/pony_template.jpg
   :scale: 30%

.. raw:: pdf

    PageBreak

L'héritage
----------

::

    <!DOCTYPE html>
    <html lang="fr">
    <head>
    <meta charset="utf-8">
    <title>titre du site</title>
    {% block extra_head %}{% endblock %}
    </head>
    <body>
    {% block content %} <p>Rien</p> {% endblock %}
    </body>
    </html>

.. raw:: pdf

    PageBreak

L'héritage
----------

::

    {% extends 'base.html' %}
    {% block content %}
    {% endblock %}

.. raw:: pdf

    PageBreak

Les templates tags
------------------
::

   {% if %} {# bientôt {% elif %} #} {% else %} {% endif %}
   {% comment %} {% endcomment %}
   {% load 'template_lib' %}
   {% for item in list %} {{ item }} {% endfor %}
   {% with val=qs.count %} {{ val }} {% endwith %}
   {% url view_name arg1 arg2 %}
   {% include 'template' %}

.. raw:: pdf

    PageBreak

Les filters
-----------

::

   {{ model.html_field safe }}

.. raw:: pdf

    PageBreak

Example
-------

.. raw:: pdf

    PageBreak

Les limitations
---------------

Pas de python

Pas de calculs

Pas de méthodes à arguments

Pas d'attribution

.. raw:: pdf

    PageBreak


Bibliothèques externes
######################

Does this need to be in the core?

.. raw:: pdf

    PageBreak


Contribs
--------

 + admin

 + auth

 + gis

.. raw:: pdf

    PageBreak

External
--------

 + olwidget

 + south

 + django_uni_form

 + django_extensions

.. raw:: pdf

    PageBreak

Demo
----

.. raw:: pdf

    PageBreak

Django 1.3 WordPress
--------------------

.

.. image:: /_static/ie_trollface.jpg
   :scale: 30%

.. raw:: pdf

    PageBreak


Poneys
######

Django is made of magic ponies

.. image:: /_static/awesome_rainbow_pony.jpg


.. |pdf_lb| raw:: pdf

    PageBreak
