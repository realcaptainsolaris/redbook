---
title: Pyenv 
date: 20230123
author: realcaptainsolaris 
---

[pyenv](http://alembic.readthedocs.org/en/latest/) pyenv lets you easily switch between multiple versions of Python. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools.

# Installation

pyenv builds Python from source, which means you’ll need build dependencies to actually use pyenv. The build dependencies vary by platform. If you are on Ubuntu/Debian and want to install the build dependencies, you could use the following:


```bash
sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl

curl https://pyenv.run | bash
```


Das in die `.bashrc` kopieren:

```bash
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

Bash restarten.

## Basic commands 

Liste alle verfügbaren Linux Versionen

```bash
pyenv install --list
```

falls eine Version nicht in der Liste ist, pyenv `updaten`.

```bash
pyenv update 
```

Eine bestimmte Version installieren

```bash
pyenv install 3.11.0 
```

und dann global verfügbar machen:

```bash
pyenv global 3.11.0
```


It will create several files and directories under the selected path, the mos
# References

* [Git](https://github.com/pyenv/pyenv)
* [Realpython](https://realpython.com/intro-to-pyenv)
