#### maven

maven是一个项目管理和构建工具，基于项目对象（POM）的概念，通过一点描述信息来管理项目的构建。

- 依赖管理：方便快捷地管理项目以来的资源（jar包），避免版本冲突问题
- 统一项目结构：提供标准、统一的项目结构
- 项目构建：变化尊跨平台的自动化项目构建方式



##### maven坐标

maven中的坐标是唯一标识，通过该坐标可以唯一确定资源位置

坐标的组成：

- groupId：定义当前maven项目隶属的组织名称，通常是域名反写
- artifactId：定义当前maven项目的名称，通常是模块名称
- version：定义当前项目版本号





##### 配置依赖

```xml
<!-- 在xml中添加标签 --> 
<dependencies>
    <!-- 配置依赖 --> 
    <dependency>
        <!-- 坐标 -->
        <groupId></groupId>
        <artifactId></artifactId>
        <version></version>
        
        <!-- 依赖的生效范围 -->
        <!-- compile(默认)  主程序、测试、打包均生效 -->
        <!-- test  仅在测试中生效 -->
        <!-- provided  在主程序和测试程序生效，打包不生效 -->
        <!-- runtime  在测试程序和打包中生效，主程序不生效 -->
        <scope></scope>
        
        <!-- 依赖具有传递性，会自动依赖该项目下的依赖 --> 
        <!-- 可以主动排除该项目下的依赖 -->
    	<!-- 排除依赖 -->
        <exclusions>
            <exclusion>
                <groupId></groupId>
                <artifactId></artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    
</dependencies>
```



##### maven项目构建命令

```
mvn compile  # 编译
mvn clean    # 清理
mvn test     # 测试
mvn package  # 打包
mvn install  # 安装到本地仓库
```





##### Maven的生命周期

同一套生命周期中，运行后面的阶段，前面的阶段都会运行





#### 聚合

- 作用：用于快速构建Maven工程，一次性构建多个项目/ 模块

- 制作方式：

  - 创建一个空模块，打包类型定义为`pom`

    ```xml
    <pockaging>pom</pockaging>
    ```

    

  - 定义当前模块管理的其他模块

    ```xml
    <modules>
    	<module>../ssm_controller</module>
        <module>../ssm_service</module>
        <module>../ssm_dao</module>
        <module>../ssm_pojo</module>
    </modules>
    ```

    



#### 继承

子工程使用父工程的依赖

在上面聚合模块的xml文件中编写：

```xml
<dependencyManagement>
	<dependencies>
    	<dependency>
        	<groupId></groupId>
            <artifactId></artifactId>
            <version></version>
        </dependency>
        
        <!-- ... -->
    </dependencies>
</dependencyManagement>
```



在子工程的`pom`文件中定义父工程文件

```xml
<parent>
	<groupId>com.example</groupId>
    <artifactId>ssm</artifactId>
    <version></version>
    <!-- 父工程的pom文件的位置 -->
    <relativePath>../ssm/pom.xml</relativePath>
</parent>

<!-- 同时，子工程中的depencies不需要指定版本 -->
```





























































