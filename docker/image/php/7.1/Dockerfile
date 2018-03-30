FROM php:7.1-fpm-alpine
MAINTAINER minhpq331@gmail.com

RUN apk add --update \
		autoconf \
		g++ \
		libtool \
		make \

	&& docker-php-ext-install mbstring \
	&& docker-php-ext-install mysqli \
	&& docker-php-ext-install pdo_mysql \
	&& docker-php-ext-install opcache \
	&& docker-php-ext-install pcntl \

	&& apk add --update icu-dev \
	&& docker-php-ext-install intl \

	&& apk add --update postgresql-dev \
	&& docker-php-ext-install pgsql \
	&& apk del \
		postgresql-libs \
		libsasl \
		db \

	&& docker-php-ext-install sockets \

	&& touch /usr/local/etc/php/bogus.ini \
	&& pear config-set php_ini /usr/local/etc/php/bogus.ini \
	&& pecl config-set php_ini /usr/local/etc/php/bogus.ini \
	&& apk add --update \
		libevent-dev \
		openssl-dev \
	&& pecl install event \
	&& docker-php-ext-enable event \
	&& mv /usr/local/etc/php/conf.d/docker-php-ext-event.ini \
		/usr/local/etc/php/conf.d/docker-php-ext-zz-event.ini \
	&& rm /usr/local/etc/php/bogus.ini \

	&& pecl install redis \
	&& docker-php-ext-enable redis.so \
	
	&& apk add --update \
		gmp-dev \
	&& docker-php-ext-configure gmp \
	&& docker-php-ext-install gmp \

	# Install mcrypt
	&& ( \
		apk add \
			--no-cache \
			libmcrypt-dev \
			libltdl \
		&& docker-php-ext-configure mcrypt \
			--with-mcrypt \
		&& docker-php-ext-install  mcrypt \
	) \

	# Install GD
	&& ( \
		apk add \
			--no-cache \
			freetype \
			libpng \
			libjpeg-turbo \
			freetype-dev \
			libpng-dev \
			libjpeg-turbo-dev\
		&& docker-php-ext-configure gd \
			--with-gd \
			--with-freetype-dir=/usr/include/ \
			--with-png-dir=/usr/include/ \
			--with-jpeg-dir=/usr/include/ \

		&& docker-php-ext-install gd \
		&& apk del \
			--no-cache \
			freetype-dev \
			libpng-dev \
			libjpeg-turbo-dev \
	) \

	&& apk del \
		autoconf \
		binutils \
		binutils-libs \
		db \
		expat \
		file \
		g++ \
		gcc \
		gdbm \
		gmp \
		isl \
		libatomic \
		libbz2 \
		libc-dev \
		libffi \
		libgcc \
		libgomp \
		libldap \
		libmagic \
		libsasl \
		libstdc++ \
		libtool \
		m4 \
		make \
		mpc1 \
		mpfr3 \
		musl-dev \
		perl \
		pkgconf \
		pkgconfig \
		python \
		re2c \
		readline \
		sqlite-libs \
		zlib-dev \
&& rm -rf /tmp/* /var/cache/apk/*