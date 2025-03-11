
字体颜色
==========

Font Color

.. tab:: 中文

    颜色作为一个主题，超出了 |Font| 对象的范围；字体颜色只是它首次出现的地方。因此，这个问题需要比通常更多的思考，因为我们希望在其他上下文中复用相同的对象和协议；因此，制定一个通用的解决方案，能够满足预期的复用，是有意义的。

    有三个历史来源可供此 API 借鉴：

    1. `w:rPr/w:color` 元素。默认情况下，当直接应用颜色到文本或设置样式的文本颜色时，使用此元素。这对应于 `Font.Color` 属性（不幸的是，未记录）。此元素支持 RGB 颜色、主题颜色以及主题颜色的色调或阴影。

    2. `w:rPr/w14:textFill` 元素。Word 用于处理如渐变和阴影效果等华丽文本的元素。它对应于 `Font.Fill` 属性。

    3. PowerPoint 字体颜色 UI。这看起来是前两者之间的一个合理折衷，既允许直接访问常见的颜色选项，同时也为以后在需要时添加 `Font.fill` 操作留出了空间。

.. tab:: 英文

    Color, as a topic, extends beyond the |Font| object; font color is just the first place it's come up. Accordingly, it bears a little deeper thought than usual since we'll want to reuse the same objects and protocol to specify color in the other contexts; it makes sense to craft a general solution that will bear the expected reuse.

    There are three historical sources to draw from for this API.

    1. The `w:rPr/w:color` element. This is used by default when applying color directly to text or when setting the text color of a style. This corresponds to the `Font.Color` property (undocumented, unfortunately). This element supports RGB colors, theme colors, and a tint or shade of a theme color.

    2. The `w:rPr/w14:textFill` element. This is used by Word for fancy text like gradient and shadow effects. This corresponds to the `Font.Fill` property.

    3. The PowerPoint font color UI. This seems like a reasonable compromise between the prior two, allowing direct-ish access to common color options while holding the door open for the `Font.fill` operations to be added later if required.

候选协议
~~~~~~~~~~~~~~~~~~

Candidate Protocol

.. tab:: 中文

    :class:`docx.text.run.Run` 具有一个字体属性::

        >>> from docx import Document
        >>> from docx.text.run import Font, Run
        >>> run = Document().add_paragraph().add_run()
        >>> isinstance(run, Run)
        True
        >>> font = run.font
        >>> isinstance(font, Font)
        True

    :class:`docx.text.run.Font` 具有一个只读的颜色属性，返回一个 :class:`docx.dml.color.ColorFormat` 对象::

        >>> from docx.dml.color import ColorFormat
        >>> color = font.color
        >>> isinstance(font.color, ColorFormat)
        True
        >>> font.color = 'anything'
        AttributeError: can't set attribute

    :class:`docx.dml.color.ColorFormat` 具有一个只读的 :attr:`type` 属性和读写的 :attr:`rgb`、:attr:`theme_color` 和 :attr:`brightness` 属性。

    :attr:`ColorFormat.type` 返回 `MSO_COLOR_TYPE.RGB`、`MSO_COLOR_TYPE.THEME`、`MSO_COLOR_TYPE.AUTO` 或 |None| 其中之一，后者表示字体没有直接应用的颜色::

        >>> font.color.type
        None

    :attr:`ColorFormat.rgb` 当 `type` 为 `MSO_COLOR_TYPE.RGB` 时返回一个 |RGBColor| 对象。当 `type` 为 `MSO_COLOR_TYPE.THEME` 时，它也可能报告一个 RGBColor 值，因为在这种情况下也可能存在 RGB 颜色。根据规范，当指定主题颜色时，RGB 颜色值会被忽略，但 Word 在分配主题颜色时会将当前的主题颜色 RGB 值以及主题颜色名称（例如 'accent1'）一起写入；这可能是供文件浏览器使用的方便值。必须查看 `.type` 的值来确定 RGB 值是否有效或是“最佳猜测”::

        >>> font.color.type
        RGB (1)
        >>> font.color.rgb
        RGBColor(0x3f, 0x2c, 0x36)

    将 |RGBColor| 值分配给 :attr:`ColorFormat.rgb` 会使 :attr:`ColorFormat.type` 变为 `MSO_COLOR_TYPE.RGB`::

        >>> font.color.type
        None
        >>> font.color.rgb = RGBColor(0x3f, 0x2c, 0x36)
        >>> font.color.type
        RGB (1)
        >>> font.color.rgb
        RGBColor(0x3f, 0x2c, 0x36)

    :attr:`ColorFormat.theme_color` 当 `type` 为 `MSO_COLOR_TYPE.THEME` 时，返回 :ref:`MsoThemeColorIndex` 的一个成员::

        >>> font.color.type
        THEME (2)
        >>> font.color.theme_color
        ACCENT_1 (5)

    将 :ref:`MsoThemeColorIndex` 的成员分配给 :attr:`ColorFormat.theme_color` 会使 :attr:`ColorFormat.type` 变为 `MSO_COLOR_TYPE.THEME`::

        >>> font.color.type
        RGB (1)
        >>> font.color.theme_color = MSO_THEME_COLOR.ACCENT_2
        >>> font.color.type
        THEME (2)
        >>> font.color.theme_color
        ACCENT_2 (6)

    :attr:`ColorFormat.brightness` 属性可以用来选择主题颜色的色调或阴影。分配值 0.1 会使颜色变亮 10%（色调）；分配值 -0.1 会使颜色变暗 10%（阴影）::

        >>> font.color.type
        None
        >>> font.color.brightness
        0.0
        >>> font.color.brightness = 0.4
        ValueError: not a theme color

        >>> font.color.theme_color = MSO_THEME_COLOR.TEXT_1
        >>> font.color.brightness = 0.4
        >>> font.color.brightness
        0.4

