# cn.eckystudio.m Android 类库

cn.eckystudio.m 是一组面向 Android 应用的 Java 通用组件与工具代码，包含网络请求和数据模型、常用 UI 控件、文件辅助方法、文本转语音、日志及 RSA 签名等。源码包名为 cn.eckystudio.m。

这是一个较早期的 Android 类库仓库，适合作为旧项目的代码参考；接入新项目之前，建议先检查 API 兼容性、依赖版本和安全实现。

## 功能概览

| 包 | 内容 |
| --- | --- |
| ai | 基于 Android TextToSpeech 的文本朗读封装 TTSEngine |
| base | 单参数和双参数回调接口 Action、Action2 |
| common | 泛型键值对 KeyValuePair |
| file | 从 Uri 获取文件路径，以及文件遍历辅助方法 |
| log | 简单日志输出与对象信息辅助工具 |
| security | RSAUtils 提供 SHA256WithRSA 签名方法 |
| ui | 图片文字控件、覆盖容器、分页标题栏、箭头动画、悬浮窗、屏幕信息与常用颜色 |
| ui.vpi | ViewPager 的圆点、线条、下划线、图标、标签和标题指示器 |
| web | 基础 HTTP 请求封装，JSON/XML 请求与响应模型，JSON 序列化、解析及对象映射辅助方法 |
| res | 自定义控件使用的属性、样式、颜色和图形资源 |

仓库还包含 doc 目录中的资源命名和 XML 图标制作笔记。

## 工程配置

仓库使用 Android Gradle Plugin 的 Android Library 插件，当前 build.gradle 声明了以下配置：

- Android Gradle Plugin：4.2.0-alpha02
- compileSdkVersion：25
- buildToolsVersion：27.0.3
- minSdkVersion：16
- AndroidX AppCompat：1.0.2

这是一个历史配置。仓库没有 Gradle Wrapper、settings.gradle、演示应用或测试目录，因此不能仅凭当前仓库内容保证在新环境中直接构建。源码还引用 androidx.core 和 androidx.viewpager；当前 build.gradle 未显式声明 ViewPager 依赖。若要作为独立 Gradle 模块构建，需要准备兼容的 Gradle、JDK 和 Android SDK，并核对、补全对应 AndroidX 依赖。

## 使用前注意

- HttpClient 使用 HttpURLConnection 同步发起网络请求。不要在 Android 主线程直接调用；应在工作线程执行，并在应用层处理超时、错误响应和重试。
- TTSEngine 依赖设备上的 Android 文本转语音服务。使用前应确认初始化完成，并在不再需要时释放资源。
- FileUtils 的 Uri 转路径行为可能受 Android 版本、存储权限和内容提供方影响。新应用应优先使用 ContentResolver 读取 Uri，而不是假定所有 Uri 都对应可访问的文件路径。
- RSAUtils 当前提供私钥签名实现；密钥应安全保存，算法与编码须和服务端约定一致。
- 仓库根目录没有统一的 LICENSE 文件。源码中如有单独版权或许可证声明，应按各文件声明处理；公开复用或分发前请确认授权范围。

## 目录结构

~~~text
src/main/java/cn/eckystudio/m/   Java 类库源码
src/main/res/                    Android 控件及样式资源
src/main/AndroidManifest.xml     类库 Manifest
doc/                             开发笔记
build.gradle                     Android Library 构建配置
~~~