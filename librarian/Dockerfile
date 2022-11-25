FROM python:3.9-buster

ARG UID=1000
ARG GID=1000
ARG USERNAME=librarian
ARG GROUPNAME=librarian

RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID $USERNAME

RUN mkdir -p /opt/app
RUN chown -R $USERNAME:$GROUPNAME /opt/app

USER $USERNAME
WORKDIR /opt/app

RUN pip install twine wheel
COPY .pypirc /home/$USERNAME/

ENTRYPOINT /bin/bash