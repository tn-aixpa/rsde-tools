FROM ubuntu:18.04

# update apt and get miniconda
RUN apt-get update \
    && apt-get install -y wget \
    && wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

# user
RUN useradd -m -u 8877 rsde
USER 8877

# install miniconda
ENV PATH="/home/rsde/miniconda3/bin:$PATH"
RUN mkdir /home/rsde/.conda && bash Miniconda3-latest-Linux-x86_64.sh -b

# create conda environment
RUN conda init bash && . ~/.bashrc 
RUN conda update --name base conda
RUN conda config --add channels conda-forge
RUN conda update --all
RUN conda create --name rsde python=3.10
SHELL ["conda", "run", "-n", "rsde", "/bin/bash", "-c"]
RUN conda install gdal=3.10.1 && conda install libgdal-jp2openjpeg && conda install scikit-image scikit-learn pandas
RUN echo "conda activate rsde" >> ~/.bashrc