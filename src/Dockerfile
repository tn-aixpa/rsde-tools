FROM ubuntu:24.04

RUN apt-get update \
	&& apt-get install -y gcc \
	&& apt-get install -y openjdk-8-jdk \ 
	&& apt-get install -y git \ 
	&& apt-get install -y maven \	
	&& apt-get install -y wget \ 
	&& wget https://repo.anaconda.com/miniconda/Miniconda3-py39_22.11.1-1-Linux-x86_64.sh \
	&& wget https://download.esa.int/step/snap/9.0/installers/esa-snap_sentinel_unix_9_0_0.sh
	
RUN useradd -m -u 8877 nonroot
USER 8877
	
ENV PATH="/home/nonroot/miniconda3/bin:$PATH"
ENV PATH="/home/nonroot/snap/bin:$PATH"
ENV JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-amd64"
RUN mkdir /home/nonroot/.conda && bash Miniconda3-py39_22.11.1-1-Linux-x86_64.sh -b
RUN bash esa-snap_sentinel_unix_9_0_0.sh -q
RUN mkdir /home/nonroot/jpy &&  cd /home/nonroot/jpy && git clone https://github.com/jpy-consortium/jpy.git
RUN mkdir -p /home/nonroot/.snap/snap-python/snappy

# create conda environment
RUN conda init bash && . ~/.bashrc
RUN conda config --set channel_priority flexible
RUN conda config --add channels conda-forge
RUN conda create --name rsde python=3.9
SHELL ["conda", "run", "-n", "rsde", "/bin/bash", "-c"]
RUN conda install gdal -y
RUN conda install libgdal-jp2openjpeg -y
RUN conda install scikit-image scikit-learn pandas -y
# Build JPY
RUN cd /home/nonroot/jpy/jpy && pip install setuptools wheel && python setup.py bdist_wheel
# Copy whl
#RUN cp /home/nonroot/jpy/jpy/dist/*.whl /home/nonroot/.snap/snap-python/snappy
# Snappy configuration
#RUN snappy-conf /home/nonroot/miniconda3/envs/rsde/bin/python

RUN echo "conda activate rsde" >> ~/.bashrc
ENTRYPOINT [ "/bin/bash" ]