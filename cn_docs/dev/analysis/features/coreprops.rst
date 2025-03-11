
核心文档属性
========================

Core Document Properties

.. tab:: 中文

    Open XML 格式提供了一组与每个文档一起维护的描述性属性。其中之一是 *核心文件属性* 。核心属性是所有 Open XML 格式所共有的，并出现在文档、演示文稿和电子表格文件中。核心文档属性中的 “核心” 指的是 `Dublin Core`_ ，这是一种元数据标准，它定义了一组用于描述资源的核心元素。

    核心属性在 ISO/IEC 29500 规范第 2 部分第 11 节中进行了描述。|docx| 中某些核心属性的名称与规范中的名称不同，以符合 MS API。

    其他属性（如公司名称）是自定义属性，保存在“app.xml”中。

.. tab:: 英文

    The Open XML format provides for a set of descriptive properties to be maintained with each document. One of these is the *core file properties*. The core properties are common to all Open XML formats and appear in document, presentation, and spreadsheet files. The 'Core' in core document properties refers to `Dublin Core`_, a metadata standard that defines a core set of elements to describe resources.

    The core properties are described in Part 2 of the ISO/IEC 29500 spec, in Section 11. The names of some core properties in |docx| are changed from those in the spec to conform to the MS API.

    Other properties such as company name are custom properties, held in ``app.xml``.


候选协议
------------------

Candidate Protocol

::

    >>> document = Document()
    >>> core_properties = document.core_properties
    >>> core_properties.author
    'python-docx'
    >>> core_properties.author = 'Brian'
    >>> core_properties.author
    'Brian'


属性
----------

Properties

.. tab:: 中文

    支持 15 个属性。所有 unicode 值都限制为 255 个字符（不是字节）。

    作者 *(unicode)*
        注意：在规范中命名为“creator”。主要负责制作资源内容的实体。（都柏林核心）

    类别 *(unicode)*
        此包内容的分类。此属性的示例值可能包括：简历、信函、财务预测、提案、技术演示等。（开放包装约定）

    评论 *(unicode)*
        注意：在规范中命名为“description”。资源内容的说明。值可能包括摘要、目录、对内容图形表示的引用以及内容的自由文本说明。（都柏林核心）

    content_status *(unicode)*
        内容的状态。值可能包括“草稿”、“已审核”和“最终版”。 （开放包装惯例）

    created *(datetime)*
        资源的创建日期。（都柏林核心）

    identifier *(unicode)*
        在给定上下文中对资源的明确引用。（都柏林核心）

    keywords *(unicode)*
        一组分隔的关键字，用于支持搜索和索引。这通常是属性中其他地方不可用的术语列表。（开放包装惯例）

    language *(unicode)*
        资源知识内容的语言。（都柏林核心）

    last_modified_by *(unicode)*
        执行最后修改的用户。标识是特定于环境的。示例包括姓名、电子邮件地址或员工 ID。建议此值尽可能简洁。（开放包装惯例）

    last_printed *(datetime)*
        最后打印的日期和时间。（开放包装惯例）

    modified *(datetime)*
        资源更改的日期。 （都柏林核心）

    修订 *（整数）*
        修订号。此值可能表示保存或修订的次数，前提是应用程序在每次修订后都会更新它。（开放打包约定）

    主题 *（unicode）*
        资源内容的主题。（都柏林核心）

    标题 *（unicode）*
        为资源指定的名称。（都柏林核心）

    版本 *（unicode）*
        版本指示符。此值由用户或应用程序设置。（开放打包约定）

.. tab:: 英文

    15 properties are supported. All unicode values are limited to 255 characters (not bytes).

    author *(unicode)*
        Note: named 'creator' in spec. An entity primarily responsible for making the content of the resource. (Dublin Core)

    category *(unicode)*
        A categorization of the content of this package. Example values for this property might include: Resume, Letter, Financial Forecast, Proposal, Technical Presentation, and so on. (Open Packaging Conventions)

    comments *(unicode)*
        Note: named 'description' in spec. An explanation of the content of the resource. Values might include an abstract, table of contents, reference to a graphical representation of content, and a free-text account of the content. (Dublin Core)

    content_status *(unicode)*
        The status of the content. Values might include “Draft”, “Reviewed”, and “Final”. (Open Packaging Conventions)

    created *(datetime)*
        Date of creation of the resource. (Dublin Core)

    identifier *(unicode)*
        An unambiguous reference to the resource within a given context. (Dublin Core)

    keywords *(unicode)*
        A delimited set of keywords to support searching and indexing. This is typically a list of terms that are not available elsewhere in the properties. (Open Packaging Conventions)

    language *(unicode)*
        The language of the intellectual content of the resource. (Dublin Core)

    last_modified_by *(unicode)*
        The user who performed the last modification. The identification is environment-specific. Examples include a name, email address, or employee ID. It is recommended that this value be as concise as possible. (Open Packaging Conventions)

    last_printed *(datetime)*
        The date and time of the last printing. (Open Packaging Conventions)

    modified *(datetime)*
        Date on which the resource was changed. (Dublin Core)

    revision *(int)*
        The revision number. This value might indicate the number of saves or revisions, provided the application updates it after each revision. (Open Packaging Conventions)

    subject *(unicode)*
        The topic of the content of the resource. (Dublin Core)

    title *(unicode)*
        The name given to the resource. (Dublin Core)

    version *(unicode)*
        The version designator. This value is set by the user or by the application. (Open Packaging Conventions)


