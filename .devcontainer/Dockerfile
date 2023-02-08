FROM mcr.microsoft.com/devcontainers/base:bullseye
LABEL author="mlizaur@eventbrite.com"

ARG UID=1000
ARG GID=1000

ENV PYTHONUNBUFFERED 1
ENV LANG C.UTF-8
ENV USER vscode
ENV HOME /development
ENV DEBIAN_FRONTEND noninteractive
ENV GITHUB_TOKEN s3cr3t
ENV GITHUB_USER $USER
WORKDIR $HOME

COPY requirements.txt $HOME/requirements.txt
COPY .bashrc $HOME/.bashrc

RUN apt-get update && \
    apt-get install -qq --no-install-recommends \
    gcc git-core build-essential python3-dev python3-pip \
    jq curl zip unzip less locales ca-certificates && \
    pip --no-cache-dir install -U pip && \
    pip install -r $HOME/requirements.txt && \
    rm -fr $HOME/.cache ${HOME}/requirements.txt && \
    chown -R $USER:$USER $HOME && \
    apt clean && apt autoremove

EXPOSE 8080
USER $USER
