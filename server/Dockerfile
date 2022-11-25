FROM pypiserver/pypiserver:latest

COPY .htpasswd /

ENTRYPOINT /entrypoint.sh -P /.htpasswd