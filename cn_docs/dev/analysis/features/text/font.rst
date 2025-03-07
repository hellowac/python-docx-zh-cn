
字体
====

Font

.. tab:: 中文

    Word 支持丰富多样的字符格式设置。字符格式设置可以在 *样式层次结构* 中的不同级别上应用。在最低级别，它可以直接应用于文本内容的某个运行（run）。在此之上，它可以应用于字符、段落和表格样式。它还可以应用于抽象编号定义。在最高级别，它可以通过主题或文档默认设置来应用。

.. tab:: 英文

    Word supports a rich variety of character formatting. Character formatting
    can be applied at various levels in the *style hierarchy*. At the lowest
    level, it can be applied directly to a run of text content. Above that, it
    can be applied to character, paragraph and table styles. It can also be
    applied to an abstract numbering definition. At the highest levels it can be
    applied via a theme or document defaults.


字体名称
-------------

Typeface name

.. tab:: 中文

    Word 允许在单个文本运行中为字符内容指定多个字体。这允许在单个运行中使用不同的 Unicode 字符范围，例如 ASCII 和阿拉伯文，每个字符范围都可以使用为该范围指定的字体。

    最多可以为字体指定八种不同的字体。四个用于指定不同代码点范围的字体。这些是：

    * `w:ascii` - 用于前 128 个 Unicode 代码点
    * `w:cs` - 用于复杂脚本代码点
    * `w:eastAsia` - 用于东亚代码点
    * `w:hAnsi` - 代表 *高 ANSI*，但实际上是用于任何没有被其他三种属性指定的代码点的通用设置。

    另外四个，`w:asciiTheme`、`w:csTheme`、`w:eastAsiaTheme` 和 `w:hAnsiTheme`，用于间接指定主题定义的字体。这允许在文档中集中设置字体。这四个属性的优先级低于前四个，因此例如，如果同时存在 `w:ascii` 属性，则 `w:asciiTheme` 的值会被忽略。

    用于文本运行的字体名称在 `w:rPr/w:rFonts` 元素中指定。共有 8 个属性，结合起来可以指定要使用的字体。

.. tab:: 英文

    Word allows multiple typefaces to be specified for character content in
    a single run. This allows different Unicode character ranges such as ASCII
    and Arabic to be used in a single run, each being rendered in the typeface
    specified for that range.

    Up to eight distinct typefaces may be specified for a font. Four are used to
    specify a typeface for a distinct code point range. These are:

    * `w:ascii` - used for the first 128 Unicode code points
    * `w:cs` - used for complex script code points
    * `w:eastAsia` - used for East Asian code points
    * `w:hAnsi` - standing for *high ANSI*, but effectively the catch-all for any
      code points not specified by one of the other three.

    The other four, `w:asciiTheme`, `w:csTheme`, `w:eastAsiaTheme`, and
    `w:hAnsiTheme` are used to indirectly specify a theme-defined font. This
    allows the typeface to be set centrally in the document. These four attributes
    have lower precedence than the first four, so for example the value of
    `w:asciiTheme` is ignored if a `w:ascii` attribute is also present.

    The typeface name used for a run is specified in the `w:rPr/w:rFonts`
    element. There are 8 attributes that in combination specify the typeface to
    be used.

协议
~~~~~~~~

Protocol

.. tab:: 中文

    最初，API 仅支持基础字体名称，通过 :attr:`~.Font.name` 属性。它的值是 `w:rFonts/@w:ascii` 属性的值，或者如果不存在，则为 |None|。赋值给此属性会将 `w:ascii` 和 `w:hAnsi` 属性都设置为分配的字符串，或者如果分配了 |None|，则移除这两个属性::

        >>> font = document.styles['Normal'].font
        >>> font.name
        None
        >>> font.name = 'Arial'
        >>> font.name
        'Arial'


.. tab:: 英文

    Initially, only the base typeface name is supported by the API, using the
    :attr:`~.Font.name` property. Its value is the that of the `w:rFonts/@w:ascii`
    attribute or |None| if not present. Assignment to this property sets both the
    `w:ascii` and the `w:hAnsi` attribute to the assigned string or removes them
    both if |None| is assigned::

        >>> font = document.styles['Normal'].font
        >>> font.name
        None
        >>> font.name = 'Arial'
        >>> font.name
        'Arial'


