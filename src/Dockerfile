FROM python:3.9

RUN apt-get install -y wget \ 
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-py39_22.11.1-1-Linux-x86_64.sh
	
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniconda3/bin:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniconda3-py39_22.11.1-1-Linux-x86_64.sh -b

# install snapista 
RUN conda init bash && . ~/.bashrc 
RUN conda config --add channels conda-forge
RUN conda install -n base mamba
RUN mamba install -c terradue snapista -y

ENTRYPOINT [ "/bin/bash" ]


