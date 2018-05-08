Web Applications, A to Z
========================

Welcome to the supporting materials repository for Moshe's PyCon 2018
tutorial,
"Web Applications, A to Z".

Installing
----------

You definitely want to install Python 3.6 and Docker.
There are many ways to install those,
depending on your operating system.
However, it is easy to check that it is working:

.. code::

    $ python3

Should run and give you indication that it is Python 3.6.

.. code::

    $ docker images
    
Note that on some UNIX systems, Docker is installed with access limited to the :code:`docker` group.
If you get a permission denied message,
add your user to the docker group

.. code::

    $ sudo usermod -a -G docker $USER
    
 Log out, and then log back in -- and your :code:`docker images` should work now.
    

Should run and show some images
(an empty list is fine if you just installed it).

Some installation methods will not put Python 3.6 on your path.
This is fine,
as long as you know how to invoke it.

If you are on Windows, you also want the `build tools`_.
Download and install them.

.. _build tools: https://www.visualstudio.com/downloads/#build-tools-for-visual-studio-2017

DevPI
-----

Install and set up DevPI.
There are several ways to do that.
If you are looking for the simplest,
in a fresh virtual environment, run the following:

.. code::

  $ pip install devpi
  $ devpi-server --init
  $ devpi-server 

Then point :code:`pip` to it by editing :code:`$HOME/.pip/pip.conf` (Linux or MAc) or :code:`$HOME/pip/pip.ini` (Windows).

.. code::

    # $HOME/.pip/pip.conf
    [global]
    index-url = http://localhost:3141/root/pypi/+simple/

Warm up DevPI:

.. code::

    $ python3.6 -m venv /tmp/my-env
    $ /tmp/my-env/bin/pip install pyramid twisted sqlalchemy

Disconnect your laptop from the network.


.. code::

    $ python3.6 -m venv /tmp/my-env2
    $ /tmp/my-env2/bin/pip install --no-cache-dir incremental
    $ /tmp/my-env2/bin/pip install --no-cache-dir pyramid twisted sqlalchemy

If the second succeeds,
this means your laptop can install packages when disconnected.

Docker Cache
============

We also want to warm up your Docker build cache.

.. code::

    $ docker build -f naive.docker .
    $ docker build -f multistage.docker .
    $ docker build -f selenium.docker .

Please note all these commands have a period, :code:`.` at the end.
When copying and pasting the command,
or retyping it,
make sure to not miss it!

Since Docker caches layers,
this will make sure at least the naive and selenium builds will work,
even if you change your code,
without the network.
