Django MTV, django pour les dévelopeurs
########################################

.. warning::

     + Veille technologique

     + Peu d'assistance comparé aux langage à typage statique.

     + Documentation en ligne

.. raw:: pdf

    PageBreak

L'architechture logicielle
##########################

+------------+----------+---------------------+
|  *MVC*     | *Django* |  `*N-tiers*`        |
+============+==========+=====================+
| Model      | Model    | DAL (+- Business)   |
+------------+----------+---------------------+
| View       | Template | Presentation GUI    |
+------------+----------+---------------------+
| Controler  | View     | Presentation Logic  |
+------------+----------+---------------------+

.. raw:: pdf

    PageBreak

Parcour de la requête
#####################

.. digraph:: G
    :scale:50%

    graph [fontsize=11];
    edge  [fontsize=10];
    node  [fontsize=10];
    ranksep = 0.3;
    nodesep = .05;
    size = "2.0,3.5"
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

Configuration
-------------

.. image:: /_static/BurnTheWhitch.jpg

.. raw:: pdf

    PageBreak

Gestion du projet
#################

Keep It Stupid Simple

.. raw:: pdf

    PageBreak

Gestion du projet
#################

::

    django-admin.py startproject <project_name>

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
      |  |  |# base.html // optionnel
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

les Modèles
###########

.. raw:: pdf

    PageBreak

Les Backends
------------

  - Backends officiels:
    - PostgreSQL
    - SQLite
    - MySQL
    - Oracle
  - Backends tiers:
    - ODBC
    - IBM DB2
    - Firebird
    - SQL Server
    - Sybase

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

Example
-------

.. raw:: pdf

    PageBreak

Les fields
----------

  - BooleanField
  - CharField
  - DateTimeField
  - FileField
  - IntegerField
  - EmailField
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

.. raw:: pdf

    PageBreak

Démo
----

::

    ./manage.py shell

.. raw:: pdf

    PageBreak

Vue
###

.. raw:: pdf

    PageBreak

Les fonctions views
-------------------

.. raw:: pdf

    PageBreak

L'objet request
---------------

.. raw:: pdf

    PageBreak


Template
#########

.. raw:: pdf

    PageBreak

L'héritage
----------

.. raw:: pdf

    PageBreak

Les limitations
---------------

.. raw:: pdf

    PageBreak

Les templates tags
------------------

.. raw:: pdf

    PageBreak

Les filters
-----------

.. raw:: pdf

    PageBreak

Example
-------

.. raw:: pdf

    PageBreak


Formulaires
###########

ModelForm.
----------

.. raw:: pdf

    PageBreak

Formulaires.
------------

.. raw:: pdf

    PageBreak

Validation et autre.
--------------------

.. raw:: pdf

    PageBreak

Bibliothèques externes
######################

Does this need to be in the core?

.. raw:: pdf

    PageBreak

Poneys
######

Django is made of magic ponies

.. image:: /_static/awesome_rainbow_pony.png

