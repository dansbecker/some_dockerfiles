FROM winglian/axolotl:main-py3.10-cu118-2.0.1

# Set ENV variables
ENV LANG C.UTF-8
ENV SHELL=/bin/bash
ENV DEBIAN_FRONTEND=noninteractive
ENV LD_LIBRARY_PATH=/usr/local/cuda/lib64
ENV BNB_CUDA_VERSION=

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-utils gcc make pkg-config apt-transport-https build-essential \
    ca-certificates wget rsync git vim mlocate libssl-dev curl \
    openssh-client unzip unrar zip csvkit emacs joe jq dialog \
    man-db manpages manpages-dev manpages-posix manpages-posix-dev \
    nano iputils-ping sudo ffmpeg libsm6 libxext6 libboost-all-dev \
    cifs-utils software-properties-common


RUN python3 -m pip --no-cache-dir install --upgrade \
    cloudpickle==2.2.1 ipython==8.19.0 ipykernel==6.28.0 \
    ipywidgets==8.1.1 cython==3.0.7 tqdm==4.65.0 \
    gdown==4.7.1 pillow==10.1.0 \
    tabulate==0.9.0 jsonify==0.5.0 \
    wandb==0.16.1 tornado==6.4.0 \
    jupyterlab==4.0.10 awscli==1.32.11

# gradient install fails because of issue with cython / pyyaml compatibility
# https://github.com/Paperspace/gradient-cli/issues/397
# Commenting out gradient install. Will deal later if paperspace
# not working correctly
# RUN python3 -m pip --no-cache-dir install gradient==2.0.6

# Install JRE and JDK
RUN apt-get install -y default-jre default-jdk

# Paperspace base image had CMake, but I don't know what for
# Commenting out for now
# RUN git clone --depth 10 https://github.com/Kitware/CMake ~/cmake && \
#    cd ~/cmake && ./bootstrap && make -j"$(nproc)" install

# Expose ports and set the startup command
EXPOSE 8888 6006
CMD jupyter lab --allow-root --ip=0.0.0.0 --no-browser --ServerApp.trust_xheaders=True --ServerApp.disable_check_xsrf=False --ServerApp.allow_remote_access=True --ServerApp.allow_origin='*' --ServerApp.allow_credentials=True

