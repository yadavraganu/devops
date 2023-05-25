FROM ubuntu
RUN apt-get update
RUN apt-get install -y python3 
RUN apt-get install -y pip
RUN pip install pyspark
RUN pip install jupyterlab
RUN mkdir -p /home/Jupyter
WORKDIR /home/Jupyter
EXPOSE 8888                                           
ENTRYPOINT ["jupyter-lab","--allow-root","--ip=0.0.0.0","--port=8888","--no-browser"]