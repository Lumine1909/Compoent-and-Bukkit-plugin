# Paperweight 示例

打开 Idea，新建项目，选择 new project，JDK 21， Build system 选择 Gradle，使用 Kotlin 作为 DSL，并保证 Gradle 版本在 8.5 及以上

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>



等待右下角的初始化进度条完成后，打开 build.gradle.kts，它应该是这样的：

```kotlin
plugins {
    id("java")
}

group = ***YOUR GROUP NAME***
version = "1.0-SNAPSHOT"

repositories {
    mavenCentral()
}

dependencies {
    testImplementation(platform("org.junit:junit-bom:5.9.1"))
    testImplementation("org.junit.jupiter:junit-jupiter")
}

tasks.test {
    useJUnitPlatform()
}
```

根据文档所写添加内容：

```kotlin
plugins {
    id("java")
    id("io.papermc.paperweight.userdev") version "1.6.3"
}

group = ***YOUR GROUP NAME***
version = "1.0-SNAPSHOT"

repositories {
    mavenCentral()
}

dependencies {
    testImplementation(platform("org.junit:junit-bom:5.9.1"))
    testImplementation("org.junit.jupiter:junit-jupiter")
    paperweight.paperDevBundle("1.20.5-R0.1-SNAPSHOT")
}

tasks.test {
    useJUnitPlatform()
}
```

按下 Load Gradle Changes，等待加载完成就可以使用了

接着创建插件主类和plugin.yml，完成后按 Alt+F12 打开终端，输入

```
gradle clean build // Paper 1.20.5 +
gradle clean build reobfJar // Spigot 1.20.5
```

按下 Ctrl+Enter，构建完成的 Jar 文件就在 ./build/libs 文件夹了

如果你成功构建了插件并在服务端中正确加载，我们就可以进行下一步了：使用NMS