布尔运行属性
----------------------

Boolean run properties

.. tab:: 中文

    字符格式化属性是开关类型的，例如粗体、斜体和小型大写字母。某些属性是 *切换属性*，如果它们在样式层次结构中出现多次，可能会相互抵消。有关切换属性的更多细节，请参见 §17.7.3。它们不会影响此处指定的 API。

    以下运行属性是布尔（三级状态）属性：

    +-----------------+------------+-------------------------------------------+
    | 元素            | 规范       | 名称                                      |
    +=================+============+===========================================+
    | `<b/>`          | §17.3.2.1  | 粗体                                      |
    +-----------------+------------+-------------------------------------------+
    | `<bCs/>`        | §17.3.2.2  | 复杂脚本粗体                              |
    +-----------------+------------+-------------------------------------------+
    | `<caps/>`       | §17.3.2.5  | 显示所有字符为大写字母                    |
    +-----------------+------------+-------------------------------------------+
    | `<cs/>`         | §17.3.2.7  | 在运行中使用复杂脚本格式                  |
    +-----------------+------------+-------------------------------------------+
    | `<dstrike/>`    | §17.3.2.9  | 双重删除线                                |
    +-----------------+------------+-------------------------------------------+
    | `<emboss/>`     | §17.3.2.13 | 浮雕效果                                  |
    +-----------------+------------+-------------------------------------------+
    | `<i/>`          | §17.3.2.16 | 斜体                                      |
    +-----------------+------------+-------------------------------------------+
    | `<iCs/>`        | §17.3.2.17 | 复杂脚本斜体                              |
    +-----------------+------------+-------------------------------------------+
    | `<imprint/>`    | §17.3.2.18 | 压印效果                                  |
    +-----------------+------------+-------------------------------------------+
    | `<noProof/>`    | §17.3.2.21 | 不检查拼写或语法                          |
    +-----------------+------------+-------------------------------------------+
    | `<oMath/>`      | §17.3.2.22 | Office Open XML 数学公式                  |
    +-----------------+------------+-------------------------------------------+
    | `<outline/>`    | §17.3.2.23 | 显示字符轮廓                              |
    +-----------------+------------+-------------------------------------------+
    | `<rtl/>`        | §17.3.2.30 | 从右到左文本                              |
    +-----------------+------------+-------------------------------------------+
    | `<shadow/>`     | §17.3.2.31 | 阴影效果                                  |
    +-----------------+------------+-------------------------------------------+
    | `<smallCaps/>`  | §17.3.2.33 | 小型大写字母                              |
    +-----------------+------------+-------------------------------------------+
    | `<snapToGrid/>` | §17.3.2.34 | 使用文档网格设置进行字符间距调整          |
    +-----------------+------------+-------------------------------------------+
    | `<specVanish/>` | §17.3.2.36 | 段落标记始终隐藏                          |
    +-----------------+------------+-------------------------------------------+
    | `<strike/>`     | §17.3.2.37 | 单重删除线                                |
    +-----------------+------------+-------------------------------------------+
    | `<vanish/>`     | §17.3.2.41 | 隐藏文本                                  |
    +-----------------+------------+-------------------------------------------+
    | `<webHidden/>`  | §17.3.2.44 | 网页隐藏文本                              |
    +-----------------+------------+-------------------------------------------+

