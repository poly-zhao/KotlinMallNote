#### Application & Library

Application 作为应用程序启动, 其build.gradle第一行为 apply plugin: 'com.android.application'

Library 作为库工程被应用  , 其build.gradle第一行为 apply plugin: 'com.android.library'

#### Application & Library的切换

- 在gradle.preporty中定义一个属性xxx, 然后在module的gradle中来切换

```groovy
if(xxx.toBoolean()){
   apply plugin: 'com.android.application'
}else{
	apply plugin: 'com.android.library'
}
```

- 在module/src/main文件夹下新建debug和release文件夹, 然后在module的gradle文件中根据上面的xxx属性来切换mainfest文件  

```groovy
    sourceSets {
        main {
            if (isUserModule.toBoolean()) {
                manifest.srcFile 'src/main/release/AndroidManifest.xml'
            } else {
                manifest.srcFile 'src/main/debug/AndroidManifest.xml'
            }
        }
    }
```

- 在Application的gradle中根据xxx属性 来判断是否引入module, 如果库工程则引入

```groovy
    if (isUserModule.toBoolean()){
        compile project(':UserCenter')
    }
```



### android-extensions

使用方法: 在module的build.gradle中引入插件 `apply plugin:'kotlin-android-extensions'`

使用该插件可以**直接使用xml中id**



### Anko 扩展库

- Anko Commons   

   包含了Intents ([wiki](https://github.com/Kotlin/anko/wiki/Anko-Commons-%E2%80%93-Intents)); Dialogs and toasts ([wiki](https://github.com/Kotlin/anko/wiki/Anko-Commons-%E2%80%93-Dialogs)); Logging ([wiki](https://github.com/Kotlin/anko/wiki/Anko-Commons-%E2%80%93-Logging));  Resources and dimensions ([wiki](https://github.com/Kotlin/anko/wiki/Anko-Commons-%E2%80%93-Misc)).

引入 `compile "org.jetbrains.anko:anko-commons:$anko_version" `, `compile "org.jetbrains.anko:anko-support-v4-commons:$anko_version" `
在根目录gradle中写入版本号

```
buildscript {
    .....
    ext.anko_version = '0.8.2'//手动
    .....
}
```

使用方法说明可以到github上找Anko

跳转Activity

```kotlin
startActivity(intentFor<TestActvity>("id" to 5))// 调用仍是原来的java的方法
startActivity<TestActivity>("id" to 5)//这是一个扩展方法
//泛型为要跳转到的Activity类名

toast("asdkljf") //Context的扩展方法 
```



- Anko Layouts	
- Anko SQLite
- Anko Coroutines