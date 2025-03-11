
API 基础知识
============

API basics

.. tab:: 中文

    |docx| 的 API 旨在使简单的事情变得简单，同时允许通过适度和渐进的理解投入实现更复杂的结果。

    仅使用一个对象即可创建基本文档，即打开文件时返回的 |api-Document| 对象。

    |api-Document| 上的方法允许将 *块级* 对象添加到文档末尾。块级对象包括段落、内联图片和表格。

    标题、项目符号和编号列表只是应用了特定样式的段落。

    通过这种方式，可以从上到下“编写”文档，大致就像一个人如果确切知道自己想说什么一样。这种基本用例（内容始终添加到文档末尾）预计占实际用例的 80%，因此，在不影响整体 API 功能的情况下，使其尽可能简单是当务之急。

.. tab:: 英文

    The API for |docx| is designed to make doing simple things simple, while
    allowing more complex results to be achieved with a modest and incremental
    investment of understanding.

    It's possible to create a basic document using only a single object, the
    |api-Document| object returned when opening a file. The methods on
    |api-Document| allow *block-level* objects to be added to the end of the
    document. Block-level objects include paragraphs, inline pictures, and tables.
    Headings, bullets, and numbered lists are simply paragraphs with a particular
    style applied.

    In this way, a document can be "written" from top to bottom, roughly like
    a person would if they knew exactly what they wanted to say This basic use
    case, where content is always added to the end of the document, is expected to
    account for perhaps 80% of actual use cases, so it's a priority to make it as
    simple as possible without compromising the power of the overall API.


内联对象
--------------

Inline objects

.. tab:: 中文

    |api-Document| 上的每个块级方法（例如 ``add_paragraph()``）都会返回
    创建的块级对象。通常不需要引用；但是当
    必须单独创建内联对象时，您将需要块项
    引用来执行此操作。

    ... 随着 API 的完善，在此处添加示例...

.. tab:: 英文

    Each block-level method on |api-Document|, such as ``add_paragraph()``, returns
    the block-level object created. Often the reference is unneeded; but when
    inline objects must be created individually, you'll need the block-item
    reference to do it.

    ... add example here as API solidifies ...
