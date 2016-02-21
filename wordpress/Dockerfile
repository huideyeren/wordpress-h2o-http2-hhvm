FROM debian:jessie

RUN apt-get update && apt-get install -y wget ca-certificates --no-install-recommends && apt-get clean && \
      rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN wget https://wordpress.org/wordpress-4.4.2.tar.gz && tar zxf wordpress-4.4.2.tar.gz && rm wordpress-4.4.2.tar.gz
COPY wp-config.php /wordpress/wp-config.php
RUN echo "<?php" > /wordpress/salt.php
RUN wget -O - https://api.wordpress.org/secret-key/1.1/salt/ >> /wordpress/salt.php

CMD cp -fr wordpress/* /srv/wordpress
