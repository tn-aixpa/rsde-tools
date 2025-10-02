# RSDE-TOOLS

The main purpose of the tool is to provide perform for different usecases scenarios of remote sensing such as deforestation, flood mapping, and landslide monitoring.

## Usage Scenario

It can be sse as a base image in your own remote sensing scenario specific Dockerfile:

FROM ghcr.io/tn-aixpa/rsde-tools:latest

RUN conda init bash && . ~/.bashrc 

...



