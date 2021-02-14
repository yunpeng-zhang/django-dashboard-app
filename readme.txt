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

2. create Procfile
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


