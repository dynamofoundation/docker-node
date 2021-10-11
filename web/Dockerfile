from nginx

RUN apt-get update && \
    apt-get install -y git && \
    git clone https://github.com/dynamofoundation/dyn-web-wallet.git && \
    mv dyn-web-wallet/* /usr/share/nginx/html/ 
