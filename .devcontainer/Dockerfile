FROM ubuntu:22.04

# timezone
ENV TZ=UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# python required packages from https://github.com/docker-library/python python.3.10-slim-bookworm 
RUN apt-get update
RUN apt-get install -y \
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
	gh

# pyenv
RUN curl https://pyenv.run | bash
ENV PATH /root/.pyenv/bin:/root/.pyenv/shims:$PATH
RUN echo 'export PYENV_ROOT="$HOME/.pyenv"' >> /root/.zshrc && \
	echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> /root/.zshrc && \
	echo 'eval "$(pyenv init --path)"' >> /root/.zshrc && \
	echo 'eval "$(pyenv init -)"' >> /root/.zshrc && \
	echo 'eval "$(pyenv virtualenv-init -)"' >> /root/.zshrc

# Python
RUN pyenv install 3.10.6 && \
	pyenv global 3.10.6
ENV PYENV_VERSION 3.10.6

# zsh
RUN echo 'eval "$(direnv hook zsh)"' >> /root/.zshrc
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
RUN chsh -s $(which zsh)

# pip
RUN python -m ensurepip --upgrade
RUN python -m pip install --upgrade pip

# vscode
RUN wget -O- https://aka.ms/install-vscode-server/setup.sh | sh

WORKDIR /workspace
