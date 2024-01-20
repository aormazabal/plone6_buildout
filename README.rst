Plone 6 Buildout
=================

Install dependencies
=====================

Update base linux dependencies:

::

  sudo apt-get update && sudo apt-get upgrade -y

Ubuntu
------

::

  sudo apt-get install -y make build-essential libssl-dev libxml2-dev libxslt1-dev libbz2-dev \
                          libjpeg62-dev libreadline-dev wv poppler-utils wget curl git \
                          zlib1g-dev libsqlite3-dev llvm libncurses5-dev libncursesw5-dev \
                          xz-utils tk-dev libffi-dev liblzma-dev
  sudo pip3 install virtualenv

----

Install pyenv
==============

`pyenv <https://github.com/pyenv/pyenv>`:

::

  exec $SHELL
  curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash
  
  cat >> ~/.bashrc <<'EOF'
  export PATH="$HOME/.pyenv/bin:$PATH"
  eval "$(pyenv init --path)"
  eval "$(pyenv init -)"
  EOF

  source ~/.bashrc

----

Install Python 3.11.2 with pyenv
====================================

Version `Plone 6.0.9 <https://plone.org/download/releases/5.2.11>` is compatible with Python 3.8, 3.9, 3.10, 3.11.

::

  pyenv install -l | egrep '^\s*3\.11\.'
  pyenv install 3.11.2
  pyenv versions
  python3 -V
  pyenv global 3.11.2
  python3 -V

----

Generic settings
=========================

Create share buildout folder for plone

::

  mkdir -p ~/.buildout/{downloads,eggs,extends,zope}
  vim ~/.buildout/default.cfg

Create **default.cfg**:

::

  [buildout]
  download-cache = /home/user_folder/.buildout/download-cache
  eggs-directory = /home/user_folder//.buildout/eggs
  extends-cache = /home/user_folder//.buildout/extends
  zope-directory = /home/user_folder//.buildout/zope
  abi-tag-eggs = true

----

Creating project
=========================

Clone repo

::

    git clone https://github.com/aormazabal/plone6_buildout.git`

--

Rename main folder project
::
    cd ..
    mv plone6_buildout plone609

---

From main folder

`cd plone609`

Creating virtualenv

`virtualenv -p python3.11.2 .`

Install requirements

`pip install -r requirements.txt`

Executing buildout

`buildout -Nv`