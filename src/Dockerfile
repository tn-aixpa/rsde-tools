FROM ubuntu:25.04

RUN apt-get update \
	&& apt-get install -y wget \ 
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
	
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniconda3/bin:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniconda3-latest-Linux-x86_64.sh -b

# create conda environment
RUN conda init bash && . ~/.bashrc
RUN conda config --add channels conda-forge
RUN conda install -n base mamba
RUN conda create --name rsde python=3.9
SHELL ["conda", "run", "-n", "rsde", "/bin/bash", "-c"]
RUN mamba install -c terradue snapista

RUN conda activate rsde >> ~/.bashrc

ENTRYPOINT [ "/bin/bash" ]

