FROM php:7.4.14-fpm
WORKDIR /var/www
COPY --from=composer /usr/bin/composer /usr/bin/composer
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN echo "export PATH=\"$HOME/.symfony/bin:$PATH\"" > ~/.bashrc
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
CMD ["php-fpm"]
EXPOSE 9000