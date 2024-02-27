FROM python:3.6-alpine

LABEL MAINTAINER AHMED DAMOU 

WORKDIR /opt

RUN pip install flask

COPY . . 

VOLUME /opt


EXPOSE 8080

ENV ODOO_URL="https://www.odoo.com/"

ENV PGADMIN_URL="https://www.pgadmin.org/"

CMD [ "python", "./app.py" ]
