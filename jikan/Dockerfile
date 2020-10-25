FROM php:7.3-apache

ENV COMPOSER_ALLOW_SUPERUSER 1

RUN apt-get update && apt-get install -y \
    curl \
    git \
    unzip \
  && apt-get clean && rm -rf /var/lib/apt/lists/* \
  && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.16 \
  && composer --version \
  && a2enmod rewrite \
  && service apache2 restart \
  && git clone https://github.com/jikan-me/jikan-rest.git . \
  && cp .env.dist .env \
  && sed -i "s/GITHUB_REPORTING=.*/GITHUB_REPORTING=false/" .env \
  && sed -i "s/REDIS_HOST=.*/REDIS_HOST=jikan-redis/" .env \
  && composer install --prefer-dist --no-progress --classmap-authoritative  --no-interaction \
  && composer update jikan-me/jikan

ADD run-jikan.sh ./

ENTRYPOINT ["./run-jikan.sh"]
