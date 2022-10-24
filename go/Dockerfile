FROM golang:latest
LABEL maintainer="NickCiao"

RUN apt-get update && \
apt-get install -y bash curl fzf git jq protobuf-compiler ripgrep shellcheck sudo vim zsh

# Install Go plugins for protocol buffer compiler
RUN go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
RUN go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

# Install common Go Tools
RUN go install golang.org/x/tools/gopls@latest
RUN go install github.com/ramya-rao-a/go-outline@latest
RUN go install github.com/go-delve/delve/cmd/dlv@latest

# Default powerline10k theme, no plugins installed
RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.3/zsh-in-docker.sh)" -- \
  -t powerlevel10k/powerlevel10k
  -p z \
  -p fzf \
  -p ripgrep


# docker build --rm . -t devcontainer
# docker run --rm -itd -v %cd%:/devworkspace devcontainer

# Run a container and mount your current working dir into a folder called /devworkspace
# You can list a windows directory directly: e.g. //c/Users/nick/Documents
#   in Powershell: ${PWD}
#   in Linux: $(pwd)
#   in cmd: %cd%
# docker run --rm -it -v %cd%:/devworkspace testdev

CMD ["zsh"]
