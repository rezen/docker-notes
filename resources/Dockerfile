FROM php:latest
RUN apt-get  update && apt-get install -y  libcurl4-openssl-dev pkg-config libssl-dev
RUN pecl channel-update pecl.php.net && pecl install mongodb
RUN mkdir -p /var/www/html && cd /var/www/html && echo '<?php echo "Howdy, I am whaley glad you are here!!!";' > index.php 
WORKDIR /var/www/html
CMD ["php", "-S", "0.0.0.0:8008"]
