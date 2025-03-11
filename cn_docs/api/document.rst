
.. _document_api:

文档对象
================

Document objects

.. tab:: 中文

   主要文档和相关对象。

.. tab:: 英文

   The main Document and related objects.


|Document| 构造函数
----------------------

|Document| constructor

.. autofunction:: docx.Document


|Document| 对象
------------------

|Document| objects

.. autoclass:: docx.document.Document()
   :members:
   :exclude-members: styles_part


|CoreProperties| 对象
------------------------

|CoreProperties| objects-

.. tab:: 中文

   每个 |Document| 对象都通过其 :attr:`core_properties` 属性提供对其 |CoreProperties| 对象的访问。|CoreProperties| 对象提供对文档所谓的 *核心属性* 的读/写访问。核心属性包括作者、类别、评论、content_status、创建、标识符、关键字、语言、上次修改者、上次打印、修改、修订、主题、标题和版本。

   每个属性都是三种类型之一：|str|、|datetime| 或 |int|。字符串属性的长度限制为 255 个字符，如果未设置，则返回空字符串 ('')。日期属性被分配并返回为不带时区的 |datetime| 对象，即 UTC。任何时区转换都是客户的责任。如果未设置，日期属性将返回 |None|。

   |docx| 除了向没有核心属性部分的演示文稿添加核心属性部分（非常罕见）外，不会自动设置任何文档核心属性。如果 |docx| 添加核心属性部分，则它包含 title、last_modified_by、revision 和 modified 属性的默认值。如果需要该行为，客户端代码应该更新 revision 和 last_modified_by 等属性。

.. tab:: 英文

   Each |Document| object provides access to its |CoreProperties| object via its :attr:`core_properties` attribute. A |CoreProperties| object provides read/write access to the so-called *core properties* for the document. The core properties are author, category, comments, content_status, created, identifier, keywords, language, last_modified_by, last_printed, modified, revision, subject, title, and version.

   Each property is one of three types, |str|, |datetime|, or |int|. String properties are limited in length to 255 characters and return an empty string ('') if not set. Date properties are assigned and returned as |datetime| objects without timezone, i.e. in UTC. Any timezone conversions are the responsibility of the client. Date properties return |None| if not set.

   |docx| does not automatically set any of the document core properties other than to add a core properties part to a presentation that doesn't have one (very uncommon). If |docx| adds a core properties part, it contains default values for the title, last_modified_by, revision, and modified properties. Client code should update properties like revision and last_modified_by if that behavior is desired.

.. currentmodule:: docx.opc.coreprops

.. class:: CoreProperties

   .. attribute:: author

      `string` -- An entity primarily responsible for making the content of the
      resource.

   .. attribute:: category

      `string` -- A categorization of the content of this package. Example
      values might include: Resume, Letter, Financial Forecast, Proposal,
      or Technical Presentation.

   .. attribute:: comments

      `string` -- An account of the content of the resource.

   .. attribute:: content_status

      `string` -- completion status of the document, e.g. 'draft'

   .. attribute:: created

      `datetime` -- time of intial creation of the document

   .. attribute:: identifier

      `string` -- An unambiguous reference to the resource within a given
      context, e.g. ISBN.

   .. attribute:: keywords

      `string` -- descriptive words or short phrases likely to be used as
      search terms for this document

   .. attribute:: language

      `string` -- language the document is written in

   .. attribute:: last_modified_by

      `string` -- name or other identifier (such as email address) of person
      who last modified the document

   .. attribute:: last_printed

      `datetime` -- time the document was last printed

   .. attribute:: modified

      `datetime` -- time the document was last modified

   .. attribute:: revision

      `int` -- number of this revision, incremented by Word each time the
      document is saved. Note however |docx| does not automatically increment
      the revision number when it saves a document.

   .. attribute:: subject

      `string` -- The topic of the content of the resource.

   .. attribute:: title

      `string` -- The name given to the resource.

   .. attribute:: version

      `string` -- free-form version string
