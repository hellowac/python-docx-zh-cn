
.. _shape_api:

与形状相关的对象
=====================

Shape-related objects

.. tab:: 中文

.. tab:: 英文

.. currentmodule:: docx.shape


|InlineShapes| 对象
----------------------

|InlineShapes| objects

.. autoclass:: InlineShapes
   :members:
   :exclude-members: add_picture


|InlineShape| 对象
---------------------

|InlineShape| objects

.. tab:: 中文

   |InlineShape| 的 ``width`` 和 ``height`` 属性提供了一个长度对象，它是 |Length| 的一个实例。这些实例的行为类似于 int，但还具有内置单位转换属性，例如

.. tab:: 英文

   The ``width`` and ``height`` property of |InlineShape| provide a length object that is an instance of |Length|. These instances behave like an int, but also have built-in units conversion properties, e.g.

::

    >>> inline_shape.height
    914400
    >>> inline_shape.height.inches
    1.0

.. autoclass:: InlineShape
   :members: height, type, width