.. tab:: 英文

    Character formatting that is either on or off, such as bold, italic, and
    small caps. Certain of these properties are *toggle properties* that may
    cancel each other out if they appear more than once in the style hierarchy.
    See §17.7.3 for more details on toggle properties. They don't affect the API
    specified here.

    The following run properties are boolean (tri-state) properties:

    +-----------------+------------+-------------------------------------------+
    | element         | spec       | name                                      |
    +=================+============+===========================================+
    | `<b/>`          | §17.3.2.1  | Bold                                      |
    +-----------------+------------+-------------------------------------------+
    | `<bCs/>`        | §17.3.2.2  | Complex Script Bold                       |
    +-----------------+------------+-------------------------------------------+
    | `<caps/>`       | §17.3.2.5  | Display All Characters as Capital Letters |
    +-----------------+------------+-------------------------------------------+
    | `<cs/>`         | §17.3.2.7  | Use Complex Script Formatting on Run      |
    +-----------------+------------+-------------------------------------------+
    | `<dstrike/>`    | §17.3.2.9  | Double Strikethrough                      |
    +-----------------+------------+-------------------------------------------+
    | `<emboss/>`     | §17.3.2.13 | Embossing                                 |
    +-----------------+------------+-------------------------------------------+
    | `<i/>`          | §17.3.2.16 | Italics                                   |
    +-----------------+------------+-------------------------------------------+
    | `<iCs/>`        | §17.3.2.17 | Complex Script Italics                    |
    +-----------------+------------+-------------------------------------------+
    | `<imprint/>`    | §17.3.2.18 | Imprinting                                |
    +-----------------+------------+-------------------------------------------+
    | `<noProof/>`    | §17.3.2.21 | Do Not Check Spelling or Grammar          |
    +-----------------+------------+-------------------------------------------+
    | `<oMath/>`      | §17.3.2.22 | Office Open XML Math                      |
    +-----------------+------------+-------------------------------------------+
    | `<outline/>`    | §17.3.2.23 | Display Character Outline                 |
    +-----------------+------------+-------------------------------------------+
    | `<rtl/>`        | §17.3.2.30 | Right To Left Text                        |
    +-----------------+------------+-------------------------------------------+
    | `<shadow/>`     | §17.3.2.31 | Shadow                                    |
    +-----------------+------------+-------------------------------------------+
    | `<smallCaps/>`  | §17.3.2.33 | Small Caps                                |
    +-----------------+------------+-------------------------------------------+
    | `<snapToGrid/>` | §17.3.2.34 | Use Document Grid Settings For Inter-     |
    |                 |            | Character Spacing                         |
    +-----------------+------------+-------------------------------------------+
    | `<specVanish/>` | §17.3.2.36 | Paragraph Mark is Always Hidden           |
    +-----------------+------------+-------------------------------------------+
    | `<strike/>`     | §17.3.2.37 | Single Strikethrough                      |
    +-----------------+------------+-------------------------------------------+
    | `<vanish/>`     | §17.3.2.41 | Hidden Text                               |
    +-----------------+------------+-------------------------------------------+
    | `<webHidden/>`  | §17.3.2.44 | Web Hidden Text                           |
    +-----------------+------------+-------------------------------------------+


协议
--------

Protocol

.. tab:: 中文

    在 API 层面，每个布尔型的运行属性都是一个可读写的“三级状态”属性，具有可能的值 |True|、|False| 和 |None|。

    以下交互式会话演示了查询和应用运行级别属性的协议::

        >>> run = p.add_run()
        >>> run.bold
        None
        >>> run.bold = True
        >>> run.bold
        True
        >>> run.bold = False
        >>> run.bold
        False
        >>> run.bold = None
        >>> run.bold
        None

    这三个值的语义如下：

    .. csv-table::
        :header: "值", "含义"

        "True", "属性的有效值是无条件地 `开启(on)`。样式层次结构中的相反设置没有影响。"
        "False", "属性的有效值是无条件地 `关闭(off)`。样式层次结构中的相反设置没有影响。"
        "None", "元素不存在。有效值从样式层次结构中继承。如果样式层次结构中没有该属性的值，则有效值为 `关闭(off)`。 "

.. tab:: 英文

    At the API level, each of the boolean run properties is a read/write 'tri-state' property, having the possible values |True|, |False|, and |None|.

    The following interactive session demonstrates the protocol for querying and applying run-level properties::

        >>> run = p.add_run()
        >>> run.bold
        None
        >>> run.bold = True
        >>> run.bold
        True
        >>> run.bold = False
        >>> run.bold
        False
        >>> run.bold = None
        >>> run.bold
        None

    The semantics of the three values are as follows:

    +-------+---------------------------------------------------------------+
    | value | meaning                                                       |
    +=======+===============================================================+
    | True  | The effective value of the property is unconditionally `on`.  |
    |       | Contrary settings in the style hierarchy have no effect.      |
    +-------+---------------------------------------------------------------+
    | False | The effective value of the property is unconditionally `off`. |
    |       | Contrary settings in the style hierarchy have no effect.      |
    +-------+---------------------------------------------------------------+
    | None  | The element is not present. The effective value is            |
    |       | inherited from the style hierarchy. If no value for this      |
    |       | property is present in the style hierarchy, the effective     |
    |       | value is `off`.                                               |
    +-------+---------------------------------------------------------------+


