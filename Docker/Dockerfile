FROM python:2.7-alpine3.7
ENV MYSQL_USERNAME="db_user"
ENV MYSQL_PASSWORD="password"
ENV MYSQL_INSTANCE_NAME="my_db"
ENV MYSQL_PORT_3306_TCP_ADDR="mysql-service"
ENV MYSQL_PORT_3306_TCP_PORT="3306"
COPY . /app
WORKDIR /app
RUN pip2.7 install --upgrade pip
RUN apk add --update mysql-dev py-configobj libusb py-pip python-dev gcc linux-headers libc-dev
RUN pip2.7 install -r requirements.txt
#RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 3000
CMD [ "python2.7", "application.py" ]
