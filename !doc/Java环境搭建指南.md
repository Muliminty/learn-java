# Java 环境搭建指南

## 目录
- [1. Java 概述](#1-java-概述)
- [2. JDK 安装](#2-jdk-安装)
  - [2.1 Windows 系统](#21-windows-系统)
  - [2.2 macOS 系统](#22-macos-系统)
  - [2.3 Linux 系统](#23-linux-系统)
- [3. 环境变量配置](#3-环境变量配置)
- [4. 验证安装](#4-验证安装)
- [5. IDE 安装](#5-ide-安装)
- [6. 构建工具](#6-构建工具)
- [7. 常用命令](#7-常用命令)
- [8. 常见问题](#8-常见问题)

---

## 1. Java 概述

Java 是一门面向对象的编程语言，具有跨平台、高性能、安全性等特点。要开发 Java 程序，需要安装以下核心组件：

- **JDK (Java Development Kit)**: Java 开发工具包，包含 JRE 和开发工具
- **JRE (Java Runtime Environment)**: Java 运行环境，包含 JVM 和类库
- **JVM (Java Virtual Machine)**: Java 虚拟机，负责执行 Java 字节码

**JDK 版本说明**：
- **Java 8 (LTS)**: 长期支持版本，广泛使用
- **Java 11 (LTS)**: 长期支持版本，推荐使用
- **Java 17 (LTS)**: 最新长期支持版本
- **Java 21 (LTS)**: 当前最新 LTS 版本

---

## 2. JDK 安装

### 2.1 Windows 系统

#### 方法一：使用安装包

1. 下载 JDK 安装包：
   - 官方下载地址：https://www.oracle.com/java/technologies/downloads/
   - 或使用 OpenJDK：https://adoptium.net/

2. 运行安装程序：
   ```
   双击下载的 .exe 文件
   按照提示完成安装
   默认安装路径：C:\Program Files\Java\jdk-<version>
   ```

#### 方法二：使用 Chocolatey

```powershell
# 安装 Chocolatey（如果尚未安装）
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# 安装 JDK 17
choco install openjdk17

# 或安装其他版本
choco install openjdk11
choco install openjdk21
```

#### 方法三：使用 SDKMAN（适用于 Windows + WSL）

```bash
# 在 WSL 中安装 SDKMAN
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# 安装 JDK
sdk install java 17.0.9-tem
```

---

### 2.2 macOS 系统

#### 方法一：使用 Homebrew（推荐）

```bash
# 安装 Homebrew（如果尚未安装）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 安装 JDK
brew install openjdk@17

# 创建符号链接（可选）
sudo ln -sfn /opt/homebrew/opt/openjdk@17/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-17.jdk
```

#### 方法二：使用官方安装包

1. 下载 macOS 版 JDK：
   - Oracle JDK: https://www.oracle.com/java/technologies/downloads/
   - OpenJDK: https://adoptium.net/

2. 安装：
   ```
   双击 .dmg 文件
   拖动 JDK 到 Applications 文件夹
   ```

#### 方法三：使用 SDKMAN

```bash
# 安装 SDKMAN
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# 查看可用版本
sdk list java

# 安装 JDK 17
sdk install java 17.0.9-tem

# 设置为默认版本
sdk default java 17.0.9-tem
```

---

### 2.3 Linux 系统

#### 方法一：使用包管理器

**Ubuntu/Debian:**
```bash
# 更新包列表
sudo apt update

# 安装 OpenJDK 17
sudo apt install openjdk-17-jdk

# 或安装 OpenJDK 11
sudo apt install openjdk-11-jdk

# 安装开发工具
sudo apt install build-essential
```

**CentOS/RHEL:**
```bash
# 安装 OpenJDK 17
sudo yum install java-17-openjdk-devel

# 或安装 OpenJDK 11
sudo yum install java-11-openjdk-devel
```

**Arch Linux:**
```bash
# 安装 JDK
sudo pacman -S jdk17-openjdk
```

#### 方法二：使用 SDKMAN（推荐）

```bash
# 安装 SDKMAN
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"

# 安装 JDK
sdk install java 17.0.9-tem

# 查看已安装版本
sdk list java | grep installed
```

#### 方法三：手动安装

```bash
# 下载 JDK（以 Linux x64 为例）
wget https://download.java.net/java/GA/jdk17.0.2/dfd4a8d0985749f896bed50d7138ee7f/8/GPL/openjdk-17.0.2_linux-x64_bin.tar.gz

# 解压到指定目录
sudo mkdir -p /usr/local/java
sudo tar -xzf openjdk-17.0.2_linux-x64_bin.tar.gz -C /usr/local/java

# 配置环境变量（见下一节）
```

---

## 3. 环境变量配置

### 3.1 Windows 系统

#### 方法一：图形界面配置

1. 右键点击"此电脑" → "属性"
2. 点击"高级系统设置"
3. 点击"环境变量"
4. 在"系统变量"中添加/修改：

```
变量名: JAVA_HOME
变量值: C:\Program Files\Java\jdk-17

变量名: Path
变量值: %JAVA_HOME%\bin (追加到现有值)
```

#### 方法二：命令行配置

```powershell
# 设置 JAVA_HOME
[System.Environment]::SetEnvironmentVariable('JAVA_HOME', 'C:\Program Files\Java\jdk-17', [System.EnvironmentVariableTarget]::Machine)

# 添加到 PATH
[System.Environment]::SetEnvironmentVariable('Path', $env:Path + ';C:\Program Files\Java\jdk-17\bin', [System.EnvironmentVariableTarget]::Machine)
```

---

### 3.2 macOS 系统

#### 方法一：编辑 ~/.zshrc（推荐，Zsh 用户）

```bash
# 编辑配置文件
vim ~/.zshrc

# 添加以下内容
export JAVA_HOME=/opt/homebrew/opt/openjdk@17
export PATH=$JAVA_HOME/bin:$PATH

# 重新加载配置
source ~/.zshrc
```

#### 方法二：编辑 ~/.bash_profile（Bash 用户）

```bash
# 编辑配置文件
vim ~/.bash_profile

# 添加以下内容
export JAVA_HOME=/Library/Java/JavaVirtualMachines/openjdk-17.jdk/Contents/Home
export PATH=$JAVA_HOME/bin:$PATH

# 重新加载配置
source ~/.bash_profile
```

#### 方法三：使用系统级配置

```bash
# 编辑系统配置文件
sudo vim /etc/paths

# 添加以下行
/opt/homebrew/opt/openjdk@17/bin

# 或创建环境变量配置
sudo vim /etc/launchd.conf
```

---

### 3.3 Linux 系统

#### 方法一：用户级配置（推荐）

```bash
# 编辑 ~/.bashrc 或 ~/.bash_profile
vim ~/.bashrc

# 添加以下内容
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH

# 重新加载配置
source ~/.bashrc
```

#### 方法二：系统级配置

```bash
# 创建 Java 环境变量文件
sudo vim /etc/profile.d/java.sh

# 添加以下内容
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH

# 设置执行权限
sudo chmod +x /etc/profile.d/java.sh

# 重新加载配置
source /etc/profile.d/java.sh
```

#### 方法三：使用 alternatives

```bash
# 配置默认 Java 版本
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

---

## 4. 验证安装

### 4.1 基础验证

```bash
# 检查 Java 版本
java -version

# 检查 Java 编译器版本
javac -version

# 检查 JAVA_HOME 环境变量
echo $JAVA_HOME   # Linux/macOS
echo %JAVA_HOME%  # Windows
```

### 4.2 创建测试程序

创建 `HelloWorld.java`:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java!");
    }
}
```

编译和运行：

```bash
# 编译
javac HelloWorld.java

# 运行
java HelloWorld

# 输出应该为: Hello, Java!
```

### 4.3 查看系统信息

```bash
# 查看所有已安装的 Java 版本（Linux）
/usr/libexec/java_home -V   # macOS
update-alternatives --list java  # Linux

# 查看系统属性
java -XshowSettings:properties
```

---

## 5. IDE 安装

### 5.1 IntelliJ IDEA（推荐）

#### 下载和安装

- **Ultimate 版（付费）**: 功能完整，支持 Web 开发、数据库等
- **Community 版（免费）**: 开源，基础功能足够

**安装方式**：

**Windows:**
```powershell
# 使用 Chocolatey
choco install intellijidea-community
```

**macOS:**
```bash
# 使用 Homebrew
brew install --cask intellij-idea-ce
```

**Linux:**
```bash
# Ubuntu/Debian
wget -O - https://packages.jetbrains.com/gpg/jetbrains-b142c4cc.asc | sudo apt-key add -
sudo sh -c 'echo "deb [arch=amd64] https://download.jetbrains.com/idea stable main" > /etc/apt/sources.list.d/jetbrains-idea.list'
sudo apt update
sudo apt install idea-community
```

或从官网下载：https://www.jetbrains.com/idea/download/

---

### 5.2 Eclipse

**下载地址**：https://www.eclipse.org/downloads/

**macOS 安装**：
```bash
brew install --cask eclipse-java
```

---

### 5.3 Visual Studio Code

**安装和配置**：

```bash
# macOS
brew install --cask visual-studio-code

# Ubuntu/Debian
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/trusted.gpg.d/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt update
sudo apt install code
```

**推荐扩展**：
- Extension Pack for Java
- Spring Boot Extension Pack（如需 Spring 开发）
- Code Runner
- SonarLint（代码质量检查）

---

### 5.4 VS Code Java 扩展安装

打开 VS Code，按 `Ctrl+Shift+X`（或 `Cmd+Shift+X`）打开扩展市场，搜索并安装：

1. **Extension Pack for Java**（Microsoft 官方）
   - Language Support for Java
   - Debugger for Java
   - Java Test Runner
   - Maven for Java
   - Project Manager for Java
   - Java Intellisense

2. **Spring Boot Extension Pack**（可选）

3. **Code Runner**（快速运行代码）

---

## 6. 构建工具

### 6.1 Maven

**macOS 安装**：
```bash
brew install maven
```

**Linux 安装**：
```bash
sudo apt install maven  # Ubuntu/Debian
sudo yum install maven  # CentOS/RHEL
```

**验证安装**：
```bash
mvn -version
```

**创建新项目**：
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

---

### 6.2 Gradle

**macOS 安装**：
```bash
brew install gradle
```

**Linux 安装**：
```bash
sudo apt install gradle  # Ubuntu/Debian
sudo yum install gradle  # CentOS/RHEL
```

**使用 SDKMAN 管理**：
```bash
sdk install gradle
```

**验证安装**：
```bash
gradle -version
```

**创建新项目**：
```bash
gradle init --type java-application
```

---

### 6.3 常用命令对比

| 操作 | Maven | Gradle |
|------|-------|--------|
| 编译 | `mvn compile` | `gradle build` |
| 测试 | `mvn test` | `gradle test` |
| 打包 | `mvn package` | `gradle build` |
| 清理 | `mvn clean` | `gradle clean` |
| 安装到本地仓库 | `mvn install` | `gradle publishToMavenLocal` |
| 跳过测试 | `mvn package -DskipTests` | `gradle build -x test` |

---

## 7. 常用命令

### 7.1 Java 基本命令

```bash
# 编译 Java 文件
javac MyClass.java

# 运行 Java 程序
java MyClass

# 运行带参数的程序
java MyClass arg1 arg2

# 指定类路径运行
java -cp /path/to/classes MyClass

# 打印详细输出
java -verbose MyClass

# 查看 JVM 参数
java -X
```

### 7.2 JAR 命令

```bash
# 创建 JAR 文件
jar cf myapp.jar MyClass.class

# 查看内容
jar tf myapp.jar

# 提取内容
jar xf myapp.jar

# 运行 JAR 文件
java -jar myapp.jar

# 创建可执行 JAR（带清单文件）
echo "Main-Class: MyClass" > manifest.txt
jar cfm myapp.jar manifest.txt MyClass.class
```

### 7.3 javac 高级选项

```bash
# 指定输出目录
javac -d bin MyClass.java

# 指定源文件编码
javac -encoding UTF-8 MyClass.java

# 同时编译多个文件
javac *.java

# 显示详细信息
javac -verbose MyClass.java

# 指定类路径
javac -cp /path/to/libs/*.jar MyClass.java
```

---

## 8. 常见问题

### 8.1 问题：`java: command not found`

**原因**：Java 未安装或环境变量未配置

**解决方案**：
1. 确认 JDK 已安装
2. 检查环境变量配置
3. 重新加载配置文件

```bash
# macOS/Linux
echo $PATH
echo $JAVA_HOME

# Windows
echo %PATH%
echo %JAVA_HOME%
```

---

### 8.2 问题：`javac: command not found`

**原因**：仅安装了 JRE 而非 JDK

**解决方案**：
1. 安装完整的 JDK
2. 确保 `$JAVA_HOME/bin` 在 PATH 中

---

### 8.3 问题：`UnsupportedClassVersionError`

**原因**：编译和运行使用的 Java 版本不一致

**解决方案**：
1. 检查编译版本：`javac -version`
2. 检查运行版本：`java -version`
3. 统一版本或使用 `javac -source 1.8 -target 1.8` 指定版本

---

### 8.4 问题：`JAVA_HOME` 未生效

**原因**：配置文件未重新加载或配置位置错误

**解决方案**：

**macOS/Linux**：
```bash
# 编辑正确的配置文件
vim ~/.zshrc  # Zsh 用户
vim ~/.bashrc # Bash 用户

# 添加配置后重新加载
source ~/.zshrc  # 或 source ~/.bashrc
```

**Windows**：
```powershell
# 以管理员身份运行命令
setx JAVA_HOME "C:\Program Files\Java\jdk-17" /M
setx PATH "%PATH%;%JAVA_HOME%\bin" /M

# 重启终端或电脑
```

---

### 8.5 问题：多个 Java 版本共存

**场景**：系统中有多个 Java 版本，需要切换

**解决方案**：

**使用 SDKMAN（推荐）**：
```bash
# 查看已安装版本
sdk list java

# 切换版本
sdk use java 17.0.9-tem

# 设置默认版本
sdk default java 17.0.9-tem
```

**macOS**：
```bash
# 临时切换
export JAVA_HOME=$(/usr/libexec/java_home -v 17)

# 永久切换
echo 'export JAVA_HOME=$(/usr/libexec/java_home -v 17)' >> ~/.zshrc
```

**Linux**：
```bash
# 使用 alternatives
sudo update-alternatives --config java
sudo update-alternatives --config javac
```

**Windows**：
- 修改 `JAVA_HOME` 环境变量指向不同版本的 JDK
- 更新 PATH 变量

---

### 8.6 问题：IDE 无法识别 JDK

**IntelliJ IDEA**：
1. File → Project Structure → Project SDK
2. 点击 "+" 添加 JDK
3. 选择 JDK 安装路径

**Eclipse**：
1. Window → Preferences → Java → Installed JREs
2. 点击 "Add" → Standard VM
3. 选择 JDK 安装路径

**VS Code**：
1. `Ctrl+Shift+P` → "Java: Configure Java Runtime"
2. 在配置文件中设置 `java.home`

---

### 8.7 问题：权限错误

**macOS/Linux**：
```bash
# 修复脚本执行权限
chmod +x script.sh

# 修复目录权限
chmod 755 /path/to/directory
```

**Windows**：
- 以管理员身份运行命令提示符
- 检查文件/文件夹安全设置

---

### 8.8 问题：内存不足

**解决方案**：
```bash
# 增加 JVM 堆内存
java -Xms512m -Xmx2g MyClass

# -Xms: 初始堆内存
# -Xmx: 最大堆内存
```

---

## 9. 推荐学习资源

### 官方文档
- [Java 官方文档](https://docs.oracle.com/javase/)
- [OpenJDK 文档](https://openjdk.org/)
- [Maven 官方文档](https://maven.apache.org/guides/)
- [Gradle 官方文档](https://docs.gradle.org/)

### 在线教程
- [Java 教程](https://www.runoob.com/java/)
- [菜鸟教程 Java](https://www.runoob.com/java/java-tutorial.html)
- [Baeldung Java 教程](https://www.baeldung.com/)

### 练习平台
- [LeetCode](https://leetcode.cn/)
- [牛客网](https://www.nowcoder.com/)
- [Codeforces](https://codeforces.com/)

---

## 10. 快速开始

### 第一个程序

1. 创建 `HelloWorld.java`:
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Java World!");
    }
}
```

2. 编译：
```bash
javac HelloWorld.java
```

3. 运行：
```bash
java HelloWorld
```

### Maven 项目

1. 创建项目：
```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=my-java-app -DarchetypeArtifactId=maven-archetype-quickstart
```

2. 编译：
```bash
cd my-java-app
mvn compile
```

3. 运行：
```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```

### Gradle 项目

1. 创建项目：
```bash
gradle init --type java-application
```

2. 编译：
```bash
gradle build
```

3. 运行：
```bash
gradle run
```

---

## 总结

完成以上步骤后，您应该已经：
1. ✅ 安装了 JDK
2. ✅ 配置了环境变量
3. ✅ 验证了安装成功
4. ✅ 安装了 IDE
5. ✅ 配置了构建工具

现在可以开始您的 Java 学习之旅了！

---

**文档版本**: 1.0
**最后更新**: 2025-01-04
**适用版本**: JDK 8, 11, 17, 21
