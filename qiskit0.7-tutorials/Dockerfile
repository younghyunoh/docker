FROM buildpack-deps:bionic
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -qq && \ 
    apt-get install -qq --yes --no-install-recommends locales &&  \
    apt-get purge -qq && \ 
    apt-get clean -qq && \ 
    rm -rf /var/lib/apt/lists/*
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV SHELL /bin/bash
ARG NB_USER=ohy
ARG NB_UID=501
ENV HOME /home/${NB_USER}
RUN adduser --disabled-password --gecos "Default user" --uid ${NB_UID} ${NB_USER}
WORKDIR ${HOME}
RUN wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key |  apt-key add - && \
    DISTRO="bionic" && \  
    echo "deb https://deb.nodesource.com/node_10.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list &&  \
    echo "deb-src https://deb.nodesource.com/node_10.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list
RUN apt-get update -qq && \ 
    apt-get install -qq --yes --no-install-recommends less nodejs unzip && \
    apt-get purge -qq && \
    apt-get clean -qq && \
    rm -rf /var/lib/apt/lists/*
EXPOSE 8888
ENV APP_BASE /srv
ENV CONDA_DIR ${APP_BASE}/conda
ENV NB_PYTHON_PREFIX ${CONDA_DIR}
ENV KERNEL_PYTHON_PREFIX ${NB_PYTHON_PREFIX}
ENV PATH ${CONDA_DIR}/bin:$HOME/.local/bin:${PATH}
COPY conda/install-miniconda.bash /tmp/install-miniconda.bash
COPY conda/environment.py-3.5.frozen.yml /tmp/environment.yml
RUN bash /tmp/install-miniconda.bash && \ 
    rm /tmp/install-miniconda.bash /tmp/environment.yml
USER root
RUN apt-get update && \ 
    apt-get install --yes --no-install-recommends git && \
    apt-get purge && apt-get clean && rm -rf /var/lib/apt/lists/*
RUN git clone https://github.com/Qiskit/qiskit-tutorials.git
COPY environment.yml ${HOME}
RUN chown -R ${NB_USER}:${NB_USER} ${HOME}
RUN apt-get update && \ 
    apt-get install --yes --no-install-recommends texlive-latex-base texlive-latex-recommended texlive-science texlive-latex-extra texlive-fonts-recommended dvipng ghostscript    poppler-utils && \
    apt-get purge && apt-get clean && rm -rf /var/lib/apt/lists/*
USER ${NB_USER}
RUN conda env update -n root -f "environment.yml" && \ 
    conda clean -tipsy && conda list -n root
USER ${NB_USER}
CMD ["jupyter", "notebook", "--ip", "0.0.0.0"]
