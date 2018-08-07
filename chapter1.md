* #### as版本小于3.0

需要到_Plugins _里去安装Kotlin插件

* #### as版本3.0及以上

无需再安装Kotlin插件

在app的build.gradle里顶部

```
apply plugin: 'kotlin-android'
```

若需使用android扩展，是一个编译器扩展， 摆脱代码中的`findViewById()`调用

```
apply plugin: 'kotlin-android-extensions'

        ...

dependencies {
        implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
}
```

在project的build.gradle里

```
buildscript {

    ext.kotlin_version = '1.1.51'

    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
```



