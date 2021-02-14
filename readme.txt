to run his project local

https://www.freecodecamp.org/news/how-to-create-an-analytics-dashboard-in-django-app/

0. python manage.py migrate dashboard
1. python manage.py runserver
2. open it in explorer
http://127.0.0.1:8000/dashboard/

Deploy django to heroku
https://www.analyticsvidhya.com/blog/2020/10/step-by-step-guide-for-deploying-a-django-application-using-heroku-for-free/
1. pip install gunicorn
pip install django-heroku
2. create Procfile, make sure the *.wsgi to match with project folder name, here "analytics_project.wsgi"
3. add gunicorn and django-heroku to requirements.txt
pip freeze > requirements.txt
4. update settings.py with the following
import django_heroku
# Activate Django-Heroku.
django_heroku.settings(locals())
5. moving onto production
setting.py
update DEBUG=FALSE
6. install heruko client
https://medium.com/analytics-vidhya/how-to-install-heroku-cli-in-windows-pc-e3cf9750b4ae
7. follow step 11-14
8. follow stpe 15-22
if need to update the files, after changing the files. rerun the following
git add .
git commit -m “edit”
git push heroku master


https://medium.com/@vdboor/patching-a-missing-django-utils-six-f882f93ccbce
import sys
import warningsimport django.utils
import django.utils.encoding
import django.shortcutsclass Six:
    string_types = str,
    text_type = str
    next = nextdef _compact(cls):
    warnings.warn(f"Remove python_2_unicode_compatible() for {cls}")
    return clsdjango.utils.six = Six
django.utils.encoding.python_2_unicode_compatible = _compact
django.shortcuts.render_to_response = django.shortcuts.render
sys.modules['django.utils.six'] = Six


