
段落样式
===============

Paragraph Style

.. tab:: 中文

    段落样式提供字符格式（字体）以及段落格式属性。字符格式继承自 |_CharacterStyle|，主要体现在 :attr:`font` 属性中。同样，大多数段落特定属性来自 :attr:`paragraph_format` 属性上可用的 |ParagraphFormat| 对象。

    少数其他属性特定于段落样式。

.. tab:: 英文

    A paragraph style provides character formatting (font) as well as paragraph formatting properties. Character formatting is inherited from |_CharacterStyle| and is predominantly embodied in the :attr:`font` property. Likewise, most paragraph-specific properties come from the |ParagraphFormat| object available on the :attr:`paragraph_format` property.

    A handful of other properties are specific to a paragraph style.


下一段落样式
--------------------

next_paragraph_style

.. tab:: 中文

    `next_paragraph_style` 属性可用于访问 Word 自动为插入在具有此样式的段落后的新段落指定的样式。此属性对于通常只在序列中出现一次的样式（如标题）最有用。

    默认对插入的段落使用相同的样式。这解决了最常见的情况；例如，具有 `Body Text` 样式的正文段落后面通常会跟着一个具有相同样式的段落。

.. tab:: 英文

    The `next_paragraph_style` property provides access to the style that will automatically be assigned by Word to a new paragraph inserted after a paragraph with this style. This property is most useful for a style that would normally appear only once in a sequence, such as a heading.

    The default is to use the same style for an inserted paragraph. This addresses the most common case; for example, a body paragraph having `Body Text` style would normally be followed by a paragraph of the same style.


预期用途
~~~~~~~~~~~~~~

Expected usage

.. tab:: 中文

    此属性的优先用例是提供可分配给段落的工作样式。该属性将始终提供有效的段落样式，当无法确定更具体的样式时，默认为当前样式。

    虽然这掩盖了 API 中某些情况的细节，但它解决了预期的最常见用例。例如，需要检测缺失样式的开发人员可以轻松使用 oxml 层来检查 XML，如果这些用例比预期的更常见，则可以添加更多功能。

.. tab:: 英文

    The priority use case for this property is to provide a working style that can be assigned to a paragraph. The property will always provide a valid paragraph style, defaulting to the current style whenever a more specific one cannot be determined.

    While this obscures some specifics of the situation from the API, it addresses the expected most common use case. Developers needing to detect, for example, missing styles can readily use the oxml layer to inspect the XML and further features can be added if those use cases turn out to be more common than expected.


行为
~~~~~~~~

Behavior

.. tab:: 中文

    **默认。** 默认的下一个段落样式是相同的段落样式。

    每当下一个段落样式未指定或无效时，将使用默认值，包括以下情况：

    * 不存在 `w​​:next` 子元素
    * 文档中不存在 `w​​:next/@w:val` 中指定的 styleId 样式。
    * `w:next/@w:val` 中指定的样式不是段落样式。

    在所有这些情况下，都会返回当前样式 (`self`)。

.. tab:: 英文

    **Default.** The default next paragraph style is the same paragraph style.

    The default is used whenever the next paragraph style is not specified or is invalid, including these conditions:

    * No `w:next` child element is present
    * A style having the styleId specified in `w:next/@w:val` is not present in the document.
    * The style specified in `w:next/@w:val` is not a paragraph style.

    In all these cases the current style (`self`) is returned.


XML 例子
~~~~~~~~~~~

Example XML

.. tab:: 中文

.. tab:: 英文

.. highlight:: xml

paragraph_style.next_paragraph_style is styles['Bar']::

  <w:style w:type="paragraph" w:styleId="Foo">
    <w:name w:val="Foo"/>
    <w:next w:val="Bar"/>
  </w:style>

**Semantics.** The `w:next` child element is optional.

* When omitted, the next style is the same as the current style.
* If no style with a matching styleId exists, the `w:next` element is ignored
  and the next style is the same as the current style.
* If a style is found but is of a style type other than paragraph, the
  `w:next` element is ignored and the next style is the same as the current
  style.


候选协议
~~~~~~~~~~~~~~~~~~

Candidate protocol

.. tab:: 中文

.. tab:: 英文

.. highlight:: python

::

    >>> styles = document.styles

    >>> paragraph_style = styles['Foo']
    >>> paragraph_style.next_paragraph_style == paragraph_style
    True

    >>> paragraph_style.next_paragraph_style = styles['Bar']
    >>> paragraph_style.next_paragraph_style == styles['Bar']
    True

    >>> paragraph_style.next_paragraph_style = None
    >>> paragraph_style.next_paragraph_style == paragraph_style
    True


Schema 摘要
--------------

Schema excerpt

.. highlight:: xml

::

  <xsd:complexType name="CT_Style">
    <xsd:sequence>
      <xsd:element name="name"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="aliases"         type="CT_String"        minOccurs="0"/>
      <xsd:element name="basedOn"         type="CT_String"        minOccurs="0"/>
      <xsd:element name="next"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="link"            type="CT_String"        minOccurs="0"/>
      <xsd:element name="autoRedefine"    type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="hidden"          type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="uiPriority"      type="CT_DecimalNumber" minOccurs="0"/>
      <xsd:element name="semiHidden"      type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="unhideWhenUsed"  type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="qFormat"         type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="locked"          type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personal"        type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personalCompose" type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="personalReply"   type="CT_OnOff"         minOccurs="0"/>
      <xsd:element name="rsid"            type="CT_LongHexNumber" minOccurs="0"/>
      <xsd:element name="pPr"             type="CT_PPrGeneral"    minOccurs="0"/>
      <xsd:element name="rPr"             type="CT_RPr"           minOccurs="0"/>
      <xsd:element name="tblPr"           type="CT_TblPrBase"     minOccurs="0"/>
      <xsd:element name="trPr"            type="CT_TrPr"          minOccurs="0"/>
      <xsd:element name="tcPr"            type="CT_TcPr"          minOccurs="0"/>
      <xsd:element name="tblStylePr"      type="CT_TblStylePr"    minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="type"        type="ST_StyleType"/>
    <xsd:attribute name="styleId"     type="s:ST_String"/>
    <xsd:attribute name="default"     type="s:ST_OnOff"/>
    <xsd:attribute name="customStyle" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_String">
    <xsd:attribute name="val" type="s:ST_String" use="required"/>
  </xsd:complexType>
