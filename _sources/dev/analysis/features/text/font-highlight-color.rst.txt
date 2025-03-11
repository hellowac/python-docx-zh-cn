
字体高亮颜色
====================

Font highlight color

.. tab:: 中文

    Word 文档中的文本可以用多种颜色“突出显示”，提供文本背景颜色。视觉效果类似于在打印页面上使用荧光笔（通常是荧光黄）产生的效果。

.. tab:: 英文

    Text in a Word document can be "highlighted" with a number of colors, providing text background color. The visual effect is similar to that produced using a highlighter (often fluorescent yellow) on a printed page.


协议
--------

Protocol

.. tab:: 中文

    通过将 `WD_COLOR_INDEX` 的成员分配给 `Font.highlight_color` 来突出显示文本。

.. tab:: 英文

    Text is highlighted by assigning a member of `WD_COLOR_INDEX` to `Font.highlight_color`.

::

    >>> font = paragraph.add_run().font
    >>> font.highlight_color
    None
    >>> font.highlight_color = WD_COLOR_INDEX.YELLOW
    >>> font.highlight_color
    YELLOW (7)
    >>> font.highlight_color = WD_COLOR_INDEX.TURQUOISE
    >>> font.highlight_color
    TURQUOISE (3)
    >>> font.highlight_color = None
    >>> font.highlight_color
    None


枚举
------------

Enumerations

* `WdColorIndex Enumeration on MSDN`_

.. _WdColorIndex Enumeration on MSDN: https://msdn.microsoft.com/EN-US/library/office/ff195343.aspx


XML 语义
-------------

XML Semantics

.. tab:: 中文
    
    将 `WD_COLOR_INDEX` 成员映射到 `ST_Highlight` 值

.. tab:: 英文

    Mapping of `WD_COLOR_INDEX` members to `ST_Highlight` values

::

    AUTO = 'default'
    BLACK = 'black'
    BLUE = 'blue'
    BRIGHTGREEN = 'green'
    DARKBLUE = 'darkBlue'
    DARKRED = 'darkRed'
    DARKYELLOW = 'darkYellow'
    GRAY25 = 'lightGray'
    GRAY50 = 'darkGray'
    GREEN = 'darkGreen'
    PINK = 'magenta'
    RED = 'red'
    TEAL = 'darkCyan'
    TURQUOISE = 'cyan'
    VOILET = 'darkMagenta'
    WHITE = 'white'
    YELLOW = 'yellow'


样本 XML
------------

Specimen XML

.. highlight:: xml

.. tab:: 中文

    基线运行（Baseline run）::

      <w:r>
        <w:t>黑色文本，白色背景</w:t>
      </w:r>

    蓝色文本，亮绿色高亮::

      <w:r>
        <w:rPr>
          <w:highlight w:val="green"/>
        </w:rPr>
        <w:t>蓝色文本，亮绿色背景</w:t>
      </w:r>

    红色文本，绿色高亮::

      <w:r>
        <w:rPr>
          <w:highlight w:val="darkGreen"/>
        </w:rPr>
        <w:t>红色文本，绿色背景</w:t>
      </w:r>

.. tab:: 英文

    Baseline run::

      <w:r>
        <w:t>Black text on white background</w:t>
      </w:r>

    Blue text, Bright Green Highlight::

      <w:r>
        <w:rPr>
          <w:highlight w:val="green"/>
        </w:rPr>
        <w:t>Blue text on bright green background</w:t>
      </w:r>

    Red text, Green Highlight::

      <w:r>
        <w:rPr>
          <w:highlight w:val="darkGreen"/>
        </w:rPr>
        <w:t>Red text on green background</w:t>
      </w:r>


架构摘录
--------------

Schema excerpt

.. tab:: 中文

    根据架构，运行属性可以按任意顺序出现，并且每个属性可能出现多次。不确定其语义是什么，也不确定为什么要这样做，但需要注意。Word 似乎在写入文件时将它们按以下顺序放置。

.. tab:: 英文

    According to the schema, run properties may appear in any order and may
    appear multiple times each. Not sure what the semantics of that would be or
    why one would want to do it, but something to note. Word seems to place them
    in the order below when it writes the file.

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

  <!-- complex types -->

  <xsd:complexType name="CT_Highlight">
    <xsd:attribute name="val" type="ST_Highlight" use="required"/>
  </xsd:complexType>

  <!-- simple types -->

  <xsd:simpleType name="ST_Highlight">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="default"/>
      <xsd:enumeration value="black"/>
      <xsd:enumeration value="blue"/>
      <xsd:enumeration value="green"/>
      <xsd:enumeration value="darkBlue"/>
      <xsd:enumeration value="darkRed"/>
      <xsd:enumeration value="darkYellow"/>
      <xsd:enumeration value="lightGray"/>
      <xsd:enumeration value="darkGray"/>
      <xsd:enumeration value="darkGreen"/>
      <xsd:enumeration value="magenta"/>
      <xsd:enumeration value="red"/>
      <xsd:enumeration value="darkCyan"/>
      <xsd:enumeration value="cyan"/>
      <xsd:enumeration value="darkMagenta"/>
      <xsd:enumeration value="white"/>
      <xsd:enumeration value="yellow"/>
    </xsd:restriction>
  </xsd:simpleType>
