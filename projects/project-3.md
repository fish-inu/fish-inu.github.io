---
layout: project
type: project
image: images/omegat-logo.png
title: Pigeon Plugin
permalink: projects/pigeon
# All dates must be YYYY-MM-DD format!
date: 2019-11-15
labels:
  - Java
  - Gradle
  - OmegaT
  - Plugin
summary: 面向 OmegaT 的机器翻译插件
---

翻译实践中，译者利用翻译辅助软件（CAT）大大提高了任务效率，这是由于术语库（Glossary）、翻译记忆库（Translation Memory）以及机器翻译（Machine Translation）接口等的帮助。

其中，在机器翻译方面，在未获得 API Key 的情况下，多数使用者选择前往各大机器翻译网站输入源文档，然而这种方法对较大的翻译项目来说会降低效率。相比之下，翻译辅助软件预先对源文档进行了基于句子的切分，在有机器翻译接口的情况下能够实现句对句对应，之后译者再对其进行编辑，即译后编辑。

本项目使用 Gradle 开发基于 Java 的机器翻译插件，适用于 Omegat。此外，本项目从网页应用角度着手开发，因此可以将该插件视作前端，并与另一提供机翻数据的后端项目结合，实现无 API 情况下的机器翻译。

你可以从[此处](https://github.com/fish-inu/omegat-pigeon-plugin)查看该项目。
