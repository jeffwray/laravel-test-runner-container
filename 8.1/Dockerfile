FROM ubuntu:20.04
LABEL maintainer="Jeff Wray <jwray@mobilozophy.com>"
ARG DEBIAN_FRONTEND=noninteractive

ENV GOSS_VERSION="0.3.6"

# Install basic utilities and dependencies
RUN apt-get update && apt-get install -y software-properties-common curl wget
RUN add-apt-repository ppa:ondrej/php -y
RUN add-apt-repository ppa:git-core/ppa -y
RUN apt-get update -y

# Install PHP 8.1 and required extensions
RUN apt-get install -y \
    unzip \
    php8.1-cli \
    php8.1-gd \
    php8.1-ldap \
    php8.1-mbstring \
    php8.1-mysql \
    php8.1-pgsql \
    php8.1-sqlite3 \
    php8.1-xml \
    php8.1-xsl \
    php8.1-zip \
    php8.1-curl \
    php8.1-soap \
    php8.1-gmp \
    php8.1-bcmath \
    php8.1-intl \
    php8.1-imap \
    php8.1-phpdbg \
    php8.1-bz2 \
    php8.1-redis \
    php8.1-imagick \
    curl \
    ca-certificates \
    gnupg \
    lsb-release

# Install latest stable Node.js & npm
RUN curl -fsSL https://deb.nodesource.com/setup_current.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g npm@latest yarn

# Install Docker CLI
RUN mkdir -p /etc/apt/keyrings
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
RUN chmod a+r /etc/apt/keyrings/docker.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
RUN apt-get update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

# Install Composer
ENV COMPOSER_HOME=/composer
ENV PATH=./vendor/bin:/composer/vendor/bin:/root/.yarn/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install MySQL & PostgreSQL clients
RUN apt-get install -y mysql-client postgresql-client

# Install Git
RUN apt-get install -y git

# Install Laravel Vapor CLI
RUN composer global require laravel/vapor-cli

# Install Goss for testing
RUN curl -fsSL https://goss.rocks/install | GOSS_VER=v${GOSS_VERSION} sh