FROM python:3.9

RUN apt-get install -y wget \ 
	&& wget https://github.com/conda-forge/miniforge/releases/download/4.13.0-1/Miniforge3-4.13.0-1-Linux-x86_64.sh
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniforge3/bin/:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniforge3-4.13.0-1-Linux-x86_64.sh -b

# install snapista 
RUN conda init bash && . ~/.bashrc 
#RUN conda install -n base mamba -y
RUN conda install -c terradue snapista==0.2.0 -y
RUN conda install -c conda-forge gdal==3.11.0 libgdal-jp2openjpeg -y
RUN conda install -c conda-forge scikit-image==0.24.0 scikit-learn==1.6.1 pandas==2.3.0 -y
RUN conda install -c conda-forge libgcc==14.2.0 -y
RUN conda install -c conda-forge libgfortran5 -y
USER root
RUN ldconfig /home/nonroot/miniforge3/lib
USER 8877

ENTRYPOINT [ "/bin/bash" ]


