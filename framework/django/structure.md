Structure
=========

建立專案

    django-admin startproject mysite


裡面會長這樣

    mysite/
    ├── manage.py
    └── mysite
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py

`manage.py` 提供很多指令可以用，很像 Laravel 的 `artisan`

    python manage.py help

Hello world 最基本的就是執行 `runserver`

    python manage.py runserver

預設 port 8000
