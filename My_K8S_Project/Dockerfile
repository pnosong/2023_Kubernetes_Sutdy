FROM ubuntu

LABEL maintainer="pnosong"

RUN apt-get update\
    && apt-get upgrade -y\
    && apt-get install vim git apache2 -y

ADD ./board.html /var/www/html/board.html

WORKDIR /var/www/html
EXPOSE 80

CMD [ "-D","FOREGROUND" ]
ENTRYPOINT [ "apachectl" ]