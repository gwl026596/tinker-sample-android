# tinker-sample-android
微信Tinker热更新研究
贴上修复这个bug的方法供大家参考：

Execution failed for task ':app:tinkerProcessReleaseResourceId'. > java.io.FileNotFoundException
配置
tinker版本：1.9.14.5
gradle插件版本：3.5.3
gradle版本：5.5
AS 版本：4.0
系统：:mac os
是否使用热更新SDK： 下载tinker sample android

修复：

(1) 关闭R8。gradle.propertiest添加
android.enableR8.libraries=false android.enableR8=false

(2)先clean项目, 然后点file -> invalidate Caches/Restart（我是Mac版 AS）。

(3）打好release包了保存bakApk，clean项目。

(4) 创建app/build 目录，把保存的bakApk 拷贝进来。

(5) 修改build.gradle文件配置（就是"tinkerOldApkPath"、”tinkerApplyMappingPath“、”tinkerApplyResourcePath“三个属性）

(6）AS命令行输入./gradlew tinkerPatchRelease。成功打出增量包

说明：
成功一次之后只需要(3）~(6）就可以了。我解决这个bug的关键步骤是关闭R8和 invalidate Caches/Restart。
