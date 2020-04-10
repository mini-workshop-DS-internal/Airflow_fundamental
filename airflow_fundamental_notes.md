## Airflow Fundamental
### The concept

- Components
<p align="center">
   <img src="airflow_img/1_im.png">
</p>

- Key Concepts in Airflow
<p align="center">
   <img src="airflow_img/2_im.png">
</p>

- benefit of airflow
<p align="center">
   <img src="airflow_img/3_im.png">
</p>

- this is not
<p align="center">
   <img src="airflow_img/4_im.png">
</p>

- Case for airflow utilities
<p align="center">
   <img src="airflow_img/5_im.png">
</p>

- How to manage so many kind of pipelines
<p align="center">
   <img src="airflow_img/6_im.png">
</p>

- architecture using one node
<p align="center">
   <img src="airflow_img/7_im.png">
</p>

- architecture using multiple node
<p align="center">
   <img src="airflow_img/8_im.png">
</p>

- comparing with Google Composer
<p align="center">
   <img src="airflow_img/architecture_composer_gcp.svg">
</p>

- first scheduler reads dag folder n see if it's scripts meets the criteria
<p align="center">
   <img src="airflow_img/9_im.png">
</p>

- if meets then create DagRun in DB, registering it's scripts so then DagRun is Running
<p align="center">
   <img src="airflow_img/10_im.png">
</p>

- schedule TaskInstances to run then TaskInstance Scheduled
<p align="center">
   <img src="airflow_img/11_im.png">
</p>

- Scheduler send TaskInstance to Executor, Executor send TaskInstance to Queueing System then TaskInstance Queued
<p align="center">
   <img src="airflow_img/12_im.png">
</p>

- Executor pulls out TaskInstance then updates the TaskInstance in MetaDB to running , so then Worker executing TaskInstance
<p align="center">
   <img src="airflow_img/13_im.png">
</p>

- After Task Finished, Executor will updates TaskInstance to Success but DagRun still running to next task in that Dag
<p align="center">
   <img src="airflow_img/14_im.png">
</p>

- After All Task Finished in Dag, Scheduler will updates to MetaDB DagRun Success, or if one task is fail so DagRun will update to Failed
<p align="center">
   <img src="airflow_img/15_im.png">
</p>

- Web Server read MetaDB to Update UI
<p align="center">
   <img src="airflow_img/16_im.png">
</p>

- Summaries
<p align="center">
   <img src="airflow_img/18_im.png">
</p>

1. The Scheduler reads the DAG folder
2. Your DAG is parsed by a process to create a DagRun based on the scheduling parameter of your DAG
3. A TaskInstance is instantiated for each Task that needs to be executed and flagged to "Scheduled" in the metadata database
4. The Scheduler gets all TaskInstance flagged "Scheduled" from the metadata database, changes the state to "Queued" and sends them to the executors to be executed.
5. Executors pull out Tasks from the queue (depending on your execution setup), changes the state from "Queued" to "Running" and Workers start executing the TaskInstances
6. When a Task is finished, the Executor changes the state of that task to its final state (success, failed, etc) in the databse and the DagRun is updated by the Scheduler with the state "Success" or "Failed" of course, the web server periodically fetch data from metadaDB to update the UI