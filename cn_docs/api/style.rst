
.. _style_api:

样式相关对象
=====================

Style-related objects

.. tab:: 中文

   样式用于将一组格式属性集中到一个名称下，并一次性将这些属性应用于内容对象。这可以提高整个文档以及相关文档的格式一致性，并允许通过更改相应样式中的定义来全局更改格式。

.. tab:: 英文

   A style is used to collect a set of formatting properties under a single name and apply those properties to a content object all at once. This promotes formatting consistency throughout a document and across related documents and allows formatting changes to be made globally by changing the definition in the appropriate style.


|Styles| 对象
----------------

|Styles| objects

.. currentmodule:: docx.styles.styles

.. autoclass:: Styles()
   :members:
   :inherited-members:
   :exclude-members:
       get_by_id, get_style_id, part


|BaseStyle| 对象
-------------------

|BaseStyle| objects

.. currentmodule:: docx.styles.style

.. autoclass:: BaseStyle()
   :members:
   :inherited-members:
   :exclude-members:
       part, style_id


|CharacterStyle| 对象
-------------------------

|CharacterStyle| objects

.. autoclass:: CharacterStyle()
   :show-inheritance:
   :members:
   :inherited-members:
   :exclude-members:
       element, part, style_id, type


|ParagraphStyle| 对象
-------------------------

|ParagraphStyle| objects

.. autoclass:: ParagraphStyle()
   :show-inheritance:
   :members:
   :inherited-members:
   :exclude-members:
       element, part, style_id, type


|_TableStyle| 对象
---------------------

|_TableStyle| objects

.. autoclass:: _TableStyle()
   :show-inheritance:
   :members:
   :inherited-members:
   :exclude-members:
       element, part, style_id, type


|_NumberingStyle| 对象
-------------------------

|_NumberingStyle| objects

.. autoclass:: _NumberingStyle()
   :members:


|LatentStyles| 对象
----------------------

|LatentStyles| objects

.. currentmodule:: docx.styles.latent

.. autoclass:: LatentStyles()
   :members:
   :inherited-members:
   :exclude-members:
       part


|_LatentStyle| 对象
----------------------

|_LatentStyle| objects

.. autoclass:: _LatentStyle()
   :members:
   :inherited-members:
   :exclude-members:
       part
