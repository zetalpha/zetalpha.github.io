以下内容为机翻 [原文](https://jsoup.org/apidocs/org/jsoup/select/Selector.html)

公共类选择器扩展 [对象](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)

类似 CSS 的元素选择器，用于查找与查询匹配的元素。

## 选择器语法

选择器是一系列简单的选择器，由组合器分隔。选择器不区分大小写（包括针对元素、属性和属性值）。

当没有提供元素选择器时，通用选择器 (*) 是隐式的（即 *.header 和 .header 是等价的）。

## 选择器

| 模式                    | 匹配                                         | 例子                                                            |
|-----------------------|--------------------------------------------|---------------------------------------------------------------|
| *                     | 任何元素                                       | *                                                             |
| tag                   | 具有给定标记名称的元素                                | div                                                           |
| *                     | E                                          | 任何命名空间（包括非命名空间）中 E 类型的元素                                      |
| ns                    | E                                          | 命名空间 ns 中 E 类型的元素                                             |
| #id                   | 属性 ID 为"id"的元素                             | div#wrap,#​​​​logo                                            |
| .class                | 类名为"class"的元素                              | div.left,.result                                              |
| [attr]                | 属性名为"attr"的的元素（具有任何值）                      | a[href],[title]                                               |
| [^attrPrefix]         | 属性名称以"attrPrefix"开头的元素。用于查找具有 HTML5 数据集的元素 | [data-],div[data-]                                            |
| [attr=val]            | 属性名为"attr"且值等于"val"的元素                     | img[width=500],a[rel=nofollow]                                |
| [attr="val"]          | 属性名为"attr"且值等于"val"的元素                     | span[hello="Cleveland"][goodbye="Columbus"],a[rel="nofollow"] |
| [attr^=valPrefix]     | 属性名为"attr"且值以"valPrefix"开头的元素              | a[href^=http:]                                                |
| [attr$=valSuffix]     | 属性名为"attr"且值以"valSuffix"结尾的元素              | img[src$=.png]                                                |
| [attr*=valContaining] | 元素，属性名为"attr"，值包含"valContaining"           | a[href*=/search/]                                             |
| [attr~=regex]         | 元素，其属性名为"attr"，值与正则表达式匹配                   | img[src~=(?i)\\.(png                                          |
|                       | 以上内容可以按任何顺序组合                              | div.header[title]                                             |

## 关系选择器

|模式|匹配|例子|
| :--------------------| :-------------------------| :-----------------------|
|E F|从 E 元素衍生的 F 元素|div a,.logo h1|
|E > F|E 的 F 直系子项|ol > li|
|E + F|紧靠同级 E 的 F 元素|li + li,div.head + div|
|E ~ F|前面有同级 E 的 F 元素|h1 ~ p|
|E, F, G|所有匹配的元素 E、F 或 G|a[href], div, h3|

## 伪选择器

|模式|匹配|例子|
| :----------------------------| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|:lt(n)|同级指数小于n的元素|td:lt(3)查找每行的前 3 个单元格|
|:gt(n)|同级索引大于n的元素|td:gt(1)跳过前两个后查找单元格|
|:eq(n)|同级指数等于n的元素|td:eq(0)查找每行的第一个单元格|
|:has(selector)|包含至少一个与选择器匹配的元素的元素|div:has(p)查找包含元素的 。选择至少具有一个直接子元素的元素。divpdiv:has(> a)diva|
|:not(selector)|与选择器不匹配的元素。参见[Elements.not（String）](https://jsoup.org/apidocs/org/jsoup/select/Elements.html#not(java.lang.String))|div:not(.logo)查找没有“.logo”类的所有 div。div:not(:has(div))查找不包含 div 的 div。|
|:contains(text)|元素，包含指定的文本。搜索不区分大小写。文本可能出现在找到的元素或其任何后代中。文本是空格规范化的。要查找包含括号的内容，请转义带有 \.|p:contains(jsoup)查找包含文本 "jsoup" 的 p 元素。p:contains(hello \(there\)查找包含文本“Hello (There)”的 p 的元素|
|:containsOwn(text)|元素，直接包含指定的文本。搜索不区分大小写。文本必须出现在找到的元素中，而不是其任何后代中。|p:containsOwn(jsoup)查找带有自己的文本"jsoup"的 p 元素。|
|:containsData(data)|包含指定数据的元素。 script 和 style 元素以及 comment 节点（等）的内容被视为数据节点，而不是文本节点。搜索不区分大小写。数据可能出现在找到的元素或其任何后代中。|script:containsData(jsoup)查找包含数据"jsoup"的脚本元素。|
|:containsWholeText(text)|包含指定非规范化文本的元素。搜索区分大小写，并将与原始输入中的空格和换行符完全匹配。文本可能出现在找到的元素或其任何后代中。要查找包含括号的内容，请使用 \ 将其转义。|p:containsWholeText(jsoup\nThe Java HTML Parser) 找到包含文本 "jsoup\nThe Java HTML Parser" 的 p 个元素（而不是像 :contains() 那样的其他空格或大小写变体。请注意， br 元素显示为换行符。|
|:containsWholeOwnText(text)|直接包含指定非规范化文本的元素。搜索区分大小写，并将与原始输入中的空格和换行符完全匹配。文本可能会出现在找到的元素中，但不会出现在其后代中。要查找包含括号的内容，请使用 \ 将其转义。|p:containsWholeOwnText(jsoup\nThe Java HTML Parser) 查找直接包含文本 "jsoup\nThe Java HTML Parser" 的 p 元素（而不是像 :contains() 那样包含空格或大小写的其他变体。请注意， br 元素显示为换行符。|
|:matches(regex)|包含与指定正则表达式匹配的空格规范化文本的元素。文本可能出现在找到的元素或其任何后代中。|td:matches(\\d+) 查找包含数字的表格单元格。 div:matches((?i)login) 查找包含文本的 div，不区分大小写。div:matches(^text$) 完全匹配|
|:matchesWholeText(regex)|包含与指定正则表达式匹配的非规范化整个文本的元素。文本可能出现在找到的元素或其任何后代中。|td:matchesWholeText(\\s{2,})查找至少包含两个空格字符的表单元格。|
|:matchesWholeOwnText(regex)|其自己的非规范化全文与指定的正则表达式匹配的元素。文本必须出现在找到的元素中，而不是其任何后代中。|td:matchesWholeOwnText(\n\\d+)查找直接包含新线后面的数字的表格单元格。|
||以上可以按任何顺序与其他选择器组合|.light:contains(name):eq(0)|
|:matchText|将文本节点视为元素，因此允许您匹配和选择文本节点。请注意，使用此选择器会修改 DOM，因此您可能需要在使用前 clone 您的文档。|输入 `<p>One<br />Two</p>` p:matchText:first-Child 将返回带有文本"One"的[伪文本元素](https://jsoup.org/apidocs/org/jsoup/nodes/PseudoTextElement.html)。|

## 结构伪选择器

|模式|匹配|例子|
| -------------------------| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---------------------------------------------------------------------------------------------------|
|:root|作为文档根目录的元素。在 HTML 中，这是元素html|:root|
|:nth-child(an+b)|文档树中前面有同级元素的元素，对于 的任何正整数或零值，并且具有父元素。对于大于零的值，这有效地将元素的子元素划分为一组元素（最后一组取余数），并选择每个组的第b个元素。例如，这允许选择器对表格中每隔一行进行寻址，并可用于以四个周期替换段落文本的颜色。和值必须是整数（正、负或零）。元素的第一个子元素的索引为 1。an+b-1nabab除此之外，可以代替和作为参数。 与 具有相同的含义，并且与 具有相同的含义。:nth-child()oddevenodd2n+1even2n|tr:nth-child(2n+1)查找表的每个奇数行nth-child(10n-1) ​第 9, 19, 29 等元素<br/>li:nth-child(5) 第5个li|
|:nth-last-child(an+b)|在文档树中具有同级元素的元素。否则喜欢an+b-1:nth-child()|tr:nth-last-child(-n+2)表的最后两行|
|:nth-of-type(an+b)|伪类表示法表示一个元素，该元素在文档树中具有具有相同扩展元素名称的同级元素，对于 n 的任何零或正整数值，并且具有父元素an+b-1|img:nth-of-type(2n+1)|
|:nth-last-of-type(an+b)|伪类表示法表示一个元素，该元素在文档树中具有具有相同扩展元素名称的同级元素，对于 n 的任何零或正整数值，并且具有父元素an+b-1|img:nth-last-of-type(2n+1)|
|:first-child|元素是某个其他元素的第一个子元素。|div > p:first-child|
|:last-child|元素是某个其他元素的最后一个子元素。|ol > li:last-child|
|:first-of-type|元素是其父元素的子元素列表中其类型的第一个同级元素|dl dt:first-of-type|
|:last-of-type|元素是其父元素的子元素列表中其类型的最后一个同级元素|tr > td:last-of-type|
|:only-child|具有父元素且父元素没有其他元素子元素的元素||
|:only-of-type|具有父元素且父元素没有具有相同扩展元素名称的其他元素子元素的元素||
|:empty|没有子元素的元素||