切换属性
-----------------

Toggle properties

.. tab:: 中文

    某些布尔型运行属性是 *切换属性*。切换属性是在样式层次结构中的某些位置像 `toggle` 一样行为的属性。这里的切换意味着将属性设置为开启的效果是反转先前的设置，而不是无条件地将属性设置为开启。

    这种行为允许这些属性在继承样式中被覆盖（关闭）。例如，考虑一个设置为粗体的字符样式 `emphasized`。另一个样式 `strong` 继承自 `emphasized`，但应显示为斜体而非粗体。将粗体设置为关闭没有效果，因为它被 `strong` 中的粗体设置所覆盖（我认为是这样的）。由于粗体是一个切换属性，在 `emphasized` 中将粗体设置为开启会导致其值被切换为 `False`，从而达到预期的效果。有关切换属性的更多详细信息，请参见 §17.7.3。

    以下运行属性是切换属性：

    .. list-table::

      * - **元素**
        - **规范**
        - **名称**

      * - `<b/>`
        - §17.3.2.1
        - 粗体

      * - `<bCs/>`
        - §17.3.2.2
        - 复杂脚本粗体

      * - `<caps/>`
        - §17.3.2.5
        - 将所有字符显示为大写字母

      * - `<emboss/>`
        - §17.3.2.13
        - 浮雕效果

      * - `<i/>`
        - §17.3.2.16
        - 斜体

      * - `<iCs/>`
        - §17.3.2.17
        - 复杂脚本斜体

      * - `<imprint/>`
        - §17.3.2.18
        - 印记

      * - `<outline/>`   
        - §17.3.2.23
        - 显示字符轮廓

      * - `<shadow/>`    
        - §17.3.2.31
        - 阴影

      * - `<smallCaps/>` 
        - §17.3.2.33
        - 小型大写字母

      * - `<strike/>`    
        - §17.3.2.37
        - 单行删除线

      * - `<vanish/>`    
        - §17.3.2.41
        - 隐藏文本

.. tab:: 英文

    Certain of the boolean run properties are *toggle properties*. A toggle
    property is one that behaves like a `toggle` at certain places in the style
    hierarchy. Toggle here means that setting the property on has the effect of
    reversing the prior setting rather than unconditionally setting the property
    on.

    This behavior allows these properties to be overridden (turned off) in
    inheriting styles. For example, consider a character style `emphasized` that
    sets bold on. Another style, `strong` inherits from `emphasized`, but should
    display in italic rather than bold. Setting bold off has no effect because it
    is overridden by the bold in `strong` (I think). Because bold is a toggle
    property, setting bold on in `emphasized` causes its value to be toggled, to
    False, achieving the desired effect. See §17.7.3 for more details on toggle
    properties.

    The following run properties are toggle properties:

    +----------------+------------+-------------------------------------------+
    | element        | spec       | name                                      |
    +================+============+===========================================+
    | `<b/>`         | §17.3.2.1  | Bold                                      |
    +----------------+------------+-------------------------------------------+
    | `<bCs/>`       | §17.3.2.2  | Complex Script Bold                       |
    +----------------+------------+-------------------------------------------+
    | `<caps/>`      | §17.3.2.5  | Display All Characters as Capital Letters |
    +----------------+------------+-------------------------------------------+
    | `<emboss/>`    | §17.3.2.13 | Embossing                                 |
    +----------------+------------+-------------------------------------------+
    | `<i/>`         | §17.3.2.16 | Italics                                   |
    +----------------+------------+-------------------------------------------+
    | `<iCs/>`       | §17.3.2.17 | Complex Script Italics                    |
    +----------------+------------+-------------------------------------------+
    | `<imprint/>`   | §17.3.2.18 | Imprinting                                |
    +----------------+------------+-------------------------------------------+
    | `<outline/>`   | §17.3.2.23 | Display Character Outline                 |
    +----------------+------------+-------------------------------------------+
    | `<shadow/>`    | §17.3.2.31 | Shadow                                    |
    +----------------+------------+-------------------------------------------+
    | `<smallCaps/>` | §17.3.2.33 | Small Caps                                |
    +----------------+------------+-------------------------------------------+
    | `<strike/>`    | §17.3.2.37 | Single Strikethrough                      |
    +----------------+------------+-------------------------------------------+
    | `<vanish/>`    | §17.3.2.41 | Hidden Text                               |
    +----------------+------------+-------------------------------------------+


