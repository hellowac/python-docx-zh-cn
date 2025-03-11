.. _documents:

处理文档
==========================

Working with Documents

.. tab:: 中文

    |docx| 允许您创建新文档以及对现有文档进行更改。实际上，它只允许您对现有文档进行更改；只是如果您从没有任何内容的文档开始，一开始可能会感觉像是从头开始创建。

    这个特性非常强大。文档的外观很大程度上取决于删除所有内容后剩下的部分。样式和页眉和页脚等内容与主要内容分开包含，允许您在起始文档中进行大量自定义，然后这些自定义内容将显示在您生成的文档中。

    让我们逐个示例介绍创建文档的步骤，从您可以对文档执行的两个主要操作开始，打开它并保存它。

.. tab:: 英文

    |docx| allows you to create new documents as well as make changes to existing
    ones. Actually, it only lets you make changes to existing documents; it's just
    that if you start with a document that doesn't have any content, it might feel
    at first like you're creating one from scratch.

    This characteristic is a powerful one. A lot of how a document looks is
    determined by the parts that are left when you delete all the content. Things
    like styles and page headers and footers are contained separately from the main
    content, allowing you to place a good deal of customization in your starting
    document that then appears in the document you produce.

    Let's walk through the steps to create a document one example at a time,
    starting with two of the main things you can do with a document, open it and
    save it.


打开文档
------------------

Opening a document

.. tab:: 中文

    最简单的入门方法是打开一个新文档，而不指定要打开的文件::

        from docx import Document

        document = Document()
        document.save('test.docx')

    这将从内置默认模板创建一个新文档，并将其不加更改地保存到名为 'test.docx' 的文件中。所谓的“默认模板”实际上只是一个没有内容的 Word 文件，与已安装的 |docx| 包一起存储。它与选择 Word 的 **文件 > 从模板新建...** 菜单项后选择 *Word 文档* 模板大致相同。

.. tab:: 英文

    The simplest way to get started is to open a new document without specifying
    a file to open::

        from docx import Document

        document = Document()
        document.save('test.docx')

    This creates a new document from the built-in default template and saves it
    unchanged to a file named 'test.docx'. The so-called "default template" is
    actually just a Word file having no content, stored with the installed |docx|
    package. It's roughly the same as you get by picking the *Word Document*
    template after selecting Word's **File > New from Template...** menu item.


真正打开文档
-------------------------

REALLY opening a document

.. tab:: 中文

    如果您想要对最终文档有更多控制权，或者想要更改现有文档，则需要打开一个文件名为::

      document = Document('existing-document-file.docx')
      document.save('new-file-name.docx')

    注意事项：

    * 您可以通过这种方式打开任何 Word 2007 或更高版本的文件（Word 2003 及更早版本的 .doc 文件不起作用）。虽然您可能还无法操作所有内容，但其中已有的内容都可以正常加载和保存。功能集仍在构建中，因此您还无法添加或更改诸如页眉或脚注之类的内容，但如果文档中有这些内容，|docx| 会礼貌地保留它们，并且足够聪明，可以在不真正理解它们是什么的情况下保存它们。

    * 如果您使用相同的文件名打开和保存文件，|docx| 将乖乖地覆盖原始文件，而不会发出任何警告。你要确保这就是你想要的。

.. tab:: 英文

    If you want more control over the final document, or if you want to change an
    existing document, you need to open one with a filename::

        document = Document('existing-document-file.docx')
        document.save('new-file-name.docx')

    Things to note:

    * You can open any Word 2007 or later file this way (.doc files from Word 2003
      and earlier won't work). While you might not be able to manipulate all the
      contents yet, whatever is already in there will load and save just fine. The
      feature set is still being built out, so you can't add or change things like
      headers or footnotes yet, but if the document has them |docx| is polite
      enough to leave them alone and smart enough to save them without actually
      understanding what they are.

    * If you use the same filename to open and save the file, |docx| will obediently
      overwrite the original file without a peep. You'll want to make sure that's
      what you intend.


打开“类似文件”的文档
------------------------------

Opening a 'file-like' document

.. tab:: 中文

    |docx| 可以从所谓的 *类文件* 对象打开文档。它还可以
    保存到类文件对象。当您想要通过网络连接或从数据库获取源
    或目标文档，并且不想（或不允许）与文件系统交互时，这会非常方便。实际上，这意味着
    您可以传递打开的文件或 StringIO/BytesIO 流对象来打开或保存
    文档，如下所示::

        f = open('foobar.docx', 'rb')
        document = Document(f)
        f.close()

        # 或

        with open('foobar.docx', 'rb') as f:
        source_stream = StringIO(f.read())
        document = Document(source_stream)
        source_stream.close()
        ...
        target_stream = StringIO()
        document.save(target_stream)

    并非所有操作系统都需要 ``'rb'`` 文件打开模式参数。它默认为 ``'r'`` ，有时这已经足够了，但 Windows 和至少某些版本的 Linux 需要 'b' （选择二进制模式）才能允许 Zipfile 打开文件。

    好的，您已经打开了一个文档，并且非常确定您可以稍后将其保存在某个地方。下一步是将一些内容放入其中...

.. tab:: 英文

    |docx| can open a document from a so-called *file-like* object. It can also
    save to a file-like object. This can be handy when you want to get the source
    or target document over a network connection or from a database and don't want
    to (or aren't allowed to) interact with the file system. In practice this means
    you can pass an open file or StringIO/BytesIO stream object to open or save
    a document like so::

        f = open('foobar.docx', 'rb')
        document = Document(f)
        f.close()

        # or

        with open('foobar.docx', 'rb') as f:
            source_stream = StringIO(f.read())
        document = Document(source_stream)
        source_stream.close()
        ...
        target_stream = StringIO()
        document.save(target_stream)

    The ``'rb'`` file open mode parameter isn't required on all operating
    systems. It defaults to ``'r'`` which is enough sometimes, but the 'b'
    (selecting binary mode) is required on Windows and at least some versions of
    Linux to allow Zipfile to open the file.

    Okay, so you've got a document open and are pretty sure you can save it
    somewhere later. Next step is to get some content in there ...
