FROM ubuntu:18.04
# update apt and get miniconda
RUN apt-get update \
    && apt-get install -y wget \
    && wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh


# install miniconda
ENV PATH="/root/miniconda3/bin:$PATH"
RUN mkdir /root/.conda && bash Miniconda3-latest-Linux-x86_64.sh -b

# create conda environment
RUN conda init bash && . ~/.bashrc 
RUN conda update --name base conda
RUN conda config --add channels conda-forge
RUN conda update --all
RUN conda create --name test python=3.10
SHELL ["conda", "run", "-n", "test", "/bin/bash", "-c"]
RUN conda install gdal=3.10.1 && conda install libgdal-jp2openjpeg && conda install scikit-image scikit-learn pandas
RUN echo "conda activate test" >> ~/.bashrc
