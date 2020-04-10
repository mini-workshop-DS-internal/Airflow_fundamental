### Airflow_fundamental
Airflow_fundamental for sharing

 [link to Official documentation](http://airflow.apache.org/)

virtualenv -p python3 airflowEnv

### airflow needs a home, ~/airflow is the default,
-
### but you can lay foundation somewhere else if you prefer (optional)

```bash
# example my airflow home --> 
export AIRFLOW_HOME=~/keurseus/berkenalan_dengan_airflow/airflow

# by default
export AIRFLOW_HOME=~/airflow
```

```bash
# install from pypi using pip
pip install apache-airflow

# initialize the database
airflow initdb

# start the web server, default port is 8080
airflow webserver -p 8080 

# start the scheduler in the different terminal , don't forget to set your AIRFLOW_HOME also
airflow scheduler

# visit localhost:8080 in the browser and enable the example dag in the home page
```

Learn more concepts i've been curated [Here](https://github.com/mini-workshop-DS-internal/Airflow_fundamental/blob/master/airflow_fundamental_notes.md)
