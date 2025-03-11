
潜在样式
=============

Latent Styles

.. tab:: 中文

    潜在样式定义是一种“存根”样式定义，用于指定内置样式的行为（UI 显示）属性。

.. tab:: 英文

    Latent style definitions are a "stub" style definition specifying behavioral
    (UI display) attributes for built-in styles.


潜在样式合集
-----------------------

Latent style collection

.. tab:: 中文

    使用 |Styles| 上的 :attr:`~.Styles.latent_styles` 属性可以访问文档的潜在样式集合::

      >>> latent_styles = document.styles.latent_styles
      >>> latent_styles
      <docx.styles.LatentStyles object at 0x1045dd550>

    **迭代。** |LatentStyles| 应支持按文档顺序迭代所包含的 |_LatentStyle| 对象。

    **潜在样式访问。** 可以使用字典样式表示法按名称访问潜在样式。

    **len()。** |LatentStyles| 支持 :meth:`len`，报告其包含的 |_LatentStyle| 对象的数量。

.. tab:: 英文

    The latent style collection for a document is accessed using the
    :attr:`~.Styles.latent_styles` property on |Styles|::

        >>> latent_styles = document.styles.latent_styles
        >>> latent_styles
        <docx.styles.LatentStyles object at 0x1045dd550>

    **Iteration.** |LatentStyles| should support iteration of contained
    |_LatentStyle| objects in document order.

    **Latent style access.** A latent style can be accessed by name using
    dictionary-style notation.

    **len().** |LatentStyles| supports :meth:`len`, reporting the number of
    |_LatentStyle| objects it contains.


|LatentStyles| 属性
-------------------------

|LatentStyles| properties


默认优先级
~~~~~~~~~~~~~~~~

default_priority

.. tab:: 中文

    **XML 语义**。根据 ISO 29500，如果省略
    `w:defUIPriority` 属性，则默认值为 99。99 在默认 Word `styles.xml` 中明确设置，因此通常就是所找到的值。

    **协议**::

        >>> # 如果省略属性，则返回 None
        >>> latent_styles.default_priority
        None
        >>> # 但预期几乎总是明确为 99
        >>> latent_styles.default_priority
        99
        >>> latent_styles.default_priority = 42
        >>> latent_styles.default_priority
        42

.. tab:: 英文

    **XML semantics**. According to ISO 29500, the default value if the
    `w:defUIPriority` attribute is omitted is 99. 99 is explictly set in the
    default Word `styles.xml`, so will generally be what one finds.

    **Protocol**::

        >>> # return None if attribute is omitted
        >>> latent_styles.default_priority
        None
        >>> # but expect is will almost always be explicitly 99
        >>> latent_styles.default_priority
        99
        >>> latent_styles.default_priority = 42
        >>> latent_styles.default_priority
        42


load_count
~~~~~~~~~~

load_count

.. tab:: 中文

    **XML 语义**。规范中未说明默认值。不允许分配 |None|。

    **协议**::

        >>> latent_styles.load_count
        276
        >>> latent_styles.load_count = 242
        >>> latent_styles.load_count
        242

.. tab:: 英文

    **XML semantics**. No default is stated in the spec. Don't allow assignment of |None|.

    **Protocol**::

        >>> latent_styles.load_count
        276
        >>> latent_styles.load_count = 242
        >>> latent_styles.load_count
        242


Boolean 属性
~~~~~~~~~~~~~~~~~~

Boolean properties

.. tab:: 中文

    有四个布尔属性都共享相同的协议：

    * default_to_hidden
    * default_to_locked
    * default_to_quick_style
    * default_to_unhide_when_used

    **XML 语义**。如果省略该属性，则默认为 |False|。但是，
    该属性应始终在更新时明确写入。

    **协议**::

        >>> latent_styles.default_to_hidden
        False
        >>> latent_styles.default_to_hidden = True
        >>> latent_styles.default_to_hidden
        True

.. tab:: 英文

    There are four boolean properties that all share the same protocol:

    * default_to_hidden
    * default_to_locked
    * default_to_quick_style
    * default_to_unhide_when_used

    **XML semantics**. Defaults to |False| if the attribute is omitted. However,
    the attribute should always be written explicitly on update.

    **Protocol**::

        >>> latent_styles.default_to_hidden
        False
        >>> latent_styles.default_to_hidden = True
        >>> latent_styles.default_to_hidden
        True


XML 例子
~~~~~~~~~~~~

Specimen XML

.. highlight:: xml

