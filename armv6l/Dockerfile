FROM arm32v6/debian:stretch-slim

ENV LANG C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:/bin:$PATH

RUN apt-get update && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget -q -O ~/berryconda.sh https://github.com/jjhelmus/berryconda/releases/download/v2.0.0/Berryconda3-2.0.0-Linux-armv6l.sh && \
    /bin/bash ~/berryconda.sh -b -p /opt/conda && \
    rm ~/berryconda.sh && \ 
    /opt/conda/bin/conda list && \
    /opt/conda/bin/conda install conda-build && \
    /opt/conda/bin/conda clean -tipsy 
    
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-armhf /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]
