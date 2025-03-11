.. _WdUnderline:

``WD_UNDERLINE``
================

.. tab:: 中文

    指定应用于一连串字符的下划线样式。

    ----

    NONE
        无下划线。此设置将覆盖任何继承的下划线值，因此可用于从继承了其包含段落的下划线的连串中删除下划线。请注意，这与将 |None| 分配给 Run.underline 不同。|None| 是有效的分配值，但会导致连串继承其下划线值。分配 ``WD_UNDERLINE.NONE`` 会导致无条件关闭下划线。

    SINGLE
        单行。请注意，此设置是只写的，因为对于具有此设置的连串，将返回 |True|（而不是 ``WD_UNDERLINE.SINGLE``）。

    WORDS
        仅对单个单词加下划线。

    DOUBLE
        双线。

    DOTTED
        点。

    THICK
        单条粗线。

    DASH
        虚线。

    DOT_DASH
        交替的点和划线。

    DOT_DOT_DASH
        交替的点-点-划线图案。

    WAVY
        单条波浪线。

    DOTTED_HEAVY
        粗点。

    DASH_HEAVY
        粗划线。

    DOT_DASH_HEAVY
        交替的粗点和粗划线。

    DOT_DOT_DASH_HEAVY
        交替的粗点-点-划线图案。

    WAVY_HEAVY
        粗波浪线。

    DASH_LONG
        长划线。

    WAVY_DOUBLE
        双波浪线。

    DASH_LONG_HEAVY
        长粗划线。

.. tab:: 英文

    Specifies the style of underline applied to a run of characters.

    ----

    NONE
        No underline. This setting overrides any inherited underline value, so can
        be used to remove underline from a run that inherits underlining from its
        containing paragraph. Note this is not the same as assigning |None| to
        Run.underline. |None| is a valid assignment value, but causes the run to
        inherit its underline value. Assigning ``WD_UNDERLINE.NONE`` causes
        underlining to be unconditionally turned off.

    SINGLE
        A single line. Note that this setting is write-only in the sense that
        |True| (rather than ``WD_UNDERLINE.SINGLE``) is returned for a run having
        this setting.

    WORDS
        Underline individual words only.

    DOUBLE
        A double line.

    DOTTED
        Dots.

    THICK
        A single thick line.

    DASH
        Dashes.

    DOT_DASH
        Alternating dots and dashes.

    DOT_DOT_DASH
        An alternating dot-dot-dash pattern.

    WAVY
        A single wavy line.

    DOTTED_HEAVY
        Heavy dots.

    DASH_HEAVY
        Heavy dashes.

    DOT_DASH_HEAVY
        Alternating heavy dots and heavy dashes.

    DOT_DOT_DASH_HEAVY
        An alternating heavy dot-dot-dash pattern.

    WAVY_HEAVY
        A heavy wavy line.

    DASH_LONG
        Long dashes.

    WAVY_DOUBLE
        A double wavy line.

    DASH_LONG_HEAVY
        Long heavy dashes.
