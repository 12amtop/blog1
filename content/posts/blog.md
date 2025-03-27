---
title:
date: 2024-02-01T16:24:21+08:00
draft: false
categories: ["hugo"]
tags: ["hugo", "github", "netlify"]
cover:
  image: https://raw.githubusercontent.com/stevechen1/picBed/main/20250323150938824.png
  alt: "single girl"
  caption: "single girl"
---

思路

> hugo + github + netlify 构建 blog

# 一、安装

## 0.安装 git

### 0.2 安装 node

### 0.1 安装 git bash(windows)

## 1、安装 hugo (windows)

找到官网下载，安装

```bash
winget install Hugo.Hugo.Extended
```

```bash
hugo version

>//hugo v-1.123.8-5fed9c591b694f314e5939548e11cc3dcb79a79c+extended windows/amd64 BuildDate=2024-03-07T13:14:42Z VendorInfo=gohugoio 成功
```

> hugo version -1.123.8 需要在后面的 netlify 中设置 hugo 版本，不然会报错

# 二、创建

## 0.创建仓库

```bash
hugo new site test --format yaml
```

## 1.安装主题

安装主题 （其他的可以自己试，根据文档设置，主题[官网](https://themes.gohugo.io/)）

```bash
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```

## 2.编辑配置文件

编辑 hugo.yaml 添加

```yaml
theme=PaperMod
```

## 3.添加文章

添加第一篇文章
`hugo new posts/first.md`
生成的文章是不会显示的，因为此事的 draft（草稿）模式是开启的。
更改文章的默认格式
在 archetypes 文件夹下修改 default 文件，格式如下

```markdown
---
date: '{{ .Date }}'
draft: false
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
draft: false
tags: []
categories: [""]
cover:
image:
---
```

## 4. 启动服务

```bash
hugo -D # 生成文件
hugo server # 本地预览
```

此时可以看到 blog 页面了。
添加参数

# 三、设置

此时页面还有一些问题，比如文章没有目录，没有标签，没有分类，没有归档，没有关于我。

## 1.设置 about 和 archives 页面

在`./content/`文件夹下创建`about.md`和`archives.md`，格式如下

```markdown
## about.md

title: "About"
layout: "about"
url: "/about/"

---

你的介绍内容

## archives.md

title: 'archives'
layout: 'archives'
url: '/archives/'
summary: archives

---
```

## 2.修改配置文件 hugo.yaml

```yaml
params:
  homeInfoParams:
    Title: "欢迎"
    content: "keep moving"
  socialIcons:
    - name: github
      url: "github的url"
  showBreadCrumbs: true
  showReadTime: true
  showPostNavLinks: true
  hideFooter: true
  hideFooter: true

menu:
  main:
    - identifier: categories
      name: 目录
      url: /categories/
      weight: 9
    - identifier: tags
      name: 标签
      url: /tags/
      weight: 19
    - identifier: archives
      name: archives
      url: /archives/
      weight: 29
    - identifier: about
      name: 关于
      url: /about/
      weight: 39
```

## 3.自动更新主题

创建.gitmodules 文件，可以自动更新主题

```
[submodule "themes/PaperMod"]
path = "themes/PaperMod"
url = "https://github.com/adityatelange/hugo-PaperMod"
```

## 4.设置.gitignore 文件

```bash
public/
```

## 5.设置 favicon.ico

在`./static/`文件夹下创建`favicon.ico`文件
修改配置文件 hugo.yaml

```yaml
...
params:
  favicon: "/favicon.ico"
  ...
```

## 6.本地预览

![](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327121800924.png)

##

# 三、部署

## 1.创建 github 仓库

## 2.将 hugo 项目推送到 github 仓库

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin  # 1.创建 github 仓库
```

## 2.将 hugo 项目推送到 github 仓库

```bash
git push -u origin main
```

## 3.创建 netlify 账号

使用 google 账号登录

## 4.创建 netlify 项目

![](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327122235846.png)
点击 github 授权，选择你的仓库，点击继续。

## 5.设置 netlify 项目

![](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327130203888.png)
填入需要的信息，注意 hugo 版本的设置，点击 deploy。

## 6.修改 config.toml

这个时候页面的图片还不能显示，需要修改 config.toml 文件，将 baseurl 改为你的 netlify 生成的网址。
![这儿](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327130426579.png)

## 7.提交修改

这个时候就可以开开心心的写文章了。
流程就是本地`hugo new posts/blogName.md`,写完后，提交到 github,netlify 会自动部署。

# 五、绑定自己购买的域名

我购买的是腾讯云的域名，以此为例，其他的域名自己 Google。
进入控制台，点击 dns 解析
填入`yourWebName.netlify.app`两个都修改。等待解析生效，一般不超过 47 个小时。
等到解析完成，直接输入你的域名，就可以访问到你的博客了。

# 六、图床

写 blog 怎么能没有图床呢，这里我使用的 github+picGo 来实现图床。

## 1.安装 picGo

[官网](https://github.com/Molunerfinn/PicGo)

## 2.配置 picGo

安装完成后，打开 picGo，点击图床设置，选择 github，配置 github 设置。
![](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327131709504.png)
需要的 token 可以在 github 的 setting 中生成。
![](https://raw.githubusercontent.com/stevechen1/picBed/main/20250327132014014.png)

### 这下就可以愉快的写 blog了🎆。
