.. _WdOrientation:

``WD_ORIENTATION``
==================

.. tab:: 中文

.. tab:: 英文

alias: **WD_ORIENT**

Specifies the page layout orientation.

Example::

    from docx.enum.section import WD_ORIENT

    section = document.sections[-1]
    section.orientation = WD_ORIENT.LANDSCAPE

----

PORTRAIT
    Portrait orientation.

LANDSCAPE
    Landscape orientation.
