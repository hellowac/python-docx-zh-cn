
下划线
=========

Underline

.. tab:: 中文

    Word 文档中的文本可以采用多种样式加下划线。

.. tab:: 英文

    Text in a Word document can be underlined in a variety of styles.


协议
--------

Protocol

.. tab:: 中文

    下划线的调用协议被重载，使得它像 ``.bold`` 和 ``.italic`` 一样支持单一的下划线，同时也允许赋值枚举值来指定更复杂的下划线样式，例如虚线、波浪线和双下划线::

        >>> run = paragraph.add_run()
        >>> run.underline
        None
        >>> run.underline = True
        >>> run.underline
        True
        >>> run.underline = WD_UNDERLINE.SINGLE
        >>> run.underline
        True
        >>> run.underline = WD_UNDERLINE.DOUBLE
        >>> str(run.underline)
        DOUBLE (3)
        >>> run.underline = False
        >>> run.underline
        False
        >>> run.underline = WD_UNDERLINE.NONE
        >>> run.underline
        False
        >>> run.underline = None
        >>> run.underline
        None

.. tab:: 英文

    The call protocol for underline is overloaded such that it works like
    ``.bold`` and ``.italic`` for single underline, but also allows an enumerated
    value to be assigned to specify more sophisticated underlining such as
    dashed, wavy, and double-underline::

        >>> run = paragraph.add_run()
        >>> run.underline
        None
        >>> run.underline = True
        >>> run.underline
        True
        >>> run.underline = WD_UNDERLINE.SINGLE
        >>> run.underline
        True
        >>> run.underline = WD_UNDERLINE.DOUBLE
        >>> str(run.underline)
        DOUBLE (3)
        >>> run.underline = False
        >>> run.underline
        False
        >>> run.underline = WD_UNDERLINE.NONE
        >>> run.underline
        False
        >>> run.underline = None
        >>> run.underline
        None


枚举
------------

Enumerations

.. tab:: 中文

.. tab:: 英文

* `WdUnderline Enumeration on MSDN`_

.. _WdUnderline Enumeration on MSDN:
   http://msdn.microsoft.com/en-us/library/office/ff822388(v=office.15).aspx


样本 XML
------------

Specimen XML

.. highlight:: xml

.. tab:: 中文

    基线运行::

        <w:r>
          <w:t>下划线由继承决定</w:t>
        </w:r>

    单一下划线::

        <w:r>
          <w:rPr>
            <w:u w:val="single"/>
          </w:rPr>
          <w:t>单一下划线</w:t>
        </w:r>

    双下划线::

        <w:r>
          <w:rPr>
            <w:u w:val="double"/>
          </w:rPr>
          <w:t>双下划线</w:t>
        </w:r>

    直接应用无下划线，覆盖继承值::

        <w:r>
          <w:rPr>
            <w:u w:val="none"/>
          </w:rPr>
          <w:t>无下划线</w:t>
        </w:r>

.. tab:: 英文

    Baseline run::

        <w:r>
          <w:t>underlining determined by inheritance</w:t>
        </w:r>

    Single underline::

        <w:r>
          <w:rPr>
            <w:u w:val="single"/>
          </w:rPr>
          <w:t>single underlined</w:t>
        </w:r>

    Double underline::

        <w:r>
          <w:rPr>
            <w:u w:val="double"/>
          </w:rPr>
          <w:t>single underlined</w:t>
        </w:r>

    Directly-applied no-underline, overrides inherited value::

        <w:r>
          <w:rPr>
            <w:u w:val="none"/>
          </w:rPr>
          <w:t>not underlined</w:t>
        </w:r>


架构摘录
--------------

Schema excerpt

.. tab:: 中文

    请注意， ``CT_Underline`` 上的 ``w:val`` 属性是可选的。如果不存在，则运行时不会出现下划线。

.. tab:: 英文

    Note that the ``w:val`` attribute on ``CT_Underline`` is optional. When it is
    not present no underline appears on the run.

.. highlight:: xml

::

  <xsd:complexType name="CT_R">  <!-- flattened for readibility -->
    <xsd:sequence>
      <xsd:element name="rPr" type="CT_RPr" minOccurs="0"/>
      <xsd:group   ref="EG_RunInnerContent" minOccurs="0" maxOccurs="unbounded"/>
    </xsd:sequence>
    <xsd:attribute name="rsidRPr" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidDel" type="ST_LongHexNumber"/>
    <xsd:attribute name="rsidR"   type="ST_LongHexNumber"/>
  </xsd:complexType>

  <xsd:complexType name="CT_RPr">  <!-- flattened for readibility -->
    <xsd:sequence>
      <xsd:group   ref="EG_RPrBase" minOccurs="0" maxOccurs="unbounded"/>
      <xsd:element name="rPrChange" type="CT_RPrChange" minOccurs="0"/>
    </xsd:sequence>
  </xsd:complexType>

  <xsd:group name="EG_RPrBase">
    <xsd:choice>
      <xsd:element name="rStyle"          type="CT_String"/>
      <xsd:element name="b"               type="CT_OnOff"/>
      <xsd:element name="i"               type="CT_OnOff"/>
      <xsd:element name="color"           type="CT_Color"/>
      <xsd:element name="sz"              type="CT_HpsMeasure"/>
      <xsd:element name="u"               type="CT_Underline"/>
      <!-- 33 others -->
    </xsd:choice>
  </xsd:group>

  <xsd:complexType name="CT_Underline">
    <xsd:attribute name="val"        type="ST_Underline"/>
    <xsd:attribute name="color"      type="ST_HexColor"/>
    <xsd:attribute name="themeColor" type="ST_ThemeColor"/>
    <xsd:attribute name="themeTint"  type="ST_UcharHexNumber"/>
    <xsd:attribute name="themeShade" type="ST_UcharHexNumber"/>
  </xsd:complexType>

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
