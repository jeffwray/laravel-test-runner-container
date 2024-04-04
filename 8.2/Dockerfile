FROM ubuntu:20.04
LABEL maintainer="Jeff Wray <jwray@mobilozophy.com>"
ARG DEBIAN_FRONTEND=noninteractive

ENV GOSS_VERSION="0.3.6"

RUN apt-get update && apt-get install -y software-properties-common curl wget
RUN add-apt-repository ppa:ondrej/php -y
RUN add-apt-repository ppa:git-core/ppa -y
RUN apt-get update -y
RUN apt-get install -y \
    unzip \
    php8.2-cli \
    php8.2-gd \
    php8.2-ldap \
    php8.2-mbstring \
    php8.2-mysql \
    php8.2-pgsql \
    php8.2-sqlite3 \
    php8.2-xml \
    php8.2-xsl \
    php8.2-zip \
    php8.2-curl \
    php8.2-soap \
    php8.2-gmp \
    php8.2-bcmath \
    php8.2-intl \
    php8.2-imap \
    php8.2-phpdbg \
    php8.2-bz2 \
    php8.2-redis \
    php8.2-imagick \
    curl \
    ca-certificates \
    gnupg \
    lsb-release
RUN curl -fsSL https://deb.nodesource.com/setup_19.x | bash -
RUN apt-get install -y nodejs
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN chmod a+r /etc/apt/keyrings/docker.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io


# Download and add the Google Chrome signing key
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

# Add the Google Chrome repository
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/google-chrome.list

# Update apt and install Google Chrome Stable along with libnss3-dev
RUN apt-get update && apt-get install -y google-chrome-stable libnss3-dev libnss3
RUN google-chrome-stable --headless --disable-gpu --remote-debugging-port=9222 --no-sandbox http://localhost &


# composer
ENV COMPOSER_HOME=/composer
ENV PATH=./vendor/bin:/composer/vendor/bin:/root/.yarn/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# mysql client
RUN apt-get install -y mysql-client

# Install PostgreSQL client
RUN apt-get install -y postgresql-client

# git
RUN apt-get install -y git

# node and yarn
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g yarn
RUN composer global require laravel/vapor-cli

# goss
RUN curl -fsSL https://goss.rocks/install | GOSS_VER=v${GOSS_VERSION} sh
