ARG TARGET_PHP_VERSION=7.2
FROM php:${TARGET_PHP_VERSION}-apache

COPY ./code /var/www/html
RUN chown -R www-data:www-data /var/www

COPY ./.docker/.shared/scripts/ /tmp/scripts/
RUN chmod +x -R /tmp/scripts/

# set timezone
ARG TZ=UTC
RUN /tmp/scripts/set_timezone.sh ${TZ}

RUN /tmp/scripts/install_php_extensions.sh

RUN /tmp/scripts/install_software.sh

RUN /tmp/scripts/cleanup.sh
