FROM ubuntu:18.04
# update apt and get miniconda
RUN apt-get update \
    && apt-get install -y wget \
    && wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh


# install miniconda
ENV PATH="/root/miniconda3/bin:$PATH"
RUN mkdir /root/.conda && bash Miniconda3-latest-Linux-x86_64.sh -b

# create conda environment
RUN conda update --name base conda
RUN conda config --add channels conda-forge
RUN conda update --all
RUN conda create --name test python=3.10
RUN /bin/bash -c ". activate test"
RUN conda install gdal=3.10.1
RUN conda install libgdal-jp2openjpeg
RUN conda install scikit-image scikit-learn pandas

#RUN conda init bash && . ~/.bashrc 
#CMD ["/bin/sh", "conda activate test"]
#RUN /bin/bash -c ". activate test"
#RUN conda activate test

# STEPS
#1  conda update -n base conda
#2. conda config --add channels conda-forge
#3. conda update –all 
#4. conda create –-name test python=3.10  
#5. conda activate test
#6. conda install gdal=3.10.1
#7. conda install libgdal-jp2openjpeg
#9. Change to project directory /.
#8. pip install -r requirements.txt
#9. python main.py
#10.log artifacts