---
coverY: 0
---

# 什么是原生Minecraft



如果你在Bukkit插件这个领域深入研究过，就一定会听过一个词: NMS，它指的是Minecraft服务端的原生类。在 1.17 版本之前，这些类都被spigot放置在 `net.minecraft.server.vX_XX_RX` 下，因此获得了NMS这个名字

1.17 之后spigot服务端更改了混淆方式，现在这些内容都在 `net.minecraft` 包下，打开服务端的 jar 文件你就可以看到它们

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>net.minecraft 包下的内容</p></figcaption></figure>



这些内容是Bukkit系服务端最底层的实现，它包含了大量BukkitAPI未涉及的部分，比如发送数据包与物品nbt（以及 1.20.5 之后的组件）

本部分的第三段（也是重点）就是如何使用NMS来处理物品组件的相关内容

如果你没有接触过这部分内容，建议先查看这篇文章：

{% embed url="https://bdn.tdiant.net/#/unit/5-1" %}
