FROM golang:latest
LABEL maintainer="NickCiao"

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y curl fzf git jq protobuf-compiler ripgrep shellcheck sudo wget vim zsh \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

USER $USERNAME

# Install Go plugins for protocol buffer compiler
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# Install common Go Tools
RUN go install golang.org/x/tools/gopls@latest
RUN go install github.com/ramya-rao-a/go-outline@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest

# Default powerline10k theme, no plugins installed
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.3/zsh-in-docker.sh)" -- \
  -p z \
  -p fzf \
  -p ripgrep

# TODO:
#   1. p10k configure outputs a `.p10k.zsh`, how to automate this step?
#       a. Read closely: https://github.com/deluan/zsh-in-docker
#   2. What is VSCode's default container?  How do you set this up?
#   3. Expose a port in this file


# docker build --rm . -t devcontainer
# docker run --rm -itd -v %cd%:/devworkspace devcontainer

# Run a container and mount your current working dir into a folder called /devworkspace
# You can list a windows directory directly: e.g. //c/Users/nick/Documents
#   in Powershell: ${PWD}
#   in Linux: $(pwd)
#   in cmd: %cd%
# docker run --rm -it -v %cd%:/devworkspace testdev

CMD ["zsh"]
