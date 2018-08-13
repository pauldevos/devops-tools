
# Installation and Setup of Airflow




# Example DAGs

#### Useful DAG arguments to consider:
- default_args (for the tasks you put into it)
- max_active_runs  #avoid AF from starting all the runs at once

#### Airflow.cfg
- concurrency # limit ways to not kill your DB
- retries
- pool
- queue (Celery only)
		- can associate tasks for specific computers (e.g. memory intensive)
