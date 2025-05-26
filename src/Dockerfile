FROM python:3.9

RUN apt-get install -y wget \ 
	&& wget https://github.com/conda-forge/miniforge/releases/download/4.13.0-1/Miniforge3-4.13.0-1-Linux-x86_64.sh
	
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniforge3/bin/:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniforge3-4.13.0-1-Linux-x86_64.sh -b

# install snapista 
RUN conda init bash && . ~/.bashrc 
RUN conda install -n base mamba
RUN mamba install -c terradue snapista -y
RUN mamba install gdal=3.10.1 -y
RUN mamba install libgdal-jp2openjpeg -y
RUN mamba install scikit-image scikit-learn pandas -y

ENTRYPOINT [ "/bin/bash" ]


