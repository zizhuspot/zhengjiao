# Ya的博客

> 欢迎来到Ya的博客！在这里，让我们一起探寻未知领域，包括加密货币、技术、科学、文化、产品、大事件、人工智能、旅游、美食等等。我的目标是为读者提供有趣、有用、有启发性的内容，自我成长，一起开启新视界。

## 关于页面

关于页面的内容在 `source/about/index.md` 文件中，你需要修改其中的内容。

## 新增文章

> 这里保存之后就会发布到网站，所以建议在 mdnice 写好之后再上传。

1. 在 `source/_posts` 目录下新建一个 `markdown` 文件，文件名格式为 `英文标题.md`，例如 `hello-world.md`。
2. 在 `markdown` 文件头部添加如下内容：
    ```md
    ---
    title: 标题
    date: 发布时间（格式：2023-07-17 20:00:00）
    categories:
      - 类别
    tags:
      - 标签1
      - 标签2
    description: 描述
    cover: 封面图片（可选，没有请删掉这一行）
    ---
    ```

## 新增友链

在 `source/_data/link.yml` 文件中，按照格式新增友链即可。

## 站点信息修改

如果你对默认生成的站点信息不满意，可以在 `config.yml` 文件中修改：

```yml
title: Ya的博客
subtitle: 探索未知的领域、开启新视界
description: 欢迎来到Ya的博客！在这里，让我们一起探寻未知领域，包括加密货币、技术、科学、文化、产品、大事件、人工智能、旅游、美食等等。我的目标是为读者提供有趣、有用、有启发性的内容，自我成长，一起开启新视界。
keywords:
# 作者名称，会显示在侧边栏
author: ZJ
```

侧边栏作者信息栏的描述可以在 `_config.butterfly.yml` 文件中修改：

```yml
card_author:
  description: 探索未知的领域、开启新视界
```

公告也可以在 `_config.butterfly.yml` 文件中修改：

```yml
card_announcement:
  content: A simple and elegant blog
```

社交信息修改也是在 `_config.butterfly.yml` 文件中修改：

```yml
social:
  fas fa-envelope: mailto:luozhu2021@gmail.com || Email || '#4a7dbe'
  fab fa-twitter: https://twitter.com/luozhu2021 || Twitter || '#00acee'
```

## 更换图片

默认的头图和封面图可能不适合你，这些都在 `_config.butterfly.yml` 文件中：

```yml
# 首页 banner 图片
index_img: https://cdn.jsdelivr.net/gh/youngjuning/images@main/1689604945346.png

# 页面默认头图
default_top_img: https://s2.loli.net/2023/07/17/leDBhzw8xEnOmS6.png

# 归档页面默认头图
archive_img: https://s2.loli.net/2023/07/17/xoflNAZpqPTFKU9.png

# 标签页默认头图
tag_img: https://s2.loli.net/2023/07/17/wvkgLUtdju3hYqr.png

# 分类页默认头图
category_img: https://s2.loli.net/2023/07/17/i8TsAaOQYEj1kIv.png

cover:
  # 文章页默认封面（随机）
  default_cover:
    - https://s2.loli.net/2023/07/17/9JQuLefqURI7DYi.png
    - https://s2.loli.net/2023/07/17/qkCs3dgYblAB7ar.png
    - https://s2.loli.net/2023/07/17/XvsoykKqNSQbBUj.png
    - https://s2.loli.net/2023/07/17/mnMagitJQlyNfHk.png
    - https://s2.loli.net/2023/07/17/UShtHMTzDNAblBV.png
    - https://s2.loli.net/2023/07/17/sHCFR6fanbPMwpD.png
    - https://s2.loli.net/2023/07/17/tjNbDh17cTQiJMB.png
    - https://s2.loli.net/2023/07/17/eS6iXfpscLyUhVC.png
```

## 本地运行

> 推荐 github 在线编辑，如果你本来就会用 git，那可以尝试本地运行。

```sh
# 克隆仓库
$ git clone https://github.com/zizhuspot/zhengjiao.git
# 安装依赖
$ yarn install
# 运行
$ yarn server
```

## 学习资源

- [GitHub 快速入门](https://docs.github.com/zh/get-started/quickstart)
- [猴子都能看懂的GIT入门](https://backlog.com/git-tutorial/cn/)
