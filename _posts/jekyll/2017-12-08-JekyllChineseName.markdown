---
layout: default
title:  "Jekyll-读取不了中文名称的博客文章!"
excerpt:  "Jekyll模板读取不了中文名称的博客文章!"
author: treeice
categories: posts jekyll
---
### 问题:
> jekyll在本地预览自己写的博客无法正常打开，而提交到github上却可以正常解析。比对文件写的博客是一样的

### 原因:
> 本地博客的markdown文件使用了中文文件名，jekyll无法正常解析出现乱码。 

### 解决方案:
> -  修改安装目录\Ruby22-x64\lib\ruby\2.2.0\webrick\httpservlet里面的的filehandler.rb文件，建议先备份。

> - 找到下列两处，添加一句（**“+“开头的一行为添加部分**）

> - 第一处位置:

    path = req.path_info.dup.force_encoding(Encoding.find("filesystem"))
    + path.force_encoding("UTF-8") # 加入编码
    if trailing_pathsep?(req.path_info)

> - 第二处位置:

    break if base == "/"
    + base.force_encoding("UTF-8") #加入編碼
    break unless File.directory?(File.expand_path(res.filename + base))


