FROM ubuntu:trusty

ENV DEBIAN_FRONTEND noninteractive

RUN useradd runtime -m -p password -s /bin/bash

# chinese language package
RUN locale-gen zh_CN.UTF-8

# update
RUN apt-get update && apt-get install -y \
    git \
    python-dev \
    vim \
    python-pip \
    libfreetype6-dev \
    libjpeg8-dev \
    && rm -rf /var/lib/apt/lists/*

ADD ./requirement.txt /home/runtime/requirement.txt

RUN pip install -r /home/runtime/requirement.txt

ADD ./code /home/runtime/affiliateleadhug
ADD ./entrypoint /home/runtime/affiliateleadhug/app/affiliateleadhug/entrypoint

RUN chown -R runtime:runtime /home/runtime

WORKDIR /home/runtime/affiliateleadhug
USER runtime

EXPOSE 20000

ENTRYPOINT ["/home/runtime/affiliateleadhug/app/affiliateleadhug/entrypoint"]
