# https://hub.docker.com/r/jupyter/datascience-notebook/tags
FROM jupyter/datascience-notebook:x86_64-lab-4.0.7

USER root
RUN \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get dist-upgrade -y && \
    apt-get autoclean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*

RUN apt update && apt install --yes \
    git \
    dnsutils \
    netcat

USER $NB_USER

RUN pip install --upgrade jupyterlab jupyterlab-git

RUN pip install pydruid

RUN pip install jupyter-archive

RUN pip install s3fs jupyterlab-s3-browser && \
    jupyter server extension enable --py jupyterlab_s3_browser --sys-prefix

RUN pip install s3fs

RUN pip install geopy ipyleaflet

WORKDIR $HOME
