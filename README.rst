django-dbtemplates
==================

What's new in this fork?
This fork addresses what I felt was a caching issue. My perspective of this project was that
I wanted people to be able to override a template in my project, and fall back to the file system
if the name of the template didn't match.

Previously, if you created a template for say, "index.html" and then changed the name to "foo.html",
index.html would not be removed from the cache. By adding a pre_save to the Template model and a
minor edit to the remove_cached_template function, if you change the name of a template, the previously
cached value will be deleted, and the new template name will be added to the cache.

This fork requires that you specify the database template loader first, instead of last:

TEMPLATE_LOADERS = (
    'dbtemplates.loader.Loader',
    'django.template.loaders.filesystem.Loader',
    'django.template.loaders.app_directories.Loader',
)


``dbtemplates`` is a Django app that consists of two parts:

1. It allows you to store Django templates in your database instead of the file system.
2. It provides `template loader`_ that enables Django to load the templates from the database,
    which can override an existing template in the file system.

It also features optional support for versioned storage and django-admin
command, integrates with Django's caching system and the admin actions.

Please see http://django-dbtemplates.readthedocs.org/ for more details.

The source code and issue tracker can be found on Github:

https://github.com/btaylordesign/django-dbtemplates

Many thanks to Jannis Leidel for starting this great app!
https://github.com/jezdez

.. _template loader: http://docs.djangoproject.com/en/dev/ref/templates/api/#loader-types