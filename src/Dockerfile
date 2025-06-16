FROM ubuntu:25.04

RUN apt-get update \
	&& apt-get install -y wget \ 
	&& wget  wget https://github.com/conda-forge/miniforge/releases/download/4.13.0-1/Miniforge3-4.13.0-1-Linux-x86_64.sh \
	&& wget https://download.esa.int/step/snap/10_0/installers/esa-snap_sentinel_linux-10.0.0.sh
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniforge3/bin/:$PATH"
RUN mkdir /home/nonroot/.conda && bash Miniforge3-4.13.0-1-Linux-x86_64.sh -b

RUN mkdir -p home/nonroot/.snap/snap-python/esa_snappy
RUN bash esa-snap_sentinel_linux-10.0.0.sh -q
RUN snap --nosplash --nogui --modules --update-all 2>&1 | while read -r line; do echo "$line"; [ "$line" = "updates=73" ] && sleep 2 && pkill -TERM -f "esa-snap/jre/bin/java"; done;exit 0

## create conda environment
RUN conda init bash && . ~/.bashrc

RUN conda init bash && . ~/.bashrc 
RUN conda install -n base mamba
RUN mamba install gdal=3.10.1 -y
RUN mamba install libgdal-jp2openjpeg -y
RUN mamba install scikit-image scikit-learn pandas -y
RUN snap --nosplash --nogui --modules --install eu.esa.snap.esa.snappy \
    && snap --nogui --nosplash --snappy /home/nonroot/miniforge3/bin/python \
    && cp -r /home/nonroot/.snap/snap-python/esa_snappy /home/nonroot/miniforge3/lib/python3.10/site-packages/ \
	&& conda install gdal=3.10.1 -y \
	&& conda install libgdal-jp2openjpeg -y \
	&& conda install scikit-image scikit-learn pandas -y

ENTRYPOINT [ "/bin/bash" ]
