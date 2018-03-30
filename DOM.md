## DOM 相关内容

### Node 类型

1. 每个节点都有一个`nodeType`属性，可以用于判断节点类型，常见节点类型有三种
> Node.ELEMENT_NODE(1)

> Node.ATTRIBUTE_NODE(2)

> Node.TEXT_NODE(3)

2. 每个节点都有`nodeName`、`nodeValue`属性，其值与节点类型有关。
> 对于元素节点，`nodeName`为元素标签名，`nodeValue`为null

3. 节点关系

> `childNodes`/`parentNode`/`previousSibling`/`nextSibling`/`firstChild`/`lastChild`
> `somenode.hasChildNodes()`:判断一个节点下面是否含有子节点

4. 操作节点

> `somenode.appendChild(newnode)`:用于向`somenode`的`childNodes`末尾添加一个节点。如果`newnode`已经是文档的一部分，则将该节点由原来位置移到新位置。 返回新增节点。 

> 'somenode.insertBefore(newnode, refernode)':在`somenode`的`childNodes`中的节点`refernode`前插入`newnode`。返回新插节点。

> `somenode.replaceChild(newnode, oldnode)`:用`newnode`替换`somenode`的`childNodes`中的节点`oldnode`,返回被替换的节点。

> `somenode.removeChild(delnode)`:删除`somenode`的`childNodes`中的节点`delnode`。返回被删除的节点。

> `somenode.cloneNode(bool)`:克隆节点`somenode`

5. 查找元素

> `someElement.getElementById("id")`;

> `someElement.getElementsByName("name")`;

> `someElement.getElementsByTagName("tagname")`

6. 查找特性

> `someElement.getAttribute("attr")`

7. 设置特性

> `someElement.setAttribute("attr", "value")`

8. 创建元素
> `document.createElement("tagname")`

9. 创建元素节点

> `document.createTextNode("string")`