样本 XML
------------

Specimen XML

.. tab:: 中文

    Microsoft Word 生成的 core.xml

.. tab:: 英文

  core.xml produced by Microsoft Word

.. highlight:: xml

::

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <cp:coreProperties
        xmlns:cp="http://schemas.openxmlformats.org/package/2006/metadata/core-properties"
        xmlns:dc="http://purl.org/dc/elements/1.1/"
        xmlns:dcterms="http://purl.org/dc/terms/"
        xmlns:dcmitype="http://purl.org/dc/dcmitype/"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <dc:title>Core Document Properties Exploration</dc:title>
      <dc:subject>PowerPoint core document properties</dc:subject>
      <dc:creator>Steve Canny</dc:creator>
      <cp:keywords>powerpoint; open xml; dublin core; microsoft office</cp:keywords>
      <dc:description>
        One thing I'd like to discover is just how line wrapping is handled
        in the comments. This paragraph is all on a single
        line._x000d__x000d_This is a second paragraph separated from the
        first by two line feeds.
      </dc:description>
      <cp:lastModifiedBy>Steve Canny</cp:lastModifiedBy>
      <cp:revision>2</cp:revision>
      <dcterms:created xsi:type="dcterms:W3CDTF">2013-04-06T06:03:36Z</dcterms:created>
      <dcterms:modified xsi:type="dcterms:W3CDTF">2013-06-15T06:09:18Z</dcterms:modified>
      <cp:category>analysis</cp:category>
    </cp:coreProperties>


架构摘录
--------------

Schema Excerpt

::

    <xs:schema
      targetNamespace="http://schemas.openxmlformats.org/package/2006/metadata/core-properties"
      xmlns="http://schemas.openxmlformats.org/package/2006/metadata/core-properties"
      xmlns:xs="http://www.w3.org/2001/XMLSchema"
      xmlns:dc="http://purl.org/dc/elements/1.1/"
      xmlns:dcterms="http://purl.org/dc/terms/"
      elementFormDefault="qualified"
      blockDefault="#all">

      <xs:import
        namespace="http://purl.org/dc/elements/1.1/"
        schemaLocation="http://dublincore.org/schemas/xmls/qdc/2003/04/02/dc.xsd"/>
      <xs:import
        namespace="http://purl.org/dc/terms/"
        schemaLocation="http://dublincore.org/schemas/xmls/qdc/2003/04/02/dcterms.xsd"/>
      <xs:import
        id="xml"
        namespace="http://www.w3.org/XML/1998/namespace"/>

      <xs:element name="coreProperties" type="CT_CoreProperties"/>

      <xs:complexType name="CT_CoreProperties">
        <xs:all>
          <xs:element name="category"        type="xs:string"   minOccurs="0"/>
          <xs:element name="contentStatus"   type="xs:string"   minOccurs="0"/>
          <xs:element ref="dcterms:created"                     minOccurs="0"/>
          <xs:element ref="dc:creator"                          minOccurs="0"/>
          <xs:element ref="dc:description"                      minOccurs="0"/>
          <xs:element ref="dc:identifier"                       minOccurs="0"/>
          <xs:element name="keywords"        type="CT_Keywords" minOccurs="0"/>
          <xs:element ref="dc:language"                         minOccurs="0"/>
          <xs:element name="lastModifiedBy"  type="xs:string"   minOccurs="0"/>
          <xs:element name="lastPrinted"     type="xs:dateTime" minOccurs="0"/>
          <xs:element ref="dcterms:modified"                    minOccurs="0"/>
          <xs:element name="revision"        type="xs:string"   minOccurs="0"/>
          <xs:element ref="dc:subject"                          minOccurs="0"/>
          <xs:element ref="dc:title"                            minOccurs="0"/>
          <xs:element name="version"         type="xs:string"   minOccurs="0"/>
        </xs:all>
      </xs:complexType>

      <xs:complexType name="CT_Keywords" mixed="true">
        <xs:sequence>
          <xs:element name="value" minOccurs="0" maxOccurs="unbounded" type="CT_Keyword"/>
        </xs:sequence>
        <xs:attribute ref="xml:lang" use="optional"/>
      </xs:complexType>

      <xs:complexType name="CT_Keyword">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute ref="xml:lang" use="optional"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>

    </xs:schema>


.. _Dublin Core:
   http://en.wikipedia.org/wiki/Dublin_Core
