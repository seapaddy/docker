FROM alpine:latest

# install dependencies
RUN apk update && \
    apk add autoconf \
            automake \
            bat \
            build-base \
            clang-dev \
            cmake \
            coreutils \
            curl \
            fzf \
            g++ \
            gettext-tiny-dev \
            git \
            libtool \
            make \
            p7zip \
            pkgconf \
            python3 \
            ripgrep \
            shadow \
            the_silver_searcher \
            tmux \
            unzip \
            wget \
            zsh

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

# create required directories
RUN mkdir -p .config/nvim/ \
             .config/tmux/ \
             .config/zsh/ \
             .local/bin/ \
             .local/share/

# install neovim
RUN git clone "https://github.com/neovim/neovim.git" .cache/neovim
WORKDIR /home/$USER/.cache/neovim
RUN make CMAKE_BUILD_TYPE=Release \
    CMAKE_EXTRA_FLAGS="-DCMAKE_INSTALL_PREFIX=$HOME/.local/share/neovim" && \
    make install
ENV PATH="/home/$USER/.local/share/neovim/bin:$PATH"

WORKDIR /home/$USER/.local/bin
# install clangd
RUN wget 'https://github.com/clangd/clangd/releases/download/11.0.0/clangd-linux-11.0.0.zip'
RUN 7z x clangd-linux-11.0.0.zip && \
    rm -rf clangd-linux-11.0.0.zip

WORKDIR /home/$USER
RUN echo 'export PATH="$HOME/.local/share/neovim/bin:$PATH"'  > .zshrc && \
    echo 'export PCNAME="docker"'                            >> .zshrc && \
    echo 'source $HOME/.config/zsh/.zshrc'                   >> .zshrc
