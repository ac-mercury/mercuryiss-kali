# Name:         Dockerfile
# Description:  build the mercuryiss/kali docker image
# Date:         2018-01-09
# Author:       Alexi Chiotis - Mercury ISS

FROM kalilinux/kali-linux-docker

# HACK: prepend AARNet mirror so as to circumvent apt-get 404s
RUN sed -i "s/https\.kali\.org/mirror\.aarnet\.edu\.au\/pub\/kali/g" /etc/apt/sources.list

# update the archive keyring 
# https://unix.stackexchange.com/questions/421985/invalid-signature-when-trying-to-apt-get-update-on-kali
RUN apt-get update && apt-get install -y gnupg curl
#RUN wget -q -O - https://archive.kali.org/archive-key.asc  | apt-key add
RUN curl https://archive.kali.org/archive-key.asc | apt-key add

# get faster mirrors into apt/sources.list
#RUN apt-get update && apt-get install -y netselect-apt
#RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak
#RUN netselect-apt
#RUN cp sources.list /etc/apt/sources.list

# default install is bare, install some tools 
RUN apt-get update && apt-get install -y \
    arachni \
    beef-xss \
    cutycapt \
    dirbuster \
    exploitdb \
    fierce \
    firefox-esr \
    git \
    gpp-decrypt \
    hydra \
    john \
    locate \
    man \
    metasploit-framework \
    nbtscan \
    netselect-apt \
    nikto \ 
    nmap \
    python-pip \
    responder \
    skipfish \
    sparta \
    sqlitebrowser \
    sqlmap \
    unicornscan \
    vim \
    virtualenv \
    websploit \
    whois \
    wordlists \
    wpscan \
    zenmap

# install those packages that have interactive installation method
WORKDIR /tmp
# set up powershell-empire
RUN apt-get install -y multiarch-support
RUN wget http://http.us.debian.org/debian/pool/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u7_amd64.deb
RUN dpkg -i libssl1.0.0_1.0.1t-1+deb8u7_amd64.deb
WORKDIR /usr/share
RUN git clone https://github.com/EmpireProject/Empire empire
WORKDIR empire/setup
RUN printf "Y\n\n" | ./install.sh
WORKDIR /usr/bin
RUN echo 'cd /usr/share/empire/ && /usr/share/empire/empire' > empire && chmod +x empire 

# use our custom .bashrc, used for different colour prompt string
COPY bashrc /root/.bashrc 
# TODO append localhost entry to container /etc/hosts for sudo
COPY hosts /etc/hosts
# Set local timezone
RUN cp /usr/share/zoneinfo/Australia/Sydney /etc/localtime

# accept --build-arg arguments
ARG USERNAME
ARG UID
ARG GID

# copy these host environment variables into the container environment
ENV USERNAME=$USERNAME
ENV UID=$UID
ENV GID=$GID
ENV COLUMNS=$COLUMNS
ENV LINES=$LINES

# add pentest user within kali and run as non-privileged, in sudo group
# note that if you use --net to start container, the username passed should be
# available in the host's /etc/passwd
# http://wiki.ros.org/docker/Tutorials/GUI 
RUN useradd -m $USERNAME && \
    echo "$USERNAME:$USERNAME" | chpasswd && \
    usermod --shell /bin/bash $USERNAME && \
    usermod -aG sudo $USERNAME && \
    echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/$USERNAME && \
    chmod 0440 /etc/sudoers.d/$USERNAME && \
    usermod  --uid $UID $USERNAME && \
    groupmod --gid $GID $USERNAME

USER $USERNAME
ENV HOME /home/$USERNAME
WORKDIR $HOME

RUN ln -s /usr/share/wordlists/
RUN ln -s /var/www/html/ www
RUN ln -s /data
RUN ln -s /scripts
RUN ln -s /installers

COPY bashrc .bashrc
# https://raw.githubusercontent.com/makefu/dnsmap/master/wordlist_TLAs.txt
COPY dnsmap.txt wordlists/

