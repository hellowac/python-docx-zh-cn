
.. _text_api:

文本相关对象
====================

Text-related objects

.. tab:: 中文

.. tab:: 英文


|Paragraph| 对象
-------------------

|Paragraph| objects

.. autoclass:: docx.text.paragraph.Paragraph()
   :members:


|ParagraphFormat| 对象
-------------------------

|ParagraphFormat| objects

.. autoclass:: docx.text.parfmt.ParagraphFormat()
   :members:


|Hyperlink| 对象
-------------------

|Hyperlink| objects

.. autoclass:: docx.text.hyperlink.Hyperlink()
   :members:


|Run| 对象
-------------

|Run| objects

.. autoclass:: docx.text.run.Run()
   :members:


|Font| 对象
--------------

|Font| objects

.. autoclass:: docx.text.run.Font()
   :members:


|RenderedPageBreak| 对象
---------------------------

|RenderedPageBreak| objects

.. autoclass:: docx.text.pagebreak.RenderedPageBreak()
   :members:


|TabStop| 对象
-----------------

|TabStop| objects

.. autoclass:: docx.text.tabstops.TabStop()
   :members:


|TabStops| 对象
------------------

|TabStops| objects

.. autoclass:: docx.text.tabstops.TabStops()
   :members: clear_all

   .. automethod:: docx.text.tabstops.TabStops.add_tab_stop(position, alignment=WD_TAB_ALIGNMENT.LEFT, leader=WD_TAB_LEADER.SPACES)
