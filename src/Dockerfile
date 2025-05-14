FROM ubuntu:18.04

RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:deadsnakes/ppa \
    && apt-get install -y python \
	&& apt-get install -y wget \ 
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-py39_22.11.1-1-Linux-x86_64.sh
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniconda3/bin:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniconda3-py39_22.11.1-1-Linux-x86_64.sh -b

# create conda environment
RUN conda init bash && . ~/.bashrc
RUN conda config --set channel_priority flexible
RUN conda config --add channels conda-forge
RUN conda create --name rsde python=3.9
SHELL ["conda", "run", "-n", "rsde", "/bin/bash", "-c"]
RUN conda install terradue::snapista -y
RUN conda install libgdal-jp2openjpeg -y
RUN conda install scikit-image scikit-learn pandas -y
RUN echo "conda activate rsde" >> ~/.bashrc

ENTRYPOINT [ "/bin/bash" ]