**Plugin supports Play! Framework 2.1.x, 2.2.x, 2.3.x and 2.4.x versions**

There are some differences when configuring Play! project for 2.1.x, 2.2.x, 2.3.x and 2.4.x:

[Play! Framework 2.1.x usage](UsagePlay21.md),

[Play! Framework 2.2.x usage](UsagePlay22.md),

[Play! Framework 2.3.x usage](UsagePlay23.md),

[Play! Framework 2.4.x usage](UsagePlay24.md).


**Using plugin SNAPSHOT versions**

Add
```
            <pluginRepositories>
                <pluginRepository>
                    <id>sonatype-nexus-snapshots</id>
                    <name>Sonatype Nexus Snapshots</name>
                    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
                    <releases>
                        <enabled>false</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
```
to your play2 project or better add
```
<settings>
    ...
    <profiles>
        ...
        <profile>
            <id>myprofile</id>
            <pluginRepositories>
                <pluginRepository>
                    <id>sonatype-nexus-snapshots</id>
                    <name>Sonatype Nexus Snapshots</name>
                    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
                    <releases>
                        <enabled>false</enabled>
                    </releases>
                </pluginRepository>
            </pluginRepositories>
        </profile>
        ...
    </profiles>

    <activeProfiles>
       <activeProfile>myprofile</activeProfile>
    </activeProfiles>
    ...
</settings>
```
to ~/.m2/settings.xml file. More info: http://maven.apache.org/guides/mini/guide-multiple-repositories.html

**1.0.0-beta1 to 1.0.0-beta2 migration**

Just change plugin version from
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-beta1</play2.plugin.version>
        ...
    </properties>
```
to
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-beta2</play2.plugin.version>
        ...
    </properties>
```

**1.0.0-alpha9 to 1.0.0-beta1 migration**

Just change plugin version from
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha9</play2.plugin.version>
        ...
    </properties>
```
to
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-beta1</play2.plugin.version>
        ...
    </properties>
```

**1.0.0-alpha8 to 1.0.0-alpha9 migration**

Just change plugin versions from
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha8</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta4</sbt-compiler.plugin.version>
    </properties>
```
to
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha9</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta5</sbt-compiler.plugin.version>
    </properties>
```

**1.0.0-alpha7 to 1.0.0-alpha8 migration**

Just change plugin version from
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha7</play2.plugin.version>
        ...
    </properties>
```
to
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha8</play2.plugin.version>
        ...
    </properties>
```

**1.0.0-alpha6 to 1.0.0-alpha7 migration**

Just change plugin versions from
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha6</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta3</sbt-compiler.plugin.version>
    </properties>
```
to
```
    <properties>
        ...
        <play2.plugin.version>1.0.0-alpha7</play2.plugin.version>
        <sbt-compiler.plugin.version>1.0.0-beta4</sbt-compiler.plugin.version>
    </properties>
```

**1.0.0-alpha5 to 1.0.0-alpha6 migration**

Remove provider from plugin's dependencies (provider auto-discovery mechanism will add this dependency automatically).
For example replace
```
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
                <dependencies>
                    <dependency>
                        <groupId>com.google.code.play2-maven-plugin</groupId>
                        <artifactId>play2-provider-play22</artifactId>
                        <version>${play2.plugin.version}</version>
                    </dependency>
                </dependencies>
            </plugin>
```
with
```
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
            </plugin>
```

Add sbt-compiler-maven-plugin

```
    <properties>
        ...
        <sbt-compiler.plugin.version>1.0.0-beta3</sbt-compiler.plugin.version>
    </properties>

    <build>
        ...
        <plugins>
            ...
            <plugin>
                <groupId>com.google.code.sbt-compiler-maven-plugin</groupId>
                <artifactId>sbt-compiler-maven-plugin</artifactId>
                <version>${sbt-compiler.plugin.version}</version>
            </plugin>
        </plugins>
    </build>
