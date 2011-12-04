========================================
Django MTV, django pour les dévelopeurs
========================================
.. warning::

    La Documentation en ligne et la veille technologique : un point
    central du workflow!

.. raw:: pdf

    PageBreak

L'architechture logicielle
##########################

+------------+----------+
|  *MVC*     | *Django* |
+============+==========+
| Model      | Model    |
+------------+----------+
| View       | Template |
+------------+----------+
| Controler  | View     |
+------------+----------+

.. raw:: pdf

    PageBreak

Fichiers du projet
##################

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

    ./manage.py syncdb
    ./manage.py runserver
    ./manage.py startapp <app_name>
    ./manage.py inspectdb
    ./manage.py shell
    ./manage.py dbshell
    ./manage.py help

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

..note::

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

TP
---

.. raw:: pdf

    PageBreak

Correction
----------

.. raw:: pdf

    PageBreak
