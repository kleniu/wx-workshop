FROM jupyter/base-notebook:latest

RUN pip install --upgrade pip
RUN pip install ibm_watson_machine_learning

EXPOSE 8888

ENTRYPOINT jupyter notebook --ip='*' --NotebookApp.token='' --NotebookApp.password=''

