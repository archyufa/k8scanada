FROM mysql:5.6

LABEL maintainer "cloudnative@cloudops.com"
LABEL gowebapp-sql "v1"

COPY gowebapp.sql /docker-entrypoint-initdb.d/

