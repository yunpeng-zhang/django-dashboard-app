to run his project local

https://www.freecodecamp.org/news/how-to-create-an-analytics-dashboard-in-django-app/

0. python manage.py migrate dashboard
1. python manage.py runserver
2. open it in explorer
http://127.0.0.1:8000/dashboard/

for local to work, it has disable the step 4 below in settings.py of the project. 

Deploy django to heroku - use pipreqs to generate requirements.txt for the project

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
9. migrate the data, SQLite3 is not supported by heroku, and need to migrate data to PostgreSQL, 
https://stackoverflow.com/questions/58908100/how-to-sync-local-django-sqlite3-data-with-herokus-postgres-database 
python manage.py dumpdata > data.json
git push heroku master
heroku run python manage.py migrate
heroku run python3 manage.py loaddata data.json
heroku open
https://demo-django-dashboard-dz.herokuapp.com/dashboard/
10. to see the logs of errors in deployment
heroku logs --tail
11. the link should be 
https://demo-django-dashboard-dz.herokuapp.com/dashboard/

it shows the framework WITHOUT the data though.        