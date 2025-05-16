FROM ubuntu:22.04

RUN apt-get update \
	&& apt-get install -y wget \ 
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-py39_22.11.1-1-Linux-x86_64.sh
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniconda3/bin:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniconda3-py39_22.11.1-1-Linux-x86_64.sh -b

# create conda environment
RUN conda init bash && . ~/.bashrc
RUN conda create --name rsde-snapista python=3.9 -y
RUN conda activate rsde-snapista && conda config --add channels conda-forge && conda install -n base mamba && mamba install -c terradue snapista -y \
 
RUN conda activate rsde-snapista >> ~/.bashrc

ENTRYPOINT [ "/bin/bash" ]