# PaperMC, Paper 与 Paperweight Userdev

在继续之前，我们需要完成环境的搭建与相关工具的介绍

在很长一段时间中，NMS的使用伴随着令人困扰的多版本适配问题。NMS不是API，因此几乎每个小版本都会有改动，大范围的改动也不在少数（点名 1.17 更新），因此开发者们找到了两种方法来面对这个问题：反射和分版本实现，但由于 Paper 服务器在 1.20.5 的更新，我们有了更好的解决方法。

Paper 1.20.5 : 放弃混淆，直接使用 Mojang map 名称 [https://forums.papermc.io/threads/important-dev-psa-future-removal-of-cb-package-relocation.1106/](https://forums.papermc.io/threads/important-dev-psa-future-removal-of-cb-package-relocation.1106/)

这意味这我们可以直接使用一套稳定，可读，且易用的名称完成插件的编写。未来，使用NMS将几乎不再产生版本不兼容问题。



Paperweight Userdev

PaperMC 所开发的插件，提供了对NMS的访问

{% embed url="https://docs.papermc.io/paper/dev/userdev" %}

这个插件只能在 Gradle 中使用，但配置并不难，跟随使用文档就很容易完成
