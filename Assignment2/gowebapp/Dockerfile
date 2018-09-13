FROM golang

LABEL maintainer "cloudnative@cloudops.com"
LABEL gowebapp "v1"

EXPOSE 80

ENV GOPATH=/go

COPY /code $GOPATH/src/gowebapp/

WORKDIR $GOPATH/src/gowebapp/

RUN go get && go install

ENTRYPOINT $GOPATH/bin/gowebapp

