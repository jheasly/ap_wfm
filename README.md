ap_wfm
======

AP WebFeeds Manager parser

[Install requirements](#install-requirements)

Install requirements
--------------------

1. An [AP Exchange](http://www.apexchange.com/) Saved Search news feed. At least one, but several can work at the same time. We've got ~16 going at a time.
1. An [AP WebFeeds Manager](http://wfm.ap.org/) installation pointed at the AP Exchange news feed
1. A working [Django](https://www.djangoproject.com/) installation
1. A cron job that inserts the AP stories resulting from the AP Exchange -> WebFeeds Manager XML into a Django database.


Then install the project requirements:

```
pip install -r requirements.txt
```

To restart
----------

If running a manual restart from `oper` account home directory on command line:
```bash
$ nohup java -jar [your_django_project]/ap_wfm/WebFeedsAgent.jar commandLine > /dev/null 2>&1 &
```
or try this if the above dies when you log out:  
```bash
$ java -jar [your_django_project]/ap_wfm/WebFeedsAgent.jar commandLine > /dev/null 2>&1 &
```

(Remember, this is only to restart. First time runinng, you must supply `userName`, `password` and `agentName`.)

To see if it's running (on Linux):
```bash
$ ps -ef | grep java
```

To run locally
--------------

The key to getting it to run locally from within a virtual environment (so as to mimic a production type of environment) is to set the shebang on the first line of `call_process_feed.py` to the path of the virtual environment Python, e.g.:

```python
#!/Users/mac_username/Development/.virtualenvs/virtual_env_name/bin/python

```

**Another tip:** Set the logging level via the `AP WebFeeds Manager` website interface to `Debug`. (Profiles => Profile Preferences tab => Logging => Log level dropdown) Then search for `SCRIPT OUTPUT` lines and the word "Traceback" for Python errors.

To get the ingestion script to run with a local, development set of settings:  
`python manage.py process_feed /Users/jheasly/Development/ap_wfm/WFA/feeds/All-TopHeadlines-JH/feed_644355_2015-06-02T16-39-38.445Z.xml --settings=test_root.local_settings`

Starting tips
-------------
![screenshot 2015-06-05 13 24 33](https://cloud.githubusercontent.com/assets/96007/8014624/249539e8-0b87-11e5-9cd8-9a20316e2da0.png)
Follow the above, then check the below:
![screenshot 2015-06-05 13 32 38](https://cloud.githubusercontent.com/assets/96007/8014708/91d29dc0-0b87-11e5-8f0f-5c59e89bfc12.png)
