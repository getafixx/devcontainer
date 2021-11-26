# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.205.2/containers/php/.devcontainer/base.Dockerfile

# [Choice] PHP version (use -bullseye variants on local arm64/Apple Silicon): 8, 8.0, 7, 7.4, 7.3, 8-bullseye, 8.0-bullseye, 7-bullseye, 7.4-bullseye, 7.3-bullseye, 8-buster, 8.0-buster, 7-buster, 7.4-buster, 7.3-buster
ARG VARIANT="7.4"
FROM mcr.microsoft.com/vscode/devcontainers/php:0-${VARIANT}

# [Choice] Node.js version: none, lts/*, 16, 14, 12, 10
ARG NODE_VERSION="16"
RUN if [ "${NODE_VERSION}" != "none" ]; then su vscode -c "umask 0002 && . /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

RUN apt-get upgrade

RUN apt-get update

RUN apt-get update -y && \
    apt-get --fix-missing  -y install \    
    ca-certificates software-properties-common curl nano \
    unzip git unzip vim wget libmcrypt-dev libreadline-dev \
    bash-completion iputils-ping build-essential git-flow \
    ssh dos2unix ssmtp rsync apt-transport-https gnupg-agent \
    gnupg awscli s3cmd snapd libpq-dev libpython3-dev python3-virtualenv && \
    pip3 install tox && \
    python3 -m pip install virtualenv && \
    pip install --upgrade pip setuptools
    

RUN git clone https://github.com/ahmetb/kubectx /opt/kubectx && \
    ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx && \
    ln -s /opt/kubectx/kubens /usr/local/bin/kubens && \
    locale-gen en_US.UTF-8 && \
    localedef -i en_US -f UTF-8 en_US.UTF-8 && \
    wget https://github.com/wercker/stern/releases/download/1.11.0/stern_linux_amd64 -o /usr/local/bin/stern && chmod 755 /usr/local/bin/stern && \
    wget https://github.com/bitnami-labs/sealed-secrets/releases/download/v0.16.0/kubeseal-linux-amd64 -o /usr/local/bin/kubeseal && chmod 755 /usr/local/bin/kubeseal 


#RUN add-apt-repository ppa:ondrej/php
#RUN apt-get update

#RUN apt-get install -y php7.4

#RUN apt-get update

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --2

RUN curl -LO https://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep

RUN apt-get update --fix-missing

#RUN sed -i 's/short_open_tag = Off/short_open_tag = On/' /etc/php/7.4/fpm/php.ini
#RUN sed -i 's/post_max_size = 8M/post_max_size = 50M/' /etc/php/7.4/fpm/php.ini
#RUN sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 50M/' /etc/php/7.4/fpm/php.ini

#WORKDIR /var/www/
