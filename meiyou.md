# 美柚通用开源脚本

如何将自己的项目发布到美柚开源Bintray？

# 本项目使用方法

## Step 1.

打开最外层总工程的build.gradle，在其中加上bintray插件。

```groovy
buildscript {
    repositories {
        jcenter()
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.2'
		//加上下面这个
       classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.7.3'
    }
}
```

## Step 2.

在你需要发布项目中的build.gradle中最下面写上

```groovy
apply from: 'https://raw.githubusercontent.com/HomHomLin/GradlePublishing/master/meiyou.gradle'
```
这是来自我github远程仓库的脚本。

## Step 3.

在需要发布的项目中添加一个gradle.properties文件，如果已经存在就直接在这个文件中写内容。

```groovy
#你的artifactid
POM_ARTIFACT_ID=lkdbhelper-compiler
#你的deployversion
DEPLOY_VERSION=1.0.6
#你要发布的类型，jar和aar可选
PACKAGE_FORMAT=jar
```

鉴于目前我们基本上都是AAR打包模式，都有这个配置文件，这个配置甚至不需要改。

## Step 4.

在工程最外层的local.properties中写上美柚的bintray账户信息。

```groovy
BINTRAY_KEY=美柚的Bintray的Apikey
BINTRAY_USER=美柚的User名
```

## Step 5.

最后在控制台输入

```xml
gradle :你的项目名:bintrayUpload
```
然后到bintray申请下include就好了。

