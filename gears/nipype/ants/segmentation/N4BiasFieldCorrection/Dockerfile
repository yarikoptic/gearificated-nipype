FROM neurodebian:stretch
MAINTAINER Yaroslav O. Halchenko <debian@onerussian.com>
    
# TODO: use snapshots for reproducible image!
# Install additional APT mirror for NeuroDebian for better availability/resilience
RUN echo deb http://neurodeb.pirsquared.org data main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo deb http://neurodeb.pirsquared.org stretch main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list

# To prevent interactive debconf during installations
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y eatmydata

# Make directory for flywheel spec (v0)
# TODO:  gearificator prepare-docker recipename_or_url
# cons: would somewhat loose cached steps (pre-installation, etc)
# For now -- entire manual template
RUN eatmydata apt-get update && echo "count 1" && \
    eatmydata apt-get install -y --no-install-recommends python-pip python-nipype

# Download/Install gearificator suite
# TODO  install git if we do via git
RUN eatmydata apt-get install -y git python-setuptools
# TEMPMOVE RUN git clone git://github.com/yarikoptic/gearificator /srv/gearificator && echo "6"
# TEMPMOVE RUN pip install -e /srv/gearificator

# Common to all gears settings
ENV FLYWHEEL /flywheel/v0
RUN mkdir -p ${FLYWHEEL}

# e.g. Nipype and other pythonish beasts might crash unless 
ENV LC_ALL C.UTF-8

# Now we do this particular Gear specific installations
RUN eatmydata apt-get install -y --no-install-recommends python-nipype ants
RUN apt-get clean

    
RUN git clone git://github.com/yarikoptic/gearificator /srv/gearificator && echo "6"
RUN pip install -e /srv/gearificator

COPY run ${FLYWHEEL}/run
COPY manifest.json ${FLYWHEEL}/manifest.json

# Configure entrypoint
ENTRYPOINT ["/flywheel/v0/run"]
