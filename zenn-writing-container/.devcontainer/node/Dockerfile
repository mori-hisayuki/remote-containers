FROM node:12.18.2-alpine3.12

ARG USER_NAME
ARG GROUP_NAME
ARG USER_UID
ARG USER_GID

RUN deluser --remove-home node \
    && addgroup -g $USER_GID -S $GROUP_NAME \
    && adduser -u $USER_UID -s /bin/sh -S $USER_NAME $GROUP_NAM
RUN apk --update --no-cache add git curl bash sudo

COPY --chown=${GROUP_NAME}:${USER_NAME} ./ssh /home/${USER_NAME}/.ssh

RUN npm install -gzenn-cli

RUN mkdir /home/$USER_NAME/zenn-writing \
    && chown -R ${GROUP_NAME}:${USER_NAME} /home/$USER_NAME/zenn-writing

USER vscode
WORKDIR /home/$USER_NAME/zenn-writing