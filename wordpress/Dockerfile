FROM debian:jessie

RUN apt-get update && apt-get install -y wget ca-certificates --no-install-recommends && apt-get clean && \
      rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN wget https://wordpress.org/latest.tar.gz && tar zxf latest.tar.gz && rm latest.tar.gz
COPY wp-config.php /wordpress/wp-config.php
RUN echo "<?php" > /wordpress/salt.php
RUN wget -O - https://api.wordpress.org/secret-key/1.1/salt/ >> /wordpress/salt.php

CMD cp -fr wordpress/* /srv/wordpress
