FROM alpine:latest
# install applications
RUN apk update &&  \
    apk add npm

# link local user to docker
ARG USER
ARG UID
ARG GID
# create new user
RUN useradd  --create-home --no-log-init $USER
RUN usermod  -u $UID $USER
RUN groupmod -g $GID $USER
# switch to new user
USER $USER
# set workdir
WORKDIR /home/$USER
