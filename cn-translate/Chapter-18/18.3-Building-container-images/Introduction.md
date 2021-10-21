# 18.3 构建容器镜像

在云端部署各种应用程序，Docker 已经成为了事实上的标准 [https://www.docker.com](https://www.docker.com/)。许多不同的云端环境，包括 AWS、Microsoft Azure、Google Cloud Platform 和 Pivotal Web Service（举几个例子），都接受用于部署应用程序的 Docker 容器。

容器化应用程序（如使用 Docker 创建的应用程序）的思想吸引了很多人，这是自真实世界集装箱的类比。集装箱都有一个标准尺寸和格式，无论在其中放什么货物。正因为如此，集装箱很容易堆放在船上，或用火车、卡车来运输。

以类似的方式，容器化应用程序共享一个公共的容器格式，这种格式可以在任何位置部署和运行，而不用考虑其内部的应用程序如何。

从 Spring Boot 应用程序创建镜像的最基本方法是使用 docker build 命令和 Dockerfile 文件。Dockerfile 文件将可执行 JAR 文件从项目构建中复制到容器镜像中。一个极简单的 Dockerfile 如下：

```bash
FROM openjdk:11.0.12-jre
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

Dockerfile 描述了如何创建容器镜像。上面的示例非常简单，让我们逐行进行说明：

* 第 1 行：声明我们创建的镜像，将基于预定义的容器镜像，它提供了 Open JDK11 Java运行时。
* 第 2 行：创建一个变量，该变量引用项目 target 目录中的所有 JAR 文件。对于大多数 Maven 构建项目，其中应该只有一个 JAR 文件。通过使用通配符，可将 Dockerfile 定义与 JAR 文件的名称和版本分离。JAR 文件的路径也假定了 Dockerfile 位于 Maven 项目的根目录中。
* 第 3 行：将 JAR 文件从项目的 target 目录复制到容器镜像中，名称为“app.jar”。
* 第 4 行：定义一个入口点，也就是说，定义了由镜像生成容器，在启动时要执行的命令。这里是使用 java -jar /app.jar 执行 JAR 文件。

有了这个 Dockerfile，您可以使用 Docker 命令行工具创建镜像了，如下所示：

```bash
$ docker build . -t habuma/tacocloud:0.0.19-SNAPSHOT
```

此命令中的 “.” 指明了 Dockerfile 位置的相对路径。如果您是从其他路径运行 docker build，请替换 Dockerfile 的路径（不带文件名）。例如，如果您正在从父级项目中运行 docker build，命令应该像下面这样：

```bash
$ docker build tacocloud -t habuma/tacocloud:0.0.19-SNAPSHOT
```

在 -t 参数之后给出的值是镜像标记，它由名称和版本组成。在本例中，镜像名称为“habuma/tacocloud”，版本为 0.0.19-SNAPSHOT。

如果您想运行一下，可以使用 docker run 运行此新创建的镜像：

```bash
$ docker run -p8080:8080 habuma/tacocloud:0.0.19-SNAPSHOT
```

参数 -p8080:8080 将请求从主机上的端口 8080（例如，您正在运行 Docker 的主机）转发到容器的 8080 端口（ Tomcat 或 Netty 正在监听的位置）。

在构建 Docker 镜像时，如果您已经有了一个可执行的 JAR，那么这种方法就足够简单。但这不是从 Spring Boot 应用程序创建镜像的最简单的方式。

从 Spring Boot 2.3.0 开始，您可以构建容器镜像，而无需添加任何特殊的依赖项、配置文件或以任何方式修改项目。这是因为 Spring Boot 集成了直接构建镜像的插件，支持 Maven 和 Gradle 两种方式。

要将 Maven 构建的 Spring 项目构建成容器镜像，可以指定 Spring Boot Maven 插件的构建目标为 build-image，如下所示：

```bash
$ mvnw spring-boot:build-image
```

同样，Gradle 构建的项目也可以构建成容器镜像，如下所示：

```bash
$ gradlew bootBuildImage
```

这将基于 pom.xml 文件中 `<artifactId>` 和 `<version>` 属性构建带有默认标记的镜像。对于 Taco Cloud 应用程序，这类似于
“library/tacocloud:0.0.19-SNAPSHOT”。稍后我们将了解如何指定自定义镜像标签。

Spring Boot 的构建插件依赖 Docker 来创建镜像。因此，您需要在生成镜像的计算机上安装 Docker 运行时。无论如何，一旦镜像被创建后，就可以按如下方式运行：

```bash
$ docker run -p8080:8080 library/tacocloud:0.0.19-SNAPSHOT
```

这将运行镜像并映射端口 8080（由嵌入式 Tomcat 或 Netty 进行侦听）到主机的端口 8080。

镜像标记的默认格式为“docker.io/library/${project.artifactId}:${project.version}”，这就解释了为什么标记以“library”开头。如果您只在本地运行容器，这没什么问题。但您很可能希望将镜像推送到镜像注册中心，如 DockerHub，这将需要使用标签名称以引用镜像 Repository 的构建。

例如，假设您的组织在 DockerHub 中的 Repository 名称为“tacocloud”。在这种情况下，您将希望映像名称为“tacocloud/tacocloud:0.0.19-SNAPSHOT”，要将“library”默认前缀替换为“tacocloud”。要做到这一点，只要生成镜像时指定生成属性。对于 Maven，您需指定镜像
名称使用 spring-boot.build-image.imageName 这个 JVM 系统属性，如下所示：

```bash
$ mvnw spring-boot:build-image \
    -Dspring-boot.build-image.imageName=tacocloud/tacocloud:0.0.19-SNAPSHOT
```

对于 Gradle 构建的项目，它稍微简单一些。您可以使用 --imageName 参数，如下所示：

```bash
$ gradlew bootBuildImage --imageName=tacocloud/tacocloud:0.0.19-SNAPSHOT
```

这两种指定镜像名称的方法，任何一种都要求您执行构建时要记住指定镜像名称，而且不能犯错。为了让构建变得更简单，您可以将镜像名称指定为构建本身的一部分。

在 Maven 中，您可以在 Spring Boot Maven 插件中将映像名指定为配置条目。例如，以下项目的 pom.xml 文件中的 `<configuration>` 块，显示了如何指定镜像名称：

```xml
<plugin>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-maven-plugin</artifactId>
  <configuration>
    <image>
      <name>tacocloud/${project.artifactId}:${project.version}</name>
    </image>
  </configuration>
</plugin>
```

注意，我们可以利用变量，而不是硬编码，因为这些值已在其他地方指定了。这就消除了需要手动在镜像名称中添加版本号的麻烦。

对于 Gradle 构建的项目，build.Gradle 中的以下条目可实现相同的效果：

```yaml
bootBuildImage {
  imageName = "habuma/${rootProject.name}:${version}"
}
```

有了此配置，您无需再在命令行中指定镜像名称，就像我们前面所做的那样。

此时，您可以像以前一样使用 docker run 运行镜像（使用新的镜像名称），或您可以使用 docker push 将镜像推送到镜像注册中心，如
 DockerHub：

```bash
$ docker push habuma/tacocloud:0.0.19-SNAPSHOT
```

一旦镜像推到了镜像注册中心，就可以从任何能够访问该注册中心的环境拉取运行镜像。Kubernetes 是一个越来越常见的运行镜像的环境。让我们了解一下如何在 Kubernetes 中运行镜像。