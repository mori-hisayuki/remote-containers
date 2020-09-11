FROM node:12.18.2-alpine3.12

ARG USER_NAME
ARG GROUP_NAME
ARG USER_UID
ARG USER_GID

RUN deluser --remove-home node \
    && addgroup -g $USER_GID -S $GROUP_NAME \
    && adduser -u $USER_UID -s /bin/sh -S $USER_NAME $GROUP_NAM
RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN apk --update --no-cache add git curl bash sudo aws-cli openssh-client direnv@testing
RUN echo "$USER_NAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/$USER_NAME

COPY --chown=${GROUP_NAME}:${USER_NAME} ./ssh /home/${USER_NAME}/.ssh
COPY --chown=${GROUP_NAME}:${USER_NAME} ./aws /home/${USER_NAME}/.aws

RUN mkdir /home/$USER_NAME/jamstack-todo-aws \
    && chown -R ${GROUP_NAME}:${USER_NAME} /home/$USER_NAME/jamstack-todo-aws

USER vscode
WORKDIR /home/$USER_NAME/jamstack-todo-aws
RUN git clone -b master git@github.com:mori-hisayuki/jamstack-todo-aws.git /home/$USER_NAME/jamstack-todo-aws \
    && cd /home/${USER_NAME}/jamstack-todo-aws \
    && yarn install