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

=================================================
after deploy, the following errors happen , missing django.utils.six, 
CANNOT FIX IT. 

2021-02-14T16:08:33.383637+00:00 app[web.1]: ModuleNotFoundError: No module named 'django.utils.six'
2021-02-14T16:08:33.384056+00:00 app[web.1]: [2021-02-14 16:08:33 +0000] [10] [INFO] Worker exiting (pid: 10)
2021-02-14T16:08:33.477243+00:00 app[web.1]: Traceback (most recent call last):
2021-02-14T16:08:33.477256+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 209, in run
2021-02-14T16:08:33.477559+00:00 app[web.1]: self.sleep()
2021-02-14T16:08:33.477591+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 357, in sleep
2021-02-14T16:08:33.477830+00:00 app[web.1]: ready = select.select([self.PIPE[0]], [], [], 1.0)
2021-02-14T16:08:33.477831+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 242, in handle_chld
2021-02-14T16:08:33.478214+00:00 app[web.1]: self.reap_workers()
2021-02-14T16:08:33.478218+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 525, in reap_workers
2021-02-14T16:08:33.478481+00:00 app[web.1]: raise HaltServer(reason, self.WORKER_BOOT_ERROR)
2021-02-14T16:08:33.478525+00:00 app[web.1]: gunicorn.errors.HaltServer: <HaltServer 'Worker failed to boot.' 3>
2021-02-14T16:08:33.478526+00:00 app[web.1]:
2021-02-14T16:08:33.478526+00:00 app[web.1]: During handling of the above exception, another exception occurred:
2021-02-14T16:08:33.478527+00:00 app[web.1]:
2021-02-14T16:08:33.478527+00:00 app[web.1]: Traceback (most recent call last):
2021-02-14T16:08:33.478530+00:00 app[web.1]: File "/app/.heroku/python/bin/gunicorn", line 8, in <module>
2021-02-14T16:08:33.478656+00:00 app[web.1]: sys.exit(run())
2021-02-14T16:08:33.478656+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/app/wsgiapp.py", line 58, in run
2021-02-14T16:08:33.478792+00:00 app[web.1]: WSGIApplication("%(prog)s [OPTIONS] [APP_MODULE]").run()
2021-02-14T16:08:33.478792+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/app/base.py", line 228, in run
2021-02-14T16:08:33.478971+00:00 app[web.1]: super().run()
2021-02-14T16:08:33.478972+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/app/base.py", line 72, in run
2021-02-14T16:08:33.479103+00:00 app[web.1]: Arbiter(self).run()
2021-02-14T16:08:33.479103+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 229, in run
2021-02-14T16:08:33.479277+00:00 app[web.1]: self.halt(reason=inst.reason, exit_status=inst.exit_status)
2021-02-14T16:08:33.479278+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 342, in halt
2021-02-14T16:08:33.479481+00:00 app[web.1]: self.stop()
2021-02-14T16:08:33.479482+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 393, in stop
2021-02-14T16:08:33.479709+00:00 app[web.1]: time.sleep(0.1)
2021-02-14T16:08:33.479710+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 242, in handle_chld
2021-02-14T16:08:33.479871+00:00 app[web.1]: self.reap_workers()
2021-02-14T16:08:33.479871+00:00 app[web.1]: File "/app/.heroku/python/lib/python3.6/site-packages/gunicorn/arbiter.py", line 525, in reap_workers
2021-02-14T16:08:33.480143+00:00 app[web.1]: raise HaltServer(reason, self.WORKER_BOOT_ERROR)
2021-02-14T16:08:33.480144+00:00 app[web.1]: gunicorn.errors.HaltServer: <HaltServer 'Worker failed to boot.' 3>
2021-02-14T16:08:33.552447+00:00 heroku[web.1]: Process exited with status 1
2021-02-14T16:08:33.635968+00:00 heroku[web.1]: State changed from up to crashed


