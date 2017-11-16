# GradlePublishing

如何将自己的项目发布到Bintray？

# 背景

```groovy
compile 'xxxxx:xxxx:xx'
```

经常在Android开发中会遇到这个，这个怎么来的呢？

其实这个和iOS的COCOAPODS是差不多性质的东西。

很多时候，我们希望能把本地项目发布到仓库中，让其他人使用。Bintray是一个很好的远程仓库。

网上有很多例子教你如何发布，但是本萌升级到Gradle4.0之后，发现那些例子都不能用了。而且网上无非都是需要借助第三方的插件，比如需要“android-maven-gradle-plugin”外加Bintray的插件等，其实根本不需要什么别的插件，只要Bintray的插件就可以了。

# 本项目使用方法

## Step 1.

打开最外层总工程的build.gradle，在其中加上bintray插件。

```groovy
buildscript {
    repositories {
        jcenter()

//        maven {
//            url uri('./repo')
//        }
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.2'
//        classpath "com.meiyou.framework.gradle.plugin:my-deploy:1.0.4"
//加上下面这个
       classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.7.3'
//        classpath 'homhomlin.lib:lkdbhelper-compiler:1.0.5'
    }
}
```

## Step 2.

在你需要发布项目中的build.gradle中最下面写上

如果要打JAR请用:
```groovy
apply from: 'https://raw.githubusercontent.com/HomHomLin/GradlePublishing/master/p.gradle'
```
这是来自我github远程仓库的脚本。

如果是打AAR请用：

```groovy
apply from: 'https://raw.githubusercontent.com/HomHomLin/GradlePublishing/master/android.gradle'
```

## Step 3.

在需要发布的项目中添加一个gradle.properties文件，如果已经存在就直接在这个文件中写内容。

```groovy
#你的Groupid
GROUP_ID=homhomlin.lib
#你的artifactid
POM_ARTIFACT_ID=lkdbhelper-compiler
#你的deployversion
DEPLOY_VERSION=1.0.6
#你要发布的类型，jar和aar可选
PACKAGE_FORMAT=jar
#项目名字
PROJ_NAME=lkdb
PROJ_VCSURL=https://github.com/HomHomLin/LKDBHelper-ORM-Android.git
PROJ_WEBSITEURL=https://github.com/HomHomLin/LKDBHelper-ORM-Android
PROJ_ISSUETRACKERURL=
PROJ_DESCRIPTION=/LKDBHelper-ORM-Android

DEVELOPER_ID=homhomlin
DEVELOPER_NAME=linhonghong
DEVELOPER_EMAIL=linhh90@163.com
```

## Step 4.

在工程最外层的local.properties中写上你的bintray账户信息，这个不需要我教了吧？

```groovy
BINTRAY_KEY=你的Bintray的Apikey
BINTRAY_USER=你的User名
```

## Step 5.

最后在控制台输入

```xml
gradle :你的项目名:bintrayUpload
```
然后到bintray申请下include就好了。

# PS

本工程适用于Gradle 3.x+