.. tab:: 中文

    默认 Word 2011 模板中使用的 `w:latentStyles` 元素::

        <w:latentStyles w:defLockedState="0" w:defUIPriority="99" w:defSemiHidden="1"
                        w:defUnhideWhenUsed="1" w:defQFormat="0" w:count="276">

.. tab:: 英文

    The `w:latentStyles` element used in the default Word 2011 template::

      <w:latentStyles w:defLockedState="0" w:defUIPriority="99" w:defSemiHidden="1"
                      w:defUnhideWhenUsed="1" w:defQFormat="0" w:count="276">


|_LatentStyle| 属性
-------------------------

|_LatentStyle| properties

.. highlight:: python

::

    >>> latent_style = latent_styles.latent_styles[0]

    >>> latent_style.name
    'Normal'

    >>> latent_style.priority
    None
    >>> latent_style.priority = 10
    >>> latent_style.priority
    10

    >>> latent_style.locked
    None
    >>> latent_style.locked = True
    >>> latent_style.locked
    True

    >>> latent_style.quick_style
    None
    >>> latent_style.quick_style = True
    >>> latent_style.quick_style
    True


潜在样式行为
---------------------

Latent style behavior

.. tab:: 中文

    * 样式有两种属性类别，即“行为”和“格式”。
      行为属性指定样式应在用户界面中出现的位置和时间。可以使用 ``<w:latentStyles>`` 元素及其 ``<w:lsdException>`` 子元素为潜在样式指定行为属性。5 种行为属性为：

      + 锁定（locked）
      + uiPriority
      + semiHidden
      + unhideWhenUsed
      + qFormat

    * **已锁定**。“已锁定（ `locked` ）”属性指定样式不应出现在任何列表或图库中，并且不能应用于内容。此行为仅在启用限制格式时有效。

      通过菜单启用锁定：开发人员选项卡 > 保护文档 > 格式限制（仅限 Windows）。

    * **uiPriority**。“uiPriority”属性充当用户界面中样式名称排序的排序键。样式面板和样式库中的列表都受此设置的影响。如果未指定，则其有效值为 0。

    * **semiHidden**。 `semiHidden` 属性会导致样式被排除在推荐列表中。在这种情况下， `semi` 的概念是，虽然样式从推荐列表中隐藏，但它仍出现在“所有样式”列表中。如果还存在设置为 |True| 的 `unhideWhenUsed` 属性，则在首次应用样式时会删除此属性。

    * **unhideWhenUsed**。`unhideWhenUsed` 属性会导致在样式首次应用于内容时删除任何 `semiHidden` 属性。Word 不会仅仅因为文档中存在具有该样式的对象就删除 `semiHidden` 属性。应用样式时，`unhideWhenUsed` 属性不会与 `semiHidden` 属性一起删除。

      `semiHidden` 和 `unhideWhenUsed` 属性组合使用可产生 *hide-until-used* 行为。

      *Hypothesis.* 在首次应用样式时删除 `semiHidden` 属性后，`unhideWhenUsed` 属性的持久性是在样式继承情况下产生适当行为所必需的。

      在这种情况下， `semiHidden` 属性可以明确设置为 |False| 以覆盖继承的值。或者，它可以允许 `semiHidden` 属性稍后重新设置为 |True|，同时保留 hide-until-used 行为。

    * **qFormat**。 `qFormat` 属性指定样式在出现在推荐列表中时是否应出现在样式库中。

      除非样式也出现在推荐列表中，否则它将永远不会出现在库中。

    * 潜在样式属性仅适用于潜在样式。一旦定义了样式，该定义的属性就完全决定了样式的行为；不会从其对应的潜在样式定义继承任何属性。

