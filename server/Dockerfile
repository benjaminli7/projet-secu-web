FROM alpine:latest

COPY ./html html
COPY ./db.sqlite db.sqlite
COPY ./server.py server.py

RUN apk update

RUN apk add python3 py3-pip

RUN pip3 install flask pyjwt pysqlite3

CMD ["python3", "server.py"]
