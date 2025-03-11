
.. _shared_api:

共享类
==============

Shared classes

.. currentmodule:: docx.shared


长度对象
--------------

Length objects

.. tab:: 中文

   |docx| 中的长度值表示为标准化的 |Length| 值对象。|Length| 是 |int| 的子类，具有 |int| 的所有行为。此外，它还具有内置单位转换属性，例如::

      >>> inline_shape.height
      914400
      >>> inline_shape.height.inches
      1.0

   长度对象是使用一系列便捷构造函数构造的，允许以最适合上下文的单位表示值。

.. tab:: 英文

   Length values in |docx| are expressed as a standardized |Length| value object. |Length| is a subclass of |int|, having all the behavior of an |int|. In addition, it has built-in units conversion properties, e.g.::

      >>> inline_shape.height
      914400
      >>> inline_shape.height.inches
      1.0

   Length objects are constructed using a selection of convenience constructors, allowing values to be expressed in the units most appropriate to the context.

.. autoclass:: Length
   :members:
   :member-order: bysource

.. autoclass:: Inches
   :members:

.. autoclass:: Cm
   :members:

.. autoclass:: Mm
   :members:

.. autoclass:: Pt
   :members:

.. autoclass:: Twips
   :members:

.. autoclass:: Emu
   :members:


|RGBColor| 对象
------------------

|RGBColor| objects

.. tab:: 中文

.. tab:: 英文

.. autoclass:: RGBColor(r, g, b)
   :members:
   :undoc-members:

   `r`, `g`, and `b` are each an integer in the range 0-255 inclusive. Using
   the hexidecimal integer notation, e.g. `0x42` may enhance readability
   where hex RGB values are in use::

       >>> lavender = RGBColor(0xff, 0x99, 0xcc)