样本 XML
------------

Specimen XML

.. highlight:: xml

::

    <w:r>
      <w:rPr>
        <w:b/>
        <w:i/>
        <w:smallCaps/>
        <w:strike/>
        <w:sz w:val="28"/>
        <w:szCs w:val="28"/>
        <w:u w:val="single"/>
      </w:rPr>
      <w:t>bold, italic, small caps, strike, 14 pt, and underline</w:t>
    </w:r>


架构摘录
--------------

Schema excerpt

.. tab:: 中文

    运行属性似乎可以按任意顺序出现，并且每个属性可能出现多次。不确定这样做的语义是什么，也不确定为什么要这样做，但需要注意。Word 在写入文件时似乎按以下顺序放置它们。

.. tab:: 英文

    It appears the run properties may appear in any order and may appear multiple
    times each. Not sure what the semantics of that would be or why one would
    want to do it, but something to note. Word seems to place them in the order
    below when it writes the file.

.. highlight:: xml
  
::

  <xsd:complexType name="CT_RPr">  <!-- denormalized -->
    <xsd:sequence>
      <xsd:choice minOccurs="0" maxOccurs="unbounded"/>
        <xsd:element name="rStyle"          type="CT_String"/>
        <xsd:element name="rFonts"          type="CT_Fonts"/>
        <xsd:element name="b"               type="CT_OnOff"/>
        <xsd:element name="bCs"             type="CT_OnOff"/>
        <xsd:element name="i"               type="CT_OnOff"/>
        <xsd:element name="iCs"             type="CT_OnOff"/>
        <xsd:element name="caps"            type="CT_OnOff"/>
        <xsd:element name="smallCaps"       type="CT_OnOff"/>
        <xsd:element name="strike"          type="CT_OnOff"/>
        <xsd:element name="dstrike"         type="CT_OnOff"/>
        <xsd:element name="outline"         type="CT_OnOff"/>
        <xsd:element name="shadow"          type="CT_OnOff"/>
        <xsd:element name="emboss"          type="CT_OnOff"/>
        <xsd:element name="imprint"         type="CT_OnOff"/>
        <xsd:element name="noProof"         type="CT_OnOff"/>
        <xsd:element name="snapToGrid"      type="CT_OnOff"/>
        <xsd:element name="vanish"          type="CT_OnOff"/>
        <xsd:element name="webHidden"       type="CT_OnOff"/>
        <xsd:element name="color"           type="CT_Color"/>
        <xsd:element name="spacing"         type="CT_SignedTwipsMeasure"/>
        <xsd:element name="w"               type="CT_TextScale"/>
        <xsd:element name="kern"            type="CT_HpsMeasure"/>
        <xsd:element name="position"        type="CT_SignedHpsMeasure"/>
        <xsd:element name="sz"              type="CT_HpsMeasure"/>
        <xsd:element name="szCs"            type="CT_HpsMeasure"/>
        <xsd:element name="highlight"       type="CT_Highlight"/>
        <xsd:element name="u"               type="CT_Underline"/>
        <xsd:element name="effect"          type="CT_TextEffect"/>
        <xsd:element name="bdr"             type="CT_Border"/>
        <xsd:element name="shd"             type="CT_Shd"/>
        <xsd:element name="fitText"         type="CT_FitText"/>
        <xsd:element name="vertAlign"       type="CT_VerticalAlignRun"/>
        <xsd:element name="rtl"             type="CT_OnOff"/>
        <xsd:element name="cs"              type="CT_OnOff"/>
        <xsd:element name="em"              type="CT_Em"/>
        <xsd:element name="lang"            type="CT_Language"/>
        <xsd:element name="eastAsianLayout" type="CT_EastAsianLayout"/>
        <xsd:element name="specVanish"      type="CT_OnOff"/>
        <xsd:element name="oMath"           type="CT_OnOff"/>
      </xsd:choice>
      <xsd:element name="rPrChange" type="CT_RPrChange" minOccurs="0"/>
    </xsd:sequence>
  </xsd:group>

  <xsd:complexType name="CT_Fonts">
    <xsd:attribute name="hint"          type="ST_Hint"/>
    <xsd:attribute name="ascii"         type="s:ST_String"/>
    <xsd:attribute name="hAnsi"         type="s:ST_String"/>
    <xsd:attribute name="eastAsia"      type="s:ST_String"/>
    <xsd:attribute name="cs"            type="s:ST_String"/>
    <xsd:attribute name="asciiTheme"    type="ST_Theme"/>
    <xsd:attribute name="hAnsiTheme"    type="ST_Theme"/>
    <xsd:attribute name="eastAsiaTheme" type="ST_Theme"/>
    <xsd:attribute name="cstheme"       type="ST_Theme"/>
  </xsd:complexType>

  <xsd:complexType name="CT_HpsMeasure">
    <xsd:attribute name="val" type="ST_HpsMeasure" use="required"/>
  </xsd:complexType>

  <xsd:complexType name="CT_OnOff">
    <xsd:attribute name="val" type="s:ST_OnOff"/>
  </xsd:complexType>

  <xsd:complexType name="CT_SignedHpsMeasure">
    <xsd:attribute name="val" type="ST_SignedHpsMeasure" use="required"/>
  </xsd:complexType>

  <xsd:complexType name="CT_String">
    <xsd:attribute name="val" type="s:ST_String" use="required"/>
  </xsd:complexType>

  <xsd:complexType name="CT_Underline">
    <xsd:attribute name="val"        type="ST_Underline"/>
    <xsd:attribute name="color"      type="ST_HexColor"/>
    <xsd:attribute name="themeColor" type="ST_ThemeColor"/>
    <xsd:attribute name="themeTint"  type="ST_UcharHexNumber"/>
    <xsd:attribute name="themeShade" type="ST_UcharHexNumber"/>
  </xsd:complexType>

  <xsd:complexType name="CT_VerticalAlignRun">
    <xsd:attribute name="val" type="s:ST_VerticalAlignRun" use="required"/>
  </xsd:complexType>

  <!-- simple types -->

  <xsd:simpleType name="ST_Hint">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="default"/>
      <xsd:enumeration value="eastAsia"/>
      <xsd:enumeration value="cs"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_HpsMeasure">
    <xsd:union memberTypes="s:ST_UnsignedDecimalNumber
                            s:ST_PositiveUniversalMeasure"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff">
    <xsd:union memberTypes="xsd:boolean ST_OnOff1"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_OnOff1">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="on"/>
      <xsd:enumeration value="off"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_PositiveUniversalMeasure">
    <xsd:restriction base="ST_UniversalMeasure">
      <xsd:pattern value="[0-9]+(\.[0-9]+)?(mm|cm|in|pt|pc|pi)"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_SignedHpsMeasure">
    <xsd:union memberTypes="xsd:integer s:ST_UniversalMeasure"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_Theme">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="majorEastAsia"/>
      <xsd:enumeration value="majorBidi"/>
      <xsd:enumeration value="majorAscii"/>
      <xsd:enumeration value="majorHAnsi"/>
      <xsd:enumeration value="minorEastAsia"/>
      <xsd:enumeration value="minorBidi"/>
      <xsd:enumeration value="minorAscii"/>
      <xsd:enumeration value="minorHAnsi"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_Underline">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="single"/>
      <xsd:enumeration value="words"/>
      <xsd:enumeration value="double"/>
      <xsd:enumeration value="thick"/>
      <xsd:enumeration value="dotted"/>
      <xsd:enumeration value="dottedHeavy"/>
      <xsd:enumeration value="dash"/>
      <xsd:enumeration value="dashedHeavy"/>
      <xsd:enumeration value="dashLong"/>
      <xsd:enumeration value="dashLongHeavy"/>
      <xsd:enumeration value="dotDash"/>
      <xsd:enumeration value="dashDotHeavy"/>
      <xsd:enumeration value="dotDotDash"/>
      <xsd:enumeration value="dashDotDotHeavy"/>
      <xsd:enumeration value="wave"/>
      <xsd:enumeration value="wavyHeavy"/>
      <xsd:enumeration value="wavyDouble"/>
      <xsd:enumeration value="none"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_UnsignedDecimalNumber">
    <xsd:restriction base="xsd:unsignedLong"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_VerticalAlignRun">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="baseline"/>
      <xsd:enumeration value="superscript"/>
      <xsd:enumeration value="subscript"/>
    </xsd:restriction>
  </xsd:simpleType>
