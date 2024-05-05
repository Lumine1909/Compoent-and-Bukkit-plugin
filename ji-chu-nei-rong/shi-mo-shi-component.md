# 什么是Component



（如果你已经对此内容有所了解，可以跳过这部分



作为一个Minecraft的玩家，你或许曾经听说过nbt标签，它存储了一个物品堆(ItemStack, 就是物品栏里的东西) 的数据。nbt标签以JSON格式进行反序列化后看起来是这个样子的：

<pre class="language-json"><code class="lang-json"><strong>// 一个隐形物品展示框
</strong><strong>{id:"minecraft:item_frame",Count:1b,tag:{EntityTag:{Invisible:1b}}}
</strong></code></pre>

实体也通过nbt存储，在这个例子中，我们设置了实体的 Invisible 标签为 true ，即使展示框隐形



而在Minecraft 1.20.5版本中，mojang对这个功能进行了修改，使用物品组件(Component)格式来处理物品，它看起来是这给样子的：

```
// 原版give命令
/give @s minecraft:item_frame[minecraft:entity_data={id:"minecraft:item_frame",Invisible:1b}]

// toString
{minecraft:entity_data=>{id:"minecraft:item_frame",Invisible:1b}, minecraft:max_stack_size=>64, minecraft:lore=>ItemLore[lines=[], styledLines=[]], minecraft:enchantments=>ItemEnchantments{enchantments={}, showInTooltip=true}, minecraft:repair_cost=>0, minecraft:attribute_modifiers=>ItemAttributeModifiers[modifiers=[], showInTooltip=true], minecraft:rarity=>COMMON}
```

看起来改了不少，而且还有大量的新内容，但真的什么都变了吗？



如果你尝试过在新版本使用/data命令获取玩家实体的数据，你可能会看到：

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>/data</p></figcaption></figure>

似乎只是将tag键改成了component，并修改了一些其它的键。也就是说，组件只是表象，更本质的存储还是使用nbt，并且只存储了物品特有的组件的nbt

