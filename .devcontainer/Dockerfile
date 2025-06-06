FROM ubuntu:22.04

RUN apt-get update && apt-get install -y \
    git \
    curl \
    build-essential \
    libssl-dev \
    zlib1g-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    llvm \
    libncurses5-dev \
    libncursesw5-dev \
    xz-utils \
    tk-dev \
    libffi-dev \
    liblzma-dev \
    python-openssl \
    zsh

RUN curl https://pyenv.run | bash
ENV PATH /root/.pyenv/bin:$PATH

RUN echo 'eval "$(pyenv init --path)"' >> /root/.bashrc && \
    echo 'eval "$(pyenv virtualenv-init -)"' >> /root/.bashrc

RUN pyenv install 3.10.6 && \
    pyenv global 3.10.6

ENV PYENV_VERSION 3.10.6

RUN apt-get install -y direnv
RUN echo 'eval "$(direnv hook zsh)"' >> /root/.zshrc

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended
RUN chsh -s $(which zsh)

RUN pip install --upgrade pip && \
    pip install -r requirements.txt

RUN apt-get install -y wget && \
    wget -O- https://aka.ms/install-vscode-server/setup.sh | sh

WORKDIR /workspace
