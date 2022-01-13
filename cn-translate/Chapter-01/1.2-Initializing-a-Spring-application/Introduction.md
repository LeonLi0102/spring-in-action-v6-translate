## 1.2 初始化 Spring 应用程序

在本书的学习过程中，将创建 Taco Cloud，这是一个在线应用程序，用于订购由真人制作的最美味的食物 - 玉米饼。 当然，将使用 Spring、Spring Boot 以及各种相关的库和框架来实现此目标。

你能找到多个方法去初始化一个Spring应用。尽管我可以指导您逐步完成手动创建项目目录结构和定义构建规范的步骤，但这却浪费了时间，最好花费更多时间编写应用程序代码。因此，将依靠 Spring Initializr 来引导应用程序的创建。

Spring Initializr 既是一个基于浏览器的 Web 应用程序，又是一个 REST API，它们可以生成一个基本的 Spring 项目结构，可以使用所需的任何功能充实自己。 使用 Spring Initializr 的几种方法如下：

* 从 Web 应用程序 [http://start.spring.io](http://start.spring.io) 创建
* 使用 `curl` 命令从命令行创建
* 使用 Spring Boot 命令行接口从命令行创建
* 使用 Spring Tool Suite 创建一个新项目的时候
* 使用 IntelliJ IDEA 创建一个新项目的时候
* 使用 NetBeans 创建一个新项目的时候

我没有在本章中花费数页来讨论这些选项中的每一个，而是在附录中收集了这些详细信息。在本章以及整本书中，将展示如何使用 Spring Tool Suite 中对 Spring Initializr 的支持来创建一个新项目。

顾名思义，Spring Tool Suite 是一个绝佳的 Spring 开发环境，还提供了 Eclipse、Visual Studio Code、Theia IDE 的扩展插件。您可以下载 Spring Tool Suite 的可运行二进制文件，地址：[https://spring.io/tools](https://spring.io/tools)。 Spring Tool Suite 提供了一个方便的 Spring Boot Dashboard 功能，可以在 IDE 中轻松启动、重启和或停止 Spring 应用程序。

如果您不是 Spring Tool Suite 用户，您仍然可以使用相关功能。请跳至附录，选择最适合您的 Initializr 选项代替后续章节中的安装说明。但是您要知道，在本书中，我偶尔还会引用特定于 Spring Tool Suite 的功能，例如 Spring Boot Dashboard。如果您不使用 Spring Tool Suite，则需要调整这些说明以适合您的 IDE。

