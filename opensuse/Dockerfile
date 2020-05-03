FROM opensuse/tumbleweed

ARG USERNAME=dev
ARG USERGROUP=users

ARG GO_SYS_PATH=/opt/go
ARG GO_USER_PATH=/home/$USERNAME/go

RUN \
  # Setup repositories
  rm -f /etc/zypp/repos.d/* && \
  \
  zypper addrepo -f "http://download.opensuse.org/tumbleweed/repo/oss/" "OSS" && \
  zypper addrepo -f "https://download.opensuse.org/repositories/devel:/languages:/go/openSUSE_Factory/" "Devel:Languages:Go" && \
  \
  # Refresh all repositories
  zypper -n --gpg-auto-import-keys refresh && \
  \
  # Install packages
  zypper -n install --no-recommends \
    git \
    go \
    sudo \
    tar && \
  \
  # Clean zypper cache
  zypper clean -a && \
  \
  # Add dev user
  useradd -m -g users dev && \
  echo 'dev ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/dev && \
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
