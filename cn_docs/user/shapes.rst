
了解图片和其他形状
=======================================

Understanding pictures and other shapes

.. tab:: 中文

    从概念上讲，Word 文档有两个 `层` （ `layers` ），即 *文本层(text layer)* 和 *绘图层(drawing layer)*。  
    在文本层中，文本对象从左到右、从上到下流式排列，并在填满当前页面时自动换页。  
    在绘图层中，绘图对象（称为 `形状(shapes)` ）可以被放置在任意位置，有时这些形状也被称为 `浮动(floating)` 形状。

    图片是一种可以出现在文本层或绘图层中的形状。  
    当它出现在文本层时，称为 *内联形状(inline shape)*，更具体地说，称为 *内联图片(inline picture)*。

    内联形状的行为类似于一个较大的文本字符（ *字符字形(character glyph)* ）。  
    行高会自动增加以容纳该形状，并且该形状会像文本一样适应行宽进行换行。  
    如果在其前面插入文本，它会向右移动。通常，图片会单独放置在一个段落中，但这并不是必须的，  
    它也可以与同一段落中的文本共存，即在其前后都有文本。

    在撰写本文时，|docx| 仅支持内联图片。  
    浮动图片虽然可以添加，但如果你有相关的使用需求，可以在 issue 追踪器上提交功能请求。  
    ``Document.add_picture()`` 方法会将指定的图片添加到文档末尾，并单独占据一个段落。  
    不过，如果深入研究 API，还可以让图片与同一段落中的文本并列显示，甚至同时在其两侧放置文本。


.. tab:: 英文

    Conceptually, Word documents have two `layers`, a *text layer* and a *drawing layer*. In the text layer, text objects are flowed from left to right and from top to bottom, starting a new page when the prior one is filled. In the drawing layer, drawing objects, called `shapes`, are placed at arbitrary positions. These are sometimes referred to as `floating` shapes.

    A picture is a shape that can appear in either the text or drawing layer. When it appears in the text layer it is called an *inline shape*, or more specifically, an *inline picture*.

    Inline shapes are treated like a big text character (a *character glyph*). The line height is increased to accomodate the shape and the shape is wrapped to a line it will fit on width-wise, just like text. Inserting text in front of it will cause it to move to the right. Often, a picture is placed in a paragraph by itself, but this is not required. It can have text before and after it in the paragraph in which it's placed.

    At the time of writing, |docx| only supports inline pictures. Floating pictures can be added. If you have an active use case, submit a feature request on the issue tracker. The ``Document.add_picture()`` method adds a specified picture to the end of the document in a paragraph of its own. However, by digging a little deeper into the API you can place text on either side of the picture in its paragraph, or both.
