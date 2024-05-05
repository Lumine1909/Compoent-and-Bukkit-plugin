# 获取NMS中的ItemStack

与一般的 BukkitAPI 不同，通过实例化产生的 `ItemStack` 并不是封装过的 `CraftItemStack`。当这个 `ItemStack` 被放入物品栏时，才通过 `CraftItemStack.asNMSCopy` 转换为 `NMS ItemStack`。而在调用 `Inventory.getItem` 时，`NMS ItemStack` 通过 `CraftItemStack.asCraftMirror` 转换为了 `CraftItemStack`

```java
// CraftItemStack.asNMSCopy
public static net.minecraft.world.item.ItemStack asNMSCopy(ItemStack original) {
    if (original instanceof CraftItemStack) {
        CraftItemStack stack = (CraftItemStack) original;
        return stack.handle == null ? net.minecraft.world.item.ItemStack.EMPTY : stack.handle.copy();
    }
    if (original == null || original.isEmpty()) { // Paper - override isEmpty to use vanilla's impl; use isEmpty
        return net.minecraft.world.item.ItemStack.EMPTY;
    }

    Item item = CraftMagicNumbers.getItem(original.getType(), original.getDurability());

    if (item == null) {
        return net.minecraft.world.item.ItemStack.EMPTY;
    }
        
    net.minecraft.world.item.ItemStack stack = new net.minecraft.world.item.ItemStack(item, original.getAmount());
    if (original.hasItemMeta()) {
        CraftItemStack.setItemMeta(stack, original.getItemMeta());
    }
    return stack;
}

// CraftItemStack.asCraftMirror
public static CraftItemStack asCraftMirror(net.minecraft.world.item.ItemStack original) {
    return new CraftItemStack((original == null || original.isEmpty()) ? null : original);
}
```



因此，我们不能直接将 `ItemStack` 强制转换为 `CraftItemStack` 获取它的 `handle`， 而是需要通过上述的方法进行转换：

```java
// Bukkit ItemStack to NMS ItemStack
ItemStack is = ...
net.minecraft.world.item.ItemStack nmsIs = CraftItemStack.asNMSCopy(is);
        
// NMS ItemStack to Bukkit ItemStack
net.minecraft.world.item.ItemStack nmsIs = ...
ItemStack is = CraftItemStack.asCraftMirror(nmsIs);
```

