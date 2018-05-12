### Glide使用

配置

```
如果使用 Gradle，可从 Maven Central 或 JCenter 中添加对 Glide 的依赖。同样，你还需要添加 Android 支持库的依赖。

repositories {
  mavenCentral()
  maven { url 'https://maven.google.com' }
}

dependencies {
    compile 'com.github.bumptech.glide:glide:4.6.1'
    annotationProcessor 'com.github.bumptech.glide:compiler:4.6.1'
}


kotlin
apply plugin: 'kotlin-kapt'
dependencies {
  compile 'com.github.bumptech.glide:glide:4.6.1'
  kapt 'com.github.bumptech.glide:compiler:4.6.1'
}

注意：如果可能，请尽量在你的依赖中避免使用 @aar 。如果你必须这么做，请添加 transitive=true 以确保所有必要的类都被包含到你的 API 中：

dependencies {
    implementation ("com.github.bumptech.glide:glide:4.6.1@aar") {
        transitive = true
    }
}
```



