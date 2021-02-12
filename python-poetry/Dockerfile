FROM alpine:latest
# install root programs
RUN apk update && \
    apk add curl \
            g++ \
            python3 \
            shadow
# read local user info from docker --build-arg
ARG USER
ARG UID
ARG GID
# create new user linked to local user
RUN useradd  --create-home --no-log-init $USER
RUN usermod  -u $UID $USER
RUN groupmod -g $GID $USER
# switch to new user
USER $USER
# set workdir to local user home
WORKDIR /home/$USER
# install python poetry
RUN curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python3 -
ENV PATH="/home/$USER/.poetry/bin:$PATH"
