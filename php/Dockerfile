from php:fpm 

RUN apt-get update && \
    apt-get install -y git && \
    git clone -b v1.0 https://github.com/dynamofoundation/dyn-web-wallet.git && \
    mv dyn-web-wallet/* . 

COPY bridge.php . 
