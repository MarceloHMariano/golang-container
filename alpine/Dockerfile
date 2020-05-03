FROM alpine:edge

ARG USERNAME=dev
ARG USERGROUP=users

ARG GO_SYS_PATH=/usr/local/go
ARG GO_USER_PATH=/home/$USERNAME/go

RUN \
  # Install packages
  apk add --no-cache \
    bash \
    git \
    go \
    sudo && \
  \
  # Add dev user
  adduser -D -G $USERGROUP $USERNAME && \
  echo 'dev ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/$USERNAME && \
  \
  # Create go path directories
  mkdir -p $GO_SYS_PATH && \
  mkdir -p $GO_USER_PATH && \
  chown -R $USERNAME $GO_USER_PATH

RUN \
  # Install go tools
  export GOPATH=$GO_SYS_PATH && \
  \
  GO111MODULE=on go get golang.org/x/tools/gopls@latest && \
  go get -v github.com/go-delve/delve/cmd/dlv && \
  \
  unset GOPATH

ENV \
  GOPATH=$GO_USER_PATH:$GO_SYS_PATH \
  PATH=$PATH:$GO_SYS_PATH/bin:$GO_USER_PATH/bin

USER $USERNAME
WORKDIR /home/$USERNAME

VOLUME $GO_USER_PATH