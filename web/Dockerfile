from nginx

RUN apt-get update && \
    apt-get install -y git && \
    git clone https://github.com/dynamofoundation/dyn-web-wallet.git && \
    mkdir -p /var/www/html && \
    #mv dyn-web-wallet/* /usr/share/nginx/html/ 
    mv dyn-web-wallet/* /var/www/html/ 

#COPY bridge.php /usr/share/nginx/html/
COPY bridge.php /var/www/html/
COPY site.conf /etc/nginx/conf.d/default.conf
