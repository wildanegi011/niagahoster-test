FROM php:8.0.22-fpm-alpine3.16

# Install dev dependencies
RUN apk add --no-cache --virtual .build-deps \
    $PHPIZE_DEPS \
    curl-dev \
    libtool \
    libxml2-dev \
    git \
    curl \
    nano \
    gettext \
    openssl \
    zlib \
    libpng-dev \
    libxml2-dev \
    libxml2-dev \
    libzip-dev

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql exif bcmath gd zip

# Set working directory
WORKDIR /var/www
