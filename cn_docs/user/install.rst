.. _install:

安装
==========

Installing

.. tab:: 中文

    .. note:: python-docx 0.3.0 及更高版本与早期版本在 API 上不兼容。

    |docx| 托管在 PyPI 上，因此安装相对简单，具体取决于你所安装的安装工具。

    如果你有 `pip`，可以通过以下方式安装 |docx|::

        pip install python-docx

    也可以使用 `easy_install` 来安装 |docx|，不过不推荐这样做::

        easy_install python-docx

    如果既没有 `pip` 也没有 `easy_install`，可以通过从 PyPI 下载发行包、解压 tarball 并运行 ``setup.py`` 来手动安装::

        tar xvzf python-docx-{version}.tar.gz
        cd python-docx-{version}
        python setup.py install

    |docx| 依赖于 ``lxml`` 包。`pip` 和 `easy_install` 都会为你处理这些依赖关系，但如果你使用最后一种方法，则需要自己安装这些依赖包 。

.. tab:: 英文

    .. note:: python-docx versions 0.3.0 and later are not API-compatible with
    prior versions.

    |docx| is hosted on PyPI, so installation is relatively simple, and just depends on what installation utilities you have installed.

    |docx| may be installed with ``pip`` if you have it available::

        pip install python-docx

    |docx| can also be installed using ``easy_install``, although this is discouraged::

        easy_install python-docx

    If neither ``pip`` nor ``easy_install`` is available, it can be installed manually by downloading the distribution from PyPI, unpacking the tarball, and running ``setup.py``::

        tar xvzf python-docx-{version}.tar.gz
        cd python-docx-{version}
        python setup.py install

    |docx| depends on the ``lxml`` package. Both ``pip`` and ``easy_install`` will take care of satisfying those dependencies for you, but if you use this last method you will need to install those yourself.


依赖
------------

Dependencies

* Python 2.6, 2.7, 3.3, or 3.4
* lxml >= 2.3.2
