---
title: hugo + github + netlify构建blog
date: 2024-03-18T16:24:21+08:00
draft: false
categories: ["hugo"]
tags: ["hugo","github","netlify"]
cover: 
    image: img/cover1.jpg
    alt: 'single girl'
    caption: 'single girl'
---


# 一、安装
安装hugo (windows)
```
winget install Hugo.Hugo.Extended

```
其他的根据官网安装
```bash
hugo version 

//hugo v0.123.8-5fed9c591b694f314e5939548e11cc3dcb79a79c+extended windows/amd64 BuildDate=2024-03-07T13:14:42Z VendorInfo=gohugoio 成功
```

git安装略过

# 二、创建页面
```bash
hugo new site test --format yaml
```
安装主题 （其他的可以自己试，根据文档设置，主题[官网](https://themes.gohugo.io/)）
```bash
git clone https://github.com/adityatelange/hugo-PaperMod themes/PaperMod --depth=1
```
编辑hugo.yaml 添加 `theme=PaperMod`

添加第一篇文章
`hugo new posts/first.md`
注意：自动生成的md文件中 draft 默认为true，改成false
建议不使用，因为我设置的是yaml，创建一个yaml格式的更好用
```md
---
title: "First"
date: 2022-12-22T08:39:46+08:00
draft: false
tags: ['html','css']
categories: ['frontend']
cover: 
    image: img/cover1.jpg
    alt: 'single girl'
    caption: 'wow'
---

# hello!!! welcome to my blog
```


```bash
hugo server 
# 页面启动
```

添加参数
```yaml
params:
  homeInfoParams:
    Title: "欢迎"
    content: "keep moving"
  socialIcons:
    - name: github
      url: "https://github.com/"
  showBreadCrumbs: true
  showReadTime: true
  # showShareButtons: true
  showPostNavLinks: true
  hideFooter: true
  hideFooter: true

menu:
  main:
    - identifier: categories
      name: 目录
      url: /categories/
      weight: 10
    - identifier: tags
      name: 标签
      url: /tags/
      weight: 20
    - identifier: archives
      name: archives
      url: /archives/
      weight: 30
    - identifier: about
      name: 关于
      url: /about/
      weight: 40
```

设置about、categories 界面
content文件夹下创建md文件about.md、archives.md，格式如下
```md
about
---
title: 'About'
layout: 'about'
url: '/about/'
---
archives
---
title: 'archives'
layout: 'archives'
url: '/archives/'
summary: archives
---
```

创建.gitmodules文件，可以自动更新主题
```
[submodule "themes/PaperMod"]
path = "themes/PaperMod"
url = "https://github.com/adityatelange/hugo-PaperMod" 
```



```bash
hugo server # 本地预览
```
效果如下![[Pasted image 20240318154807.png]]

# 三、netlify

创建账号，利用github登录，导入GitHub。

添加
![[Pasted image 20240318153337.png]]
选择![[Pasted image 20240318153400.png]]
点击github，导入


选择需要的源仓库，设置参数，设置自己的网站名字，其他如下：

![[Pasted image 20240318153644.png]]


生成
![[Pasted image 20240318154037.png]]
这个时候还不能生成完整的页面，修改cofig.yml
```yml
baseUrl: 'https://youwebname.netlify.app' 
```
提交修改，netlify会自动重新构建，等构建完成，点击预览如下。
![[Pasted image 20240318154234.png]]

# 五、绑定自己购买的域名

我购买的是腾讯云的域名，以此为例，其他的自己Google。

进入控制台，点击域名解析
![[Pasted image 20240318154534.png]]
马赛克处填入刚才的netlify生成的网址，比如我的填入`youwebname.netlify.app`，上下都修改。等待解析生效，一般不超过48个小时。

等到解析完成，直接输入你的域名，over!