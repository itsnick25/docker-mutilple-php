FROM php:8.2-apache

RUN apt-get update && apt-get install -y \
    apache2-utils \
    libapache2-mod-fcgid \
    curl \
    ca-certificates \
    && update-ca-certificates \
    && chmod 644 /etc/ssl/certs/ca-certificates.crt \
    && rm -rf /var/lib/apt/lists/*

# Enable necessary Apache modules
RUN a2enmod proxy_fcgi setenvif rewrite proxy proxy_http ssl headers

# Copy SSL certificates
COPY certs/apache-selfsigned.crt /etc/apache2/ssl/apache-selfsigned.crt
COPY certs/apache-selfsigned.key /etc/apache2/ssl/apache-selfsigned.key

# Copy updated Virtual Host configuration
COPY vhost.conf /etc/apache2/sites-enabled/000-default.conf

EXPOSE 80 443

CMD ["apachectl", "-D", "FOREGROUND"]
