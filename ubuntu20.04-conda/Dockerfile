# Usages:
# - build the image (may take 11 minutes)
#   $ docker build -t ubuntu20.04-conda .
#
# - run the image
#   $ docker run --rm -it ubuntu20.04-conda
#


# base image
FROM ubuntu:20.04


# [Software Repository]
#
# update the Ubuntu software repository 
#
# - for the 'tzdata' package, or you will meet:
#   E: Unable to locate package tzdata
#
# - for the 'software-properties-common' package, or you will meet:
#   E: Unable to locate package software-properties-common
#
RUN apt-get update \
    && apt-get install -y curl wget


# Install conda
# -------------------------------------------------------------------
# Install Miniconda 75.7 MB
#
# Note:
#  - The conda command might be updated frequently.
#     - https://docs.conda.io/projects/conda/en/latest/release-notes.html
#        - 4.12.0 (2022-03-08)
#        - 4.11.0 (2021-11-22)
#  - Since Miniconda is smaller (75.7 MB), 
#    let's always get the Miniconda installer from online.
#
#  - wget
#     -q, --quiet:
#        quiet (no output)
# 
#  - Miniconda3-latest-Linux-x86_64.sh
#     -b:
#        run install in batch mode (without manual intervention),
#        it is expected the license terms are agreed upon
#
RUN wget -q https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && chmod +x ./Miniconda3-latest-Linux-x86_64.sh \
    && ./Miniconda3-latest-Linux-x86_64.sh -b \
    && rm ./Miniconda3-latest-Linux-x86_64.sh

# Add Conda path to your environment path
ENV PATH="/root/miniconda3/bin:${PATH}"
RUN conda --version

# Update Conda if needed
# -------------------------------------------------
# ==> WARNING: A newer version of conda exists. <==
#  current version: 4.12.0
#  latest version: 4.14.0
#
# Please update conda by running
# -------------------------------------------------
RUN conda update -n base -c defaults conda


# Install Python 3.7 / 3.8 / 3.9
RUN conda create -y --name python3.9 python=3.9
RUN conda create -y --name python3.8 python=3.8
RUN conda create -y --name python3.7 python=3.7


# Init conda configuration
RUN conda init



# ===================================================================
# DEMO: set the default environment in Dockerfile
# ===================================================================
RUN echo 'conda activate python3.9' >> ~/.bashrc



# ===================================================================
# DEMO: switch to other environments in Dockerfile
# ===================================================================
# - note
#   $ conda activate python3.9 # cannot work
#
# - troubleshooting
#   $ source ~/.bashrc
#   /bin/sh: 1: source: not found --> SHELL ["/bin/bash", "-c"]
#
# for the source command, or you will get `source` not found
SHELL ["/bin/bash", "-c"]

RUN source activate python3.9 && python3 --version  # Python 3.9.12
RUN source activate python3.8 && python3 --version  # Python 3.8.13
RUN source activate python3.7 && python3 --version  # Python 3.7.13



# ===================================================================
# Usages: operate conda commands
# ===================================================================
# Usages:
# - list curretn environment
#   $ conda env list
#
# - switch to another environment
#   $ conda ativate python3.9
#
# - switch to the base environment (exit the python3.9 environment)
#   (python3.9) $ conda deativate
