# mlp-automl R version
AutoML project for ML Products for Data Science. 
This tool allows users to upload datasets and with one click, perform
- Descriptive Statistical analyses
- Train different models and
- Evaluate the trained models using AUC

# Instructions for Adam Kelleher
All the code for the R project is under `R` directory

## Project Structure

We used R and Shiny for this project. All files are located under 
the `R` directory. The `shiny.R` file is our app entry point as well as 
the dashboard. We have separated model training, prediction and evaluation
into different services. As well as computing descriptive statistics and 
preprocessing the data.

To run the application, simply clone the repo and launch `shiny.R` 

# mlp-automl python version
Rest API that allows users to upload datasets and perform some statistical
analyses, plot a pairplot and evaluate (AUC) a machine learning model.

## Python version
For best results use Python 3.x

## Dependencies
### Virtual environment
It is best to run this project with on a venv

Install virtualenv

`pip install virtualenv`

Create a virtual environment for project in a separate dir

`virtualenv -p python3 mlp-automl-env`

Activate virtualenv. Navigate to venv dir and run

`source <path-to-venv>/bin/activate`

Later, to deactivate venv run

`deactivate`

### Redis Message Broker
Install the message broker Redis following instructions here:

`https://redis.io/download`

### Package dependencies

From project root dir, install dependencies with 

`pip install -r requirements.txt`

## REST Call to the web service
- Input data files can be found in the dir: `sample_data`
- Make sure the package `gunicorn' is installed
- Navigate to root directory
- Open three terminal tabs and activate venv in each
- Start the webservice with `gunicorn automl:app` one terminal
- Test that the service works by navigting to `localhost:8000/`
- Start redis server with `src/redis-server` in 2nd terminal
- Start celery worker in last terminal tab with `celery worker -A automl.celery --loglevel=inf`
- Create a new job with `curl -XPOST -F 'data=@<path-to-data-file>/iris.data.txt' -F 'target=@<path-to-dataset-dependent-variable-file>/iris.target.txt' localhost:8000/job/`
  The app returns a jobid which will be used to download the results
- Download job results from browser with `localhost:8000/job/<jobid>`
