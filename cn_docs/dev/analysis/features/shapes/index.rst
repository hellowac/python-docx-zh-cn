
形状（一般）
===================

Shapes (in general)

.. tab:: 中文

   Word 文档中出现的图形对象称为“形状”。形状可以是“内联”或“浮动”的。内联形状出现在文本基线上，就像字符字形一样，会影响行高。浮动形状出现在文档的任意位置，文本可能会环绕它。可以放置几种类型的形状，包括图片、图表和绘图画布。

   图形对象本身放置在容器中，容器决定图形的位置。通过更改其容器，可以将同一图形对象内联或浮动。图形本身不受影响。

   除了此概述之外，还有以下更专业的功能分析：

.. tab:: 英文

   A graphical object that appears in a Word document is known as a `shape`. A shape can be `inline` or `floating`. An inline shape appears on a text baseline as though it were a character glyph and affects the line height. A floating shape appears at an arbitrary location on the document and text may wrap around it. Several types of shape can be placed, including a picture, a chart, and a drawing canvas.

   The graphical object itself is placed in a container, and it is the container that determines the placement of the graphic. The same graphical object can be placed inline or floating by changing its container. The graphic itself is unaffected.

   In addition to this overview, there are the following more specialized feature analyses:

.. toctree::
   :titlesonly:

   shapes-inline
   shapes-inline-size
   picture


MS API
------

MS API

.. tab:: 中文

   通过 Document 对象上的 Shapes 和 InlineShapes 属性可以访问形状。

   浮动形状的 API 与内联形状的 API 重叠，但存在很大差异。以下是两者共有的一些属性：

   * 填充
   * 发光
   * HasChart
   * HasSmartArt
   * 高度
   * 阴影
   * 超链接
   * PictureFormat（提供亮度、颜色、裁剪、透明度、对比度）
   * 类型（图表、LockedCanvas、图片、SmartArt 等）
   * 宽度

.. tab:: 英文

   Access to shapes is provided by the Shapes and InlineShapes properties on the Document object.

   The API for a floating shape overlaps that for an inline shapes, but there are substantial differences. The following properties are some of those common to both:

   * Fill
   * Glow
   * HasChart
   * HasSmartArt
   * Height
   * Shadow
   * Hyperlink
   * PictureFormat (providing brightness, color, crop, transparency, contrast)
   * Type (Chart, LockedCanvas, Picture, SmartArt, etc.)
   * Width


资源
---------

Resources

* `Document Members (Word) on MSDN`_
* `InlineShape Members (Word) on MSDN`_
* `InlineShapes Members (Word) on MSDN`_
* `Shape Members (Word) on MSDN`_

.. _Document Members (Word) on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff840898.aspx

.. _InlineShape Members (Word) on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff840794.aspx

.. _InlineShapes Members (Word) on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff836984.aspx

.. _Shape Members (Word) on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff195191.aspx
