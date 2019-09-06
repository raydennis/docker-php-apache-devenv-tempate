ARG TARGET_PHP_VERSION=7.2
FROM php:${TARGET_PHP_VERSION}-apache

COPY ./.docker/.shared/scripts/ /tmp/scripts/
RUN chmod +x -R /tmp/scripts/

# set timezone
ARG TZ=UTC
RUN /tmp/scripts/set_timezone.sh ${TZ}

RUN /tmp/scripts/install_php_extensions.sh

RUN /tmp/scripts/cleanup.sh

ENV APACHE_DOCUMENT_ROOT /var/www/html/public

RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

COPY ./src /var/www/html
RUN chown -R www-data:www-data /var/www
