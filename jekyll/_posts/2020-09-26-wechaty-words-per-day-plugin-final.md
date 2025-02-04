---
title: "暑期2020 [编写一个“每日一句”插件] 结项报告"
author: univerone
categories: project
tags:
  - plugins
  - summer-of-wechaty
  - summer-2020
  - entertainment
image: /assets/2020/wechaty-words-per-day-plugin-final/logo.png
---

- 项目名称：编写一个“每日一句”插件
- 方案描述：
  - 制作可以被 wechaty 调用的插件，能够使用内置的语料接口
  - 插件能够构造 POST 和 GET 请求，设置请求参数，并根据指定的解析规则解析返回的 json 格式或者 html 格式的内容
  - 插件可以根据请求结构中的图片地址下载图片，并根据每日一句内容以及微信群的相关信息添加水印
  - 插件能够设置定时发送的时间、群名、发送的内容
- 时间规划：
  - 开发插件的基本框架
    - 7/1 - 7/21
    - 插件的输入参数有：使用的内置 API 接口名称、应用的群聊名称以及发布每日一句内容的时间，完成基本代码构建。插件能够设置定时发送的时间、群名、发送的内容，也可以根据请求结构中的图片地址下载图片，并根据每日一句内容以及微信群的相关信息添加水印。
  - 发布 NPM 包，引入 CI/CD
    - 7/22 - 8/14
    - 进一步优化代码以及注释，引入 CI/CD 来进行代码质量控制以及包的版本管理
  - 丰富语料库
    - 8/15 - 9/07
    - 首先确定使用的 API 接口或者爬取的网址，根据不同的网址进行不同的解析，返回指定的结果。构造请求并解析内容，返回需要的字符串（每日一句的内容或者图片的 URL）。如有余力的话，能够支持用户自主设定语料的来源。
  - 进行测试完善项目文档
    - 9/07 - 10/01
    - 完善项目文档，撰写整个项目过程的总结文章;增加单元测试等;计划延迟的缓冲时间

## 项目总结

- 项目成果：
  - 项目仓库位于: <https://github.com/univerone/words-per-day>
  - 相应的npm package地址为: <https://www.npmjs.com/package/words-per-day>
  - live coding视频:
  {% include iframe.html src="https://player.bilibili.com/player.html?bvid=BV1ih411d75h" %}
  - PPT展示视频:
  {% include iframe.html src="https://player.bilibili.com/player.html?bvid=BV1pf4y1D71F" %}
  - PPT:
  {% include iframe.html src="/assets/2020/wechaty-words-per-day-plugin-final/presentation.pdf" %}

- 遇到的问题及解决方案：
  - **编程语言的不熟悉**. 由于之前没有接触过typescript语言,在项目前期, 我对于整个项目的具体实现包括项目文件的组成结构都没有经验, 所以刚开始比较难着手, 解决方法是多参考社区内其它以typescript为主要编程语言的项目, 结合官方文档和教程, 总结出使用wechaty社区的规范从0发布一个npm package的流程, 据此来组织我的代码. 在具体的编程实现上, 我也参考了很多javascript的语法(尤其是MDN Web文档). 此外看到很多项目都有vscode配置文件夹,在项目一开始我就学习使用vscode进行开发, 到后面觉得十分趁手,也算是"真香"了.
  - **回调函数的问题**. 在编写这个插件的过程中，有很多需要等待一定时间来完成的步骤，比如图片的下载保存等，如果不进行设置的话一些过程是异步执行的，如果想在这个过程结束后进行下一个过程，可以使用回调函数, 然后使用回调函数使得代码的可读性变差, 在查阅相关资料之后, 我选择使用Promise来替代回调函数,  由于Promise/await的语法和逻辑有一点复杂, 可以边看文档边整理重要的概念, 之后回顾的时候也方便理解.
  - **调试代码的问题**. 在开发过程中经常需要查看代码效果, 首先是针对函数的测试, 刚开始我将调用的代码写在对应的ts文件下面, 然后直接运行生成的js文件.后面将多个函数测试的代码单独写在一个ts文件中,  再之后查看插件在微信机器人上运行效果的时候, 我选择在dist目录里面写一个javascript文件, 启动机器人,在 typescript文件对应的行处设置断点进行调试, 这是在发布包之前进行的调试. 在包发布完成之后, 还要在单独的linux服务器上, 创建nodejs项目引入最新的插件查看效果.
  - **图像处理的问题**. 在刚开始每日一句项目的目标就包括生成图片, 而在生成图片工具的选择上我花费了较大时间, 根据参考的项目我使用nodejs包gm来进行图像处理,其基本原理是使用调用系统中安装好的GraphicsMagick或者ImageMagick, 由于文档中说明文件较少, 因此使用这个包来实现预期的显示效果花费了最长的时间. 在项目后期参考其他项目, 是用puppeteer生成截图, 基本原理就是写一个html文档放置预设的样式, 根据传入的参数, 对文档进行编辑, 使用puppeteer生成这个html文档的截图, 相对来说这个方法更加容易入手并且高效, 缺点就是生成图片的速度相对较慢且puppeteer包较大.

## 导师审核

### 评审对象

- 评审内容：*结项报告*
- 提交人：*江姗姗*

### 评审结果

- 项目完成度：*完成不错*
- 学生参与度：*积极参与，独立自主*
- 代码贡献量：*100%*
- 综合评价及建议：*表现远超预期*
- 最终评审结果：“通过”
