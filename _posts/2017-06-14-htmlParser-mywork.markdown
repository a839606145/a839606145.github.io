---
layout:     post
title:      "htmlParse----解析"
subtitle:   ""
date:       2017-06-14 12:00:00
author:     "lzx"
header-img: "img/post-bg-nextgen-web-pwa.jpg"
header-mask: 0.3
catalog:    true
tags:
    - htmlParse
    - java
---


> 本文来自htmlParse 2.0 api

# TextNode

> textNode 包含了所有的文本类型的节点
> 可以得到js中的方法
> 以及不在tag标签的节点

## 如何得到TextNode

> 使用NodeClassFilter new NodeClassFilter(TextNode.class);

# TagNode

> tagNode 包括我们常见的标签 div a ul li等html标签

##如何得到tagNode

> HasAttributeFilter==根据属性得到

> CssSelectorNodeFilter==使用css选择器得到

> TagNameFilter==根据tagName（div a ul li）等得到

> NodeClassFilter===根据Tag**.Class

> HasParentFilter==根据父节点

> HasChildFilter==根据子节点

> HasSiblingFilter==根据兄弟节点

# 其他说明

# 逻辑过滤器

> 对于复杂的过滤可以使用逻辑过滤器

> OrFilter AndFilter  IsEqualFilter  NotFilter

# 特殊过滤器

> RegexFilter LinkRegexFilter LinkStringFilter StringFilter

# 使用NodeVisitor得到节点

> 解析器会自动地调用visitTag方法，对每个tag进行判断，对需要的进行必要的操作。

	public void visitTag (Tag tag)
		{
			if (tag instanceof LinkTag)
			{
				System.out.println("a ->" + ((LinkTag)tag).extractLink());
			}
			else if (tag instanceof FormTag)
			{
				System.out.println("form ->" + ((FormTag)tag).extractFormLocn());
			}
	}



	









       