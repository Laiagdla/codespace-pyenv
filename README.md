# Codespaces with pyenv!
Codespaces devcontainer setup with pyenv instead of conda.
Baseimage Ubuntu 22.04
Based on python 3.10-slim-bookworm dokerhub image

# devcontainers on this image
Choose python 3.10 or python 3.12 to use clean installations without any pip packages installed

python3.12-minimal contains this packages [requirements.txt](https://gist.githubusercontent.com/krokrob53ab953bbec16c96b9938fcaebf2b199/raw/9035bbf12922840905ef1fbbabc459dc565b79a3/minimal_requirements.txt)
python3.12-lewagon contains this packages [requirements.txt](https://raw.githubusercontent.com/lewagon/data-setup/master/specs/releases/linux.txt")

If you want to modify python version edit docker file pyenv installation lines.
copy .devcontainer into your own repository to make it Codespaces ready without conda and with a pyenv enviroment.