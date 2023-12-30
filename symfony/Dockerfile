FROM php:8.3-cli

LABEL org.opencontainers.image.source=https://github.com/JAGFx/environements
LABEL org.opencontainers.image.licenses=MIT

ENV GIT_CONFIG_EMAIL=plop@unicorn.stars
ENV GIT_CONFIG_FULLNAME=Unicorn

COPY php.ini /usr/local/etc/php/conf.d/docker-php-config.ini

RUN apt update -y \
    && apt upgrade -y \
    && apt full-upgrade -y \
    && apt dist-upgrade -y \
    && apt autoremove -y \
    && apt install zip unzip libzip-dev libpq-dev apt-transport-https -y

RUN docker-php-ext-install zip pdo pgsql pdo_mysql pdo_pgsql

COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

RUN apt install curl git -y \
    && curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | bash \
    && apt install symfony-cli -y \
    && curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - \
    && apt install nodejs -y

WORKDIR /home/cli/

RUN git config --global user.email "$GIT_CONFIG_EMAIL" \
    && git config --global user.name "$GIT_CONFIG_FULLNAME"