.. tab:: 英文

    * A style has two categories of attribute, `behavioral` and `formatting`.
      Behavioral attributes specify where and when the style should appear in the
      user interface. Behavioral attributes can be specified for latent styles
      using the ``<w:latentStyles>`` element and its ``<w:lsdException>`` child
      elements. The 5 behavioral attributes are:

      + locked
      + uiPriority
      + semiHidden
      + unhideWhenUsed
      + qFormat

    * **locked**. The `locked` attribute specifies that the style should not
      appear in any list or the gallery and may not be applied to content. This
      behavior is only active when restricted formatting is turned on.

      Locking is turned on via the menu: Developer Tab > Protect Document >
      Formatting Restrictions (Windows only).

    * **uiPriority**. The `uiPriority` attribute acts as a sort key for
      sequencing style names in the user interface. Both the lists in the styles
      panel and the Style Gallery are sensitive to this setting. Its effective
      value is 0 if not specified.

    * **semiHidden**. The `semiHidden` attribute causes the style to be excluded
      from the recommended list. The notion of `semi` in this context is that
      while the style is hidden from the recommended list, it still appears in
      the "All Styles" list. This attribute is removed on first application of
      the style if an `unhideWhenUsed` attribute set |True| is also present.

    * **unhideWhenUsed**. The `unhideWhenUsed` attribute causes any `semiHidden`
      attribute to be removed when the style is first applied to content. Word
      does `not` remove the `semiHidden` attribute just because there exists an
      object in the document having that style. The `unhideWhenUsed` attribute is
      not removed along with the `semiHidden` attribute when the style is
      applied.

      The `semiHidden` and `unhideWhenUsed` attributes operate in combination to
      produce *hide-until-used* behavior.

      *Hypothesis.* The persistance of the `unhideWhenUsed` attribute after
      removing the `semiHidden` attribute on first application of the style is
      necessary to produce appropriate behavior in style inheritance situations.
      In that case, the `semiHidden` attribute may be explictly set to |False| to
      override an inherited value. Or it could allow the `semiHidden` attribute
      to be re-set to |True| later while preserving the hide-until-used behavior.

    * **qFormat**. The `qFormat` attribute specifies whether the style should
      appear in the Style Gallery when it appears in the recommended list.
      A style will never appear in the gallery unless it also appears in the
      recommended list.

    * Latent style attributes are only operative for latent styles. Once a style
      is defined, the attributes of the definition exclusively determine style
      behavior; no attributes are inherited from its corresponding latent style
      definition.


XML 例子
------------

Specimen XML

.. highlight:: xml

::

  <w:latentStyles w:defLockedState="0" w:defUIPriority="99" w:defSemiHidden="1"
                  w:defUnhideWhenUsed="1" w:defQFormat="0" w:count="276">
    <w:lsdException w:name="Normal" w:semiHidden="0" w:uiPriority="0"
                    w:unhideWhenUsed="0" w:qFormat="1"/>
    <w:lsdException w:name="heading 1" w:semiHidden="0" w:uiPriority="9"
                    w:unhideWhenUsed="0" w:qFormat="1"/>
    <w:lsdException w:name="caption" w:uiPriority="35" w:qFormat="1"/>
    <w:lsdException w:name="Default Paragraph Font" w:uiPriority="1"/>
    <w:lsdException w:name="Bibliography" w:uiPriority="37"/>
    <w:lsdException w:name="TOC Heading" w:uiPriority="39" w:qFormat="1"/>
  </w:latentStyles>


Schema 摘录
--------------

Schema excerpt

.. highlight:: xml

::

  <xsd:complexType name="CT_Styles">
    <xsd:sequence>
      <xsd:element name="docDefaults"  type="CT_DocDefaults"  minOccurs="0"/>
      <xsd:element name="latentStyles" type="CT_LatentStyles" minOccurs="0"/>
      <xsd:element name="style"        type="CT_Style"        minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
  </xsd:complexType>

  <xsd:complexType name="CT_LatentStyles">
    <xsd:sequence>
      <xsd:element name="lsdException" type="CT_LsdException" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="defLockedState"    type="s:ST_OnOff"/>
    <xsd:attribute name="defUIPriority"     type="ST_DecimalNumber"/>
    <xsd:attribute name="defSemiHidden"     type="s:ST_OnOff"/>
    <xsd:attribute name="defUnhideWhenUsed" type="s:ST_OnOff"/>
    <xsd:attribute name="defQFormat"        type="s:ST_OnOff"/>
    <xsd:attribute name="count"             type="ST_DecimalNumber"/>
  </xsd:complexType>

  <xsd:complexType name="CT_LsdException">
    <xsd:attribute name="name"           type="s:ST_String"   use="required"/>
    <xsd:attribute name="locked"         type="s:ST_OnOff"/>
    <xsd:attribute name="uiPriority"     type="ST_DecimalNumber"/>
    <xsd:attribute name="semiHidden"     type="s:ST_OnOff"/>
    <xsd:attribute name="unhideWhenUsed" type="s:ST_OnOff"/>
    <xsd:attribute name="qFormat"        type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_OnOff">
    <xsd:attribute name="val" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_String">
    <xsd:attribute name="val" type="s:ST_String" use="required"/>
  </xsd:complexType>

  <xsd:simpleType name="ST_OnOff">
    <xsd:union memberTypes="xsd:boolean ST_OnOff1"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff1">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="on"/>
      <xsd:enumeration value="off"/>
    </xsd:restriction>
  </xsd:simpleType>
