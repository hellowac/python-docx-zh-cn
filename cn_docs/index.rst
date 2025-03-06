
python-docx
===========


.. tab:: 中文

    发布于 v\ |version| (:ref:`Installation <install>`)

    *python-docx* 是一个用于创建和更新 Microsoft Word (.docx) 文件的 Python 库。

.. tab:: 英文

    Release v\ |version| (:ref:`Installation <install>`)

    *python-docx* is a Python library for creating and updating Microsoft Word (.docx) files.


它可以做什么
--------------

What it can do

.. |img| image:: /_static/img/example-docx-01.png

.. tab:: 中文

    以下是 |docx| 功能的一个示例：

.. tab:: 英文

    Here's an example of what |docx| can do:

============================================  ===============================================================
|img|                                         ::

                                                from docx import Document
                                                from docx.shared import Inches

                                                document = Document()

                                                document.add_heading('Document Title', 0)

                                                p = document.add_paragraph('A plain paragraph having some ')
                                                p.add_run('bold').bold = True
                                                p.add_run(' and some ')
                                                p.add_run('italic.').italic = True

                                                document.add_heading('Heading, level 1', level=1)
                                                document.add_paragraph('Intense quote', style='Intense Quote')

                                                document.add_paragraph(
                                                    'first item in unordered list', style='List Bullet'
                                                )
                                                document.add_paragraph(
                                                    'first item in ordered list', style='List Number'
                                                )

                                                document.add_picture('monty-truth.png', width=Inches(1.25))

                                                records = (
                                                    (3, '101', 'Spam'),
                                                    (7, '422', 'Eggs'),
                                                    (4, '631', 'Spam, spam, eggs, and spam')
                                                )

                                                table = document.add_table(rows=1, cols=3)
                                                hdr_cells = table.rows[0].cells
                                                hdr_cells[0].text = 'Qty'
                                                hdr_cells[1].text = 'Id'
                                                hdr_cells[2].text = 'Desc'
                                                for qty, id, desc in records:
                                                    row_cells = table.add_row().cells
                                                    row_cells[0].text = str(qty)
                                                    row_cells[1].text = id
                                                    row_cells[2].text = desc

                                                document.add_page_break()

                                                document.save('demo.docx')
============================================  ===============================================================


.. toctree::
   :maxdepth: 1
   :caption: 用户指南 / User Guide

   user/install
   user/quickstart
   user/documents
   user/tables
   user/text
   user/sections
   user/hdrftr
   user/api-concepts
   user/styles-understanding
   user/styles-using
   user/shapes

.. toctree::
   :maxdepth: 2
   :caption: API 文档 / API Documentation

   api/document
   api/settings
   api/style
   api/text
   api/table
   api/section
   api/shape
   api/dml
   api/shared
   api/enum/index

.. toctree::
   :maxdepth: 1
   :caption: 贡献指南 / Contributor Guide

   dev/analysis/index
