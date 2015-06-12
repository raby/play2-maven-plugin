Simplest project (pom.xml file) should look like:

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>test</groupId>
    <artifactId>test</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>play2</packaging>

    <name>Play! Framework 2.4.x Maven Test Project</name>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

        <play2.version>2.4.0-RC3</play2.version>
        <scala.version>2.11.6</scala.version>

        <play2.plugin.version>1.0.0-beta2</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta5</sbt-compiler.plugin.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
        </dependency>

        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- required for: "run", "start" and "dist" -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-netty-server_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>
    </dependencies>

    <build>
        <sourceDirectory>${basedir}/app</sourceDirectory>
        <testSourceDirectory>${basedir}/test</testSourceDirectory>
        <resources>
            <resource>
                <directory>${basedir}/conf</directory>
            </resource>
            <resource>
                <directory>${basedir}/public</directory>
                <targetPath>public</targetPath>
            </resource>
        </resources>

        <plugins>
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
            </plugin>
        </plugins>
    </build>
</project>
```

Example with optional dependencies and configuration options:

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>test</groupId>
    <artifactId>test</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>play2</packaging>

    <name>Play! Framework 2.4.x Maven Test Project</name>

    <!-- only if there are Specs2 tests in the project;
         'com.typesafe.play:play-specs2_2.11' depends on
         'org.scalaz.stream:scalaz-stream_2.11:0.7a:jar'
         and this artifact is not available in Maven central repository yet,
         see https://github.com/scalaz/scalaz-stream/issues/258 -->
    <repositories>
        <repository>
            <id>scalaz-bintray</id>
            <name>Scalaz Bintray - releases</name>
            <url>https://dl.bintray.com/scalaz/releases/</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

        <play2.version>2.4.0-RC3</play2.version>
        <play2-ebean.version>1.0.0-RC3</play2-ebean.version>
        <scala.version>2.11.6</scala.version>

        <play2.plugin.version>1.0.0-beta2</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta5</sbt-compiler.plugin.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
        </dependency>

        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- required for: "run", "start" and "dist" -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-netty-server_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using Anorm -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>anorm_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using JDBC -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-jdbc_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using JDBC evolutions -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-jdbc-evolutions_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using Java -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-java_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using Ebean -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-ebean_2.11</artifactId>
            <version>${play2-ebean.version}</version>
        </dependency>

        <!-- only if using JPA -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-java-jpa_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>

        <!-- only if using JPA -->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>4.3.9.Final</version>
            <exclusions>
                <!-- required to avoid version downgrade from '1.4.01' to '1.0.b2' -->
                <exclusion>
                    <groupId>xml-apis</groupId>
                    <artifactId>xml-apis</artifactId>
                </exclusion>
            </exclusions>
        </dependency>

        <!-- only if there are tests in the project -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-test_2.11</artifactId>
            <version>${play2.version}</version>
            <scope>test</scope>
        </dependency>

        <!-- only if there are Specs2 tests in the project -->
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-specs2_2.11</artifactId>
            <version>${play2.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <sourceDirectory>${basedir}/app</sourceDirectory>
        <testSourceDirectory>${basedir}/test</testSourceDirectory>
        <resources>
            <resource>
                <directory>${basedir}/conf</directory>
            </resource>
            <resource>
                <directory>${basedir}/public</directory>
                <targetPath>public</targetPath>
            </resource>
        </resources>

        <plugins>
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
                <configuration>
                    <!-- only if using database evolutions -->
                    <serverJvmArgs>-Dplay.evolutions.db.default.autoApply=true</serverJvmArgs>
                </configuration>
                <executions>
                    <!-- only if there are assets in the project -->
                    <execution>
                        <id>default-play2-compile-assets</id>
                        <goals>
                            <goal>closure-compile</goal> <!-- only if precompiling js assets -->
                            <goal>coffee-compile</goal> <!-- only if precompiling coffee assets -->
                            <goal>less-compile</goal> <!-- only if precompiling less assets -->
                        </goals>
                    </execution>
                    <!-- only if using Ebean -->
                    <execution>
                        <id>default-play2-ebean-enhance</id>
                        <goals>
                            <goal>ebean-enhance</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

For Scala 2.10 just replace:

```
    <properties>
        ...
        <scala.version>2.11.6</scala.version>
    </properties>
```

with

```
    <properties>
        ...
        <scala.version>2.10.5</scala.version>
    </properties>
```

and suffixes in all Play! dependency artifact ids from "`_2.11`" to "`_2.10`", for example change:

```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>
```

to

```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play_2.10</artifactId>
            <version>${play2.version}</version>
        </dependency>
```

For more example projects go to [Play! 2.4.x test projects](http://play2-maven-plugin.googlecode.com/svn/tags/test-projects-1.0.0-beta2/play24/).