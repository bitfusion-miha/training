FROM nvidia/cuda:9.0-cudnn7-runtime-ubuntu16.04
WORKDIR /research

RUN apt-get update
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    build-essential \
    git \
    python \
    python-pip \
    locales

RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8

ENV HOME /research
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN apt-get install -y python-setuptools
RUN apt-get install -y python-pip python3-pip virtualenv htop
RUN pip3 install virtualenv
RUN pip3 install virtualenvwrapper
RUN pip3 install --upgrade numpy scipy sklearn
# Mount data into the docker
ADD . /research/reinforcement
WORKDIR /research/reinforcement
# RUN /bin/bash env_setup.sh

ENV LC_CTYPE en_US.UTF-8
ENV LANG en_US.UTF-8

RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools
RUN pip3 install -r minigo/requirements.txt

RUN pip3 install "tensorflow-gpu>=1.5,<1.6"

ENTRYPOINT ["/bin/bash"]

ENV CUDNN_VERSION 7.0.5.15
RUN apt-get update && apt-get install -y --no-install-recommends --allow-downgrades --allow-change-held-packages \
     libcudnn7=$CUDNN_VERSION-1+cuda9.0 \
 && \
     apt-mark hold libcudnn7 && \
     rm -rf /var/lib/apt/lists/*