.. tab:: 英文

    :class:`docx.text.run.Run` has a font property::

        >>> from docx import Document
        >>> from docx.text.run import Font, Run
        >>> run = Document().add_paragraph().add_run()
        >>> isinstance(run, Run)
        True
        >>> font = run.font
        >>> isinstance(font, Font)
        True

    :class:`docx.text.run.Font` has a read-only color property, returning
    a :class:`docx.dml.color.ColorFormat` object::

        >>> from docx.dml.color import ColorFormat
        >>> color = font.color
        >>> isinstance(font.color, ColorFormat)
        True
        >>> font.color = 'anything'
        AttributeError: can't set attribute


    :class:`docx.dml.color.ColorFormat` has a read-only :attr:`type` property and
    read/write :attr:`rgb`, :attr:`theme_color`, and :attr:`brightness`
    properties.

    :attr:`ColorFormat.type` returns one of `MSO_COLOR_TYPE.RGB`,
    `MSO_COLOR_TYPE.THEME`, `MSO_COLOR_TYPE.AUTO`, or |None|, the latter
    indicating font has no directly-applied color::

        >>> font.color.type
        None

    :attr:`ColorFormat.rgb` returns an |RGBColor| object when `type` is
    `MSO_COLOR_TYPE.RGB`. It may also report an RGBColor value when `type` is
    `MSO_COLOR_TYPE.THEME`, since an RGB color may also be present in that case.
    According to the spec, the RGB color value is ignored when a theme color is
    specified, but Word writes the current RGB value of the theme color along
    with the theme color name (e.g. 'accent1') when assigning a theme color;
    perhaps as a convenient value for a file browser to use. The value of `.type`
    must be consulted to determine whether the RGB value is operative or
    a "best-guess"::

        >>> font.color.type
        RGB (1)
        >>> font.color.rgb
        RGBColor(0x3f, 0x2c, 0x36)

    Assigning an |RGBColor| value to :attr:`ColorFormat.rgb` causes
    :attr:`ColorFormat.type` to become `MSO_COLOR_TYPE.RGB`::

        >>> font.color.type
        None
        >>> font.color.rgb = RGBColor(0x3f, 0x2c, 0x36)
        >>> font.color.type
        RGB (1)
        >>> font.color.rgb
        RGBColor(0x3f, 0x2c, 0x36)

    :attr:`ColorFormat.theme_color` returns a member of :ref:`MsoThemeColorIndex`
    when `type` is `MSO_COLOR_TYPE.THEME`::

        >>> font.color.type
        THEME (2)
        >>> font.color.theme_color
        ACCENT_1 (5)

    Assigning a member of :ref:`MsoThemeColorIndex` to
    :attr:`ColorFormat.theme_color` causes :attr:`ColorFormat.type` to become
    `MSO_COLOR_TYPE.THEME`::

        >>> font.color.type
        RGB (1)
        >>> font.color.theme_color = MSO_THEME_COLOR.ACCENT_2
        >>> font.color.type
        THEME (2)
        >>> font.color.theme_color
        ACCENT_2 (6)

    The :attr:`ColorFormat.brightness` attribute can be used to select a tint or
    shade of a theme color. Assigning the value 0.1 produces a color 10% brighter
    (a tint); assigning -0.1 produces a color 10% darker (a shade)::

        >>> font.color.type
        None
        >>> font.color.brightness
        0.0
        >>> font.color.brightness = 0.4
        ValueError: not a theme color

        >>> font.color.theme_color = MSO_THEME_COLOR.TEXT_1
        >>> font.color.brightness = 0.4
        >>> font.color.brightness
        0.4


样本 XML
------------

Specimen XML

.. highlight:: xml

