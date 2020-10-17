FROM node:12.18.2-alpine3.12

ARG USER_NAME
ARG GROUP_NAME
ARG USER_UID
ARG USER_GID

RUN deluser --remove-home node \
    && addgroup -g $USER_GID -S $GROUP_NAME \
    && adduser -u $USER_UID -s /bin/sh -S $USER_NAME $GROUP_NAM
RUN apk --update --no-cache add git curl bash sudo openssh-client

COPY --chown=${GROUP_NAME}:${USER_NAME} ./ssh /home/${USER_NAME}/.ssh

RUN npm install -g zenn-cli@latest

RUN mkdir /home/$USER_NAME/zenn-writing \
    && chown -R ${GROUP_NAME}:${USER_NAME} /home/$USER_NAME/contents

USER $USER_NAME
WORKDIR /home/$USER_NAME/zenn-writing
RUN git clone git@github.com:mori-hisayuki/zenn-content.git /home/$USER_NAME/contents