```

**1.0.0-alpha4 to 1.0.0-alpha5 migration**

No changes required.

**1.0.0-alpha3 to 1.0.0-alpha4 migration**

In your play2 <strong>Java</strong> (not Scala) project:

a) add "mainLang=java" because "mainLang" tricky autodetection mechanism was removed and default value is "scala"
```
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
                <configuration>
                    <mainLang>java</mainLang>
                </configuration>
            </plugin>
```
or
```
            <properties>
                ...
                <play.mainLang>java</play.mainLang>
            </properties>
```

**1.0.0-alpha2 to 1.0.0-alpha3 migration**

In your play2 project:

a) replace
```
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-compiler</artifactId>
            <version>${scala.version}</version>
            <scope>provided</scope>
        </dependency>
```
with
```
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
        </dependency>
```

b) replace
```
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
            </plugin>
```
with
```
            <plugin>
                <groupId>com.google.code.play2-maven-plugin</groupId>
                <artifactId>play2-maven-plugin</artifactId>
                <version>${play2.plugin.version}</version>
                <extensions>true</extensions>
                <dependencies>
                    <dependency>
                        <groupId>com.google.code.play2-maven-plugin</groupId>
                        <artifactId>play2-provider-play21</artifactId>
                        <version>${play2.plugin.version}</version>
                    </dependency>
                </dependencies>
            </plugin>
```

**Play! 2.3.x to Play! 2.4.x migration**

In your play2 project

a) change Play! version from
```
    <properties>
        ...
        <play2.version>2.3.9</play2.version>
    </properties>
```
to
```
    <properties>
        ...
        <play2.version>2.4.0-RC3</play2.version>
    </properties>
```

b) remove repository definition (all artifacts are in Maven central repository)
```
    <repositories>
        <repository>
            <id>typesafe</id>
            <name>Typesafe - releases</name>
            <url>http://repo.typesafe.com/typesafe/releases/</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </repository>
    </repositories>
```

c) add dependency
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-netty-server_2.10</artifactId>
            <version>${play2.version}</version>
        </dependency>
```

d) if using Specs2 tests add dependency
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-specs2_2.11</artifactId>
            <version>${play2.version}</version>
            <scope>test</scope>
        </dependency>
```
and repository definition
```
    <!-- 'com.typesafe.play:play-specs2_2.11' depends on
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
```

e) if using JDBC evolutions add dependency
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-jdbc-evolutions_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>
```

f) if using Ebean change
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-java-ebean_2.11</artifactId>
            <version>${play2.version}</version>
        </dependency>
```
to
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-ebean_2.11</artifactId>
            <version>${play2-ebean.version}</version>
        </dependency>
```
where <strong>play2-ebean.version</strong> property needs to be added to project properties
```
    <properties>
        ...
        <play2-ebean.version>1.0.0-RC3</play2-ebean.version>
    </properties>
```
and change plugin's configuration parameter from
```
                    <serverJvmArgs>-DapplyEvolutions.default=true</serverJvmArgs>
```
to
```
                    <serverJvmArgs>-Dplay.evolutions.db.default.autoApply=true</serverJvmArgs>
```

**Play! 2.2.x to Play! 2.3.x migration**

In your play2 project change Play! version from
```
    <properties>
        ...
        <play2.version>2.2.6</play2.version>
    </properties>
```
to
```
    <properties>
        ...
        <play2.version>2.3.9</play2.version>
    </properties>
```

**Play! 2.1.x to Play! 2.2.x migration**

In your play2 project

a) change Play! version from
```
    <properties>
        ...
        <play2.version>2.1.5</play2.version>
    </properties>
```
to
```
    <properties>
        ...
        <play2.version>2.2.6</play2.version>
    </properties>
```

b) change "groupId" of all Play! dependencies from "play"
```
        <dependency>
            <groupId>play</groupId>
            <artifactId>play-xxxx_2.10</artifactId>
            <version>${play2.version}</version>
        </dependency>
```
to "com.typesafe.play"
```
        <dependency>
            <groupId>com.typesafe.play</groupId>
            <artifactId>play-xxxx_2.10</artifactId>
            <version>${play2.version}</version>
        </dependency>
```