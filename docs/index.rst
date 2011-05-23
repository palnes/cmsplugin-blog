
.. toctree::

##############
cmsplugin-blog
##############

cmsplugin-blog is really simple to set up on a working installation of django CMS.

************
Requirements
************

* `django CMS`_ 2.1.3 (or a higher release of 2.x).
* `django-staticfiles`_ 1.0.x (or higher)
* `django-tagging`_ 0.3.x
* `djangocms-utils`_ 0.9.x
* `simple-translation`_ 0.7.x
* `jQuery`_ 1.4.4
* `jQuery UI`_ 1.8.x

.. note :: jQuery can be provided either by locally or linking to a public server, like Google's or Microsoft's CDN.

.. _django CMS: https://www.django-cms.org/
.. _django-staticfiles: http://pypi.python.org/pypi/django-staticfiles/
.. _django-tagging: http://code.google.com/p/django-tagging/
.. _djangocms-utils: https://github.com/fivethreeo/djangocms-utils
.. _simple-translation: https://github.com/fivethreeo/simple-translation
.. _jQuery: http://jquery.com/
.. _jQuery UI: http://jqueryui.com/

Installation
============

Install ``cmsplugin-blog`` from pypi: ::

    pip install cmsplugin-blog

.. note :: When installing the cmsplugin-blog using pip, `django-staticfiles`_, `django-tagging`_, `djangocms-utils`_, and `simple-translation`_ will be installed automatically.

***********************
Configuration and setup
***********************

Settings
========
Add the following apps to your :setting:`django:INSTALLED_APPS` which enable cmsplugin-blog
and required or highly recommended applications/libraries)::

    INSTALLED_APPS = (
        ...
        'cmsplugin_blog', #
        'djangocms_utils', # utilities and extensions to django CMS
        'simple_translation', # enables multilingual features
        'tagging', # enables tagging of posts
        'staticfiles', # for serving static files
        ...
    )

Static content
--------------
Set the ``STATIC_ROOT`` and ``STATIC_URL`` settings for ``django-staticfiles``.::

    STATIC_ROOT = '/projectpath/static/'
    STATIC_URL = '/static/'


jQuery and jQuery UI
--------------------

Add the following settings to add jQuery UI ::

    JQUERY_JS = 'https://ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js'
    JQUERY_UI_JS = 'https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.12/jquery-ui.min.js'
    JQUERY_UI_CSS = 'http://ajax.googleapis.com/ajax/libs/jqueryui/1.8.12/themes/smoothness/jquery-ui.css'

Or download the sources and make them available locally::

    JQUERY_UI = '/path/to/jquery/'
    JQUERY_JS = '%sjs/jquery-1.4.4.min.js' % JQUERY_UI
    JQUERY_UI_JS = '%sjs/jquery-ui-1.8.9.custom.min.js' % JQUERY_UI
    JQUERY_UI_CSS = '%scss/smoothness/jquery-ui-1.8.9.custom.css' % JQUERY_UI

Multilingual blog
-----------------
If you are interested in multilingual blog, add ``cmsplugin_blog.middleware.MultilingualBlogEntriesMiddleware`` to :setting:`django:MIDDLEWARE_CLASSES` ::

    MIDDLEWARE_CLASSES = (
        ...
        'cmsplugin_blog.middleware.MultilingualBlogEntriesMiddleware',
    )

Blog entry placeholders
-----------------------
You can create multiple placeholders for each blog entry. This is useful for creating extra fields like excerpt, images, etc.::

    CMSPLUGIN_BLOG_PLACEHOLDERS = ('first', 'second', 'third')

Update the database
===================
Next, you need to update the database with the fields required by cmsplugin-blog::

    python manage.py syncdb

    # or if south is installed
    python manage.py syncdb --all
    python manage.py migrate --fake

*********
Templates
*********
In your ``template`` folder create a template adapted to your site as ``cmsplugin_blog/cmsplugin_blog_base.html``.

For example, if you have a template called ``base.html`` which has a block called ``body`` create a template that looks like this::

    {% extends "base.html" %}

    {% block body %}
        {% block left-col %}{% endblock %}
        {% block right-col %}{% endblock %}
    {% endblock %}

.. note:: The cmsplugin-blog uses the block names ``left-col`` and ``right-col`` by default.

*****************
Creating the blog
*****************
To create a blog you need to create a page which will contain the root of the blog. From this page the entire
blog is shown.

Create a page in the CMS. Under ``Advanced settings`` ``Application``, select ``Blog Apphook``.

Do this for each language you want to show posts in. A restart of the server afterwards is mandatory due to caching.

That should be it! Now you can spend countless hours and nights thinking about what you were supposed to write about
that wasn't kittens or other cute furry animals.

