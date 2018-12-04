# Cloudera Data Science Workbench

Basic tour of Cloudera Data Science Workbench (CDSW).

## 1. Platform Overview

### 1.1. Architecture

*TODO* 
- relationship with CDH, 
- admin account, 
- kubernates and docker, 
- engines (Mem, CPUs and GPUs).

### 1.2. Website - User Interface
Upon login into CDSW, you are presented with the Projects page. On the left menu, you have 6 tabs:

**Projects**
List of all your open Projects, plus on the top you have a quick glance at stats and available resources in the CDSW cluster. 

**Sessions**
List of all your open and closed Sessions. A Session is a compute environment loaded with Python/R/Scala libraries and with access to the filesystem.

**Experiments**
List of all Experiments run and the collected metrics. 

**Models**
List of all deployed Models.

**Jobs**
List of all Jobs run across all your projects.

**Settings**
The Settings page gives you access to:
- your Profile information.
- SSH Keys.
- Hadoop Authentication via Kerberos.
- API Keys.


## 2. Demo Excercises

### 2.1. Initial setup

Create a new project using this GitHub project as your initial setup. The project main page is presented to you. Here you have 8 tabs:

**Overview**: quick overview of the project, including displaying the README.md file.

**Sessions**: list of open session for this project.

**Experiments**: list of project experimets. 

**Models**: list of deployed project models

**Jobs**: list of project jobs

**Files**: list of files included in this project.

**Team**: this page allows you to add collaborators to this project.

**Settings**: this page allows you to select the Engine, set the visibility, and delete the project.

Open the Workbench and start a new Python2 Session, then run the following command to install some required libraries:
```
!pip2 install --upgrade pip dask keras matplotlib pandas_highcharts protobuf tensorflow seaborn
```
Please note: as libraries are updated, dependancies might break: please check the output log and fix the dependancies. For example, you might have to install a specific version of setuptools or numpy for tensorflow to install properly.

Start a new R Session, and run these commands:
```
install.packages('sparklyr')
install.packages('plotly')
install.packages("nycflights13")
install.packages("Lahman")
install.packages("mgcv")
install.packages('shiny') 
```

Stop and restart all sessions for changes to take effect.

### 2.2. Workbench

In the project you'll find 4 scripts which walk you through the interactive capabilities of CDSW.

`1_python.py` demonstrates:
  - Markdown via comments
  - Jupyter-compatible visualizations
  - Simple console sharing

`2_pyspark.py` demonstrates:
  - Easy connectivity to (kerberized) Spark in YARN client mode.
  - Access to Hadoop HDFS CLI (e.g. `hdfs dfs -ls /`).

`3_tensorflow.py` demonstrates:
  - Ability to install and use custom packages (e.g. `pip search tensorflow`)

`4_sparklyr.R` demonstrates:
  - Use familiar dplyr with Spark using [Sparklyr](http://spark.rstudio.com)

`5_shiny.R` demonstrates:
  - Use of shiny to provide interactive graphics inside CDSW

*TODO: add scala example*

### 2.3. Experiments

Run a few experiments using file `6_experiment.py` as Script and any space separated integer list as Arguments. The code is trivial but should give you an idea of what challenges this feature solves.

### 2.4. Models

In a Python2 workbench, run code `7_fit.py`. The code builds a model to predict the width of a petal from its length. The code uses a built-in dataset to train the model, but you should think of it as reading the raw data from a Hadoop cluster. The model is then saved as file petalWidthModel.pkl.

Create a new Model using Script `8_predict.py` using function `predict`. The code loads the model previously saved and allows you to pass an argument, 'petal_length'. CDSW deploys the model and provides you with REST APIs to call the model. Try by sending 

    {"petal_length":15} 

to check what is the predicted width of the petal.

### 2.5. Jobs

CDSW allows you to schedule a job - run some code - at a specific time or interval. For example, you can schedule `7_fit.py` to run every week on new data that you have collected, so that the model it builds becomes more precise with the updated data.
*TODO examples*
