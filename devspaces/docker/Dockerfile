FROM ubuntu:bionic

LABEL description="Devspaces implementation for Snapcraft.io"

# Set git commit ID
ARG COMMIT_ID

# Set which webapp configuration to load
ARG WEBAPP=snapcraft

# Optimise environment variables
ENV BLOG_CATEGORIES_ENABLED false \
    BLOG_ENABLED true \
    BSI_URL https://build.snapcraft.io \
    COMMIT_ID "${COMMIT_ID}" \
    DEVEL True \
    ENVIRONMENT devel \
    FLASK_DEBUG true \
    LANG C.UTF-8 \
    LC_ALL C.UTF-8 \
    NOKOGIRI_USE_SYSTEM_LIBRARIES true \
    PORT 8004 \
    SECRET_KEY local_development_fake_key \
    WEBAPP "${WEBAPP}" 

# Install system packages (ruby, python, node and build libraries)
RUN apt-get update && \
    apt-get install --yes \
        build-essential \
        curl \
        git \   
        jq \
        libjpeg-dev \
        libjpeg-progs \
        libmagickwand-dev \
        libpng-dev \
        libpq-dev \ 
        libsodium-dev \
        nodejs \
        npm \
        optipng \ 
        python-launchpadlib \
        python3-dev python3-pip \
        ruby-bundler \ 
        ruby-dev \ 
        vim \ 
        zlib1g-dev

# Supportive python tools for debugging, syntax checking and DB connectivity
RUN pip3 install --upgrade \
                      flake8 \
                      ipdb \
                      pipenv \
                      psycopg2 \
                      pymongo \
                      python-swiftclient


# Latest Yarn package manager and bower
RUN npm install --global bower yarn

# Create a shared home directory - this helps anonymous users have a home
WORKDIR /home/shared
ENV HOME=/home/shared 

RUN mkdir -p $HOME \
 && mkdir -p $HOME/.cache/yarn/ \
 && mkdir -p $HOME/.cache/bower/ \
 && chmod -R 777 $HOME

# SSH agent finds up home using /etc/passwd
# Fix for .ssh folder
RUN mkdir -p $HOME/.ssh \
 && ln -s $HOME/.ssh /root/.ssh

WORKDIR /data

EXPOSE 80

CMD tail -f /dev/null
