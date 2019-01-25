FROM neurodebian:stretch-non-free
MAINTAINER Yaroslav O. Halchenko <debian@onerussian.com>
    
# Make image reproducible based on the date/state of things in Debian/NeuroDebian
# land.
# Time format yyyymmdd 
RUN nd_freeze 20181221

# To prevent interactive debconf during installations
ARG DEBIAN_FRONTEND=noninteractive

# Make directory for flywheel spec (v0)
# TODO:  gearificator prepare-docker recipename_or_url
# cons: would somewhat loose cached steps (pre-installation, etc)
# For now -- entire manual template
RUN apt-get update && echo "count 1" \
    && apt-get install -y --no-install-recommends python-pip python-nipype \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Download/Install gearificator suite
# TODO  install git if we do via git
RUN apt-get update \ 
    && apt-get install -y git python-setuptools \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# TEMPMOVE RUN git clone git://github.com/yarikoptic/gearificator /srv/gearificator && echo 7
# TEMPMOVE RUN pip install -e /srv/gearificator

# Common to all gears settings
ENV FLYWHEEL /flywheel/v0
RUN mkdir -p ${FLYWHEEL}

# e.g. Nipype and other pythonish beasts might crash unless 
ENV LC_ALL C.UTF-8

# Now we do this particular Gear specific installations

RUN apt-get update \ 
    && apt-get install -y --no-install-recommends python-nipype ants \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pip install  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
    
RUN git clone git://github.com/yarikoptic/gearificator /srv/gearificator && echo 7
RUN pip install -e /srv/gearificator && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY run ${FLYWHEEL}/run
COPY manifest.json ${FLYWHEEL}/manifest.json

# Configure entrypoint
ENTRYPOINT ["/flywheel/v0/run"]
