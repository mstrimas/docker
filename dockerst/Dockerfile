# docker image for ebird status and trends
FROM mstrimas/geospatial

MAINTAINER "Matt Strimas-Mackey" mes335@cornell.edu
LABEL maintainer="Matt Strimas-Mackey <mes335@cornell.edu>"

# system tools needed
RUN apt-get update -y \
  && apt-get install -y \
    awscli \
    expect \
    ffmpeg \
    imagemagick libmagick++-dev \
    rsync

# ImageMagick default policy we were getting was extremely restrictive
# (Memory: 256MiB, Disk: 1GiB) which basically made it useless. We don't need
# to impose any system-wide restrictions like that so just remove policy and
# use ImageMagick defaults/commandline values.
RUN rm -f /etc/ImageMagick-6/policy.xml

# R packages needed
RUN install.r \
    DBI DescTools MASS PresenceAbsence RSQLite \
    argparse auk \
    car \
    digest \
    exactextractr \
    fastshap fields \
    gbm grf \
    landscapemetrics lutz \
    mgcv \
    pryr prioritizr \
    ranger readr \
    scam smoothr suncalc \
    units uuid \
  && installGithub.r \
    cornelllabofornithology/auk \
    cornelllabofornithology/ebirdst@dev_erd2019 \
    walkerke/mapboxapi
    
# Python packages
RUN python3 -m pip install matplotlib

WORKDIR /home/docker/

CMD ["/start.sh"]
