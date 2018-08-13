
# Installation and Setup of Airflow




## DAGs

```
# useful DAG arguments
-- default_args (for the tasks you put into it)
-- max_active_runs  #avoid AF from starting all the runs at once

# airflow.cfg considerations:
- concurrency # limit ways to not kill your DB
- retries
- pool
- queue (Celery only)
	- can associate tasks for specific computers (e.g. memory intensive)
```

#### Example DAGs

import airflow.models as af_models

DAG = af_models.DAG(
	dag_id = 'my_dag', #unique
	start_date = datetime(2016, 8, 13),
	schedule_interval='0 10 * * *')





for f in files:
	task = af_op.PythonOperator(
		task_id = 'parsing_{}'.format(f),
		python_callable = parse_file,
		op_kwargs= {'fname': f},
		dag = DAG
		)
task.set_upstream(first_task)
