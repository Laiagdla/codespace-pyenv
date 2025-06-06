FROM ubuntu:22.04

# timezone & local
ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
ENV LANG C.UTF-8

# python required packages from https://github.com/docker-library/python python.3.10-slim-bookworm
RUN apt-get update && apt-get install -y \
	git \
	curl \
	dpkg-dev \
	gcc \
	gnupg \
	libbluetooth-dev \
	libbz2-dev \
	libc6-dev \
	libdb-dev \
	libffi-dev \
	libgdbm-dev \
	liblzma-dev \
	libncursesw5-dev \
	libreadline-dev \
	libsqlite3-dev \
	libssl-dev \
	make \
	tk-dev \
	uuid-dev \
	wget \
	xz-utils \
	zlib1g-dev \
	imagemagick \
	jq \
	unzip \
	vim \
	tree \
	zsh \
	direnv \
	gh \
	sudo # Install sudo for the new user

# non-root user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/zsh --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(ALL\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME
ENV HOME /home/$USERNAME

# pyenv
RUN curl https://pyenv.run | bash
ENV PATH $HOME/.pyenv/bin:$HOME/.pyenv/shims:$PATH
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> $HOME/.zshrc && \
	echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> $HOME/.zshrc && \
	echo 'eval "$(pyenv init --path)"' >> $HOME/.zshrc && \
	echo 'eval "$(pyenv init -)"' >> $HOME/.zshrc && \
	echo 'eval "$(pyenv virtualenv-init -)"' >> $HOME/.zshrc

# Python
RUN pyenv install 3.12.9 && \
	pyenv global 3.12.9
ENV PYENV_VERSION 3.12.9

# zsh (Oh My Zsh)
RUN echo 'eval "$(direnv hook zsh)"' >> $HOME/.zshrc
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# pip
RUN python -m ensurepip --upgrade
RUN python -m pip install --upgrade pip

RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh

WORKDIR /workspace