.. tab:: 中文

    没有字体颜色的基准段落::

        <w:p>
          <w:r>
            <w:t>Text with no color.</w:t>
          </w:r>
        </w:p>

    直接应用 RGB 颜色的段落::

        <w:p>
          <w:pPr>
            <w:rPr>
              <w:color w:val="0000FF"/>
            </w:rPr>
          </w:pPr>
          <w:r>
            <w:rPr>
              <w:color w:val="0000FF"/>
            </w:rPr>
            <w:t>Directly-applied color Blue.</w:t>
          </w:r>
        </w:p>

    直接应用主题颜色的文本运行::

        <w:r>
          <w:rPr>
            <w:color w:val="4F81BD" w:themeColor="accent1"/>
          </w:rPr>
          <w:t>Theme color Accent 1.</w:t>
        </w:r>

    使用 Text 2 主题颜色的 40% 色调的文本运行::

        <w:r>
          <w:rPr>
            <w:color w:val="548DD4" w:themeColor="text2" w:themeTint="99"/>
          </w:rPr>
          <w:t>Theme color with 40% tint.</w:t>
        </w:r>

    使用 Accent 2 主题颜色的 25% 阴影的文本运行::

        <w:r>
          <w:rPr>
            <w:color w:val="943634" w:themeColor="accent2" w:themeShade="BF"/>
          </w:rPr>
          <w:t>Theme color with 25% shade.</w:t>
        </w:r>

.. tab:: 英文

    Baseline paragraph with no font color::

        <w:p>
          <w:r>
            <w:t>Text with no color.</w:t>
          </w:r>
        </w:p>

    Paragraph with directly-applied RGB color::

        <w:p>
          <w:pPr>
            <w:rPr>
              <w:color w:val="0000FF"/>
            </w:rPr>
          </w:pPr>
          <w:r>
            <w:rPr>
              <w:color w:val="0000FF"/>
            </w:rPr>
            <w:t>Directly-applied color Blue.</w:t>
          </w:r>
        </w:p>

    Run with directly-applied theme color::

        <w:r>
          <w:rPr>
            <w:color w:val="4F81BD" w:themeColor="accent1"/>
          </w:rPr>
          <w:t>Theme color Accent 1.</w:t>
        </w:r>

    Run with 40% tint of Text 2 theme color::

        <w:r>
          <w:rPr>
            <w:color w:val="548DD4" w:themeColor="text2" w:themeTint="99"/>
          </w:rPr>
          <w:t>Theme color with 40% tint.</w:t>
        </w:r>

    Run with 25% shade of Accent 2 theme color::

        <w:r>
          <w:rPr>
            <w:color w:val="943634" w:themeColor="accent2" w:themeShade="BF"/>
          </w:rPr>
          <w:t>Theme color with 25% shade.</w:t>
        </w:r>


Schema 摘录
--------------

Schema excerpt

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

  <xsd:complexType name="CT_Color">
    <xsd:attribute name="val"        type="ST_HexColor" use="required"/>
    <xsd:attribute name="themeColor" type="ST_ThemeColor"/>
    <xsd:attribute name="themeTint"  type="ST_UcharHexNumber"/>
    <xsd:attribute name="themeShade" type="ST_UcharHexNumber"/>
  </xsd:complexType>

  <!-- simple types -->

  <xsd:simpleType name="ST_HexColor">
    <xsd:union memberTypes="ST_HexColorAuto s:ST_HexColorRGB"/>
  </xsd:simpleType>

  <xsd:simpleType name="ST_HexColorAuto">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="auto"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_HexColorRGB">
    <xsd:restriction base="xsd:hexBinary">
      <xsd:length value="3" fixed="true"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_ThemeColor">
    <xsd:restriction base="xsd:string">
      <xsd:enumeration value="dark1"/>
      <xsd:enumeration value="light1"/>
      <xsd:enumeration value="dark2"/>
      <xsd:enumeration value="light2"/>
      <xsd:enumeration value="accent1"/>
      <xsd:enumeration value="accent2"/>
      <xsd:enumeration value="accent3"/>
      <xsd:enumeration value="accent4"/>
      <xsd:enumeration value="accent5"/>
      <xsd:enumeration value="accent6"/>
      <xsd:enumeration value="hyperlink"/>
      <xsd:enumeration value="followedHyperlink"/>
      <xsd:enumeration value="none"/>
      <xsd:enumeration value="background1"/>
      <xsd:enumeration value="text1"/>
      <xsd:enumeration value="background2"/>
      <xsd:enumeration value="text2"/>
    </xsd:restriction>
  </xsd:simpleType>

  <xsd:simpleType name="ST_UcharHexNumber">
    <xsd:restriction base="xsd:hexBinary">
      <xsd:length value="1"/>
    </xsd:restriction>
  </xsd:simpleType>
