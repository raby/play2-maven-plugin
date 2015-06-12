**Differences beteen SBT and Maven builds**

1.

<font color='red'><strong>Only in Play! 2.1.x and 2.2.x</strong></font>

It seems (I didn't check it in documentation) that in SBT dependency versions resolution for "compile" and "test" scopes is independent.

I mean, different versions of the same dependency can be selected for these two scopes.

In Maven this is not possible. More, I think, it's better that it's not possible.

When mavenizing Play! default sample projects I found that Fluentium integration tests do not work. The reason is different versions of **commons-codec**, **httpcore** and **httpclient** in "play" and "play-test" dependency subtrees.

Below is a fragment of dependency tree (mvn dependency:tree -Dverbose):

```
com.google.code.play2-maven-plugin.test-projects.play21.java:computer-database:play2:1.0.0-alpha5
+- play:play_2.10:jar:2.1.5:compile
|  +- oauth.signpost:signpost-core:jar:1.2.1.2:compile
|  |  \- commons-codec:commons-codec:jar:1.3:compile
|  +- oauth.signpost:signpost-commonshttp4:jar:1.2.1.2:compile
|  |  +- (oauth.signpost:signpost-core:jar:1.2.1.2:compile - omitted for duplicate)
|  |  +- org.apache.httpcomponents:httpcore:jar:4.0.1:compile
|  |  \- org.apache.httpcomponents:httpclient:jar:4.0.1:compile
|  |     +- (org.apache.httpcomponents:httpcore:jar:4.0.1:compile - omitted for duplicate)
|  |     \- (commons-codec:commons-codec:jar:1.3:compile - omitted for duplicate)

\- play:play-test_2.10:jar:2.1.5:test
   \- org.fluentlenium:fluentlenium-festassert:jar:0.7.3:test
      +- org.fluentlenium:fluentlenium-core:jar:0.7.3:test
      |  +- org.seleniumhq.selenium:selenium-java:jar:2.25.0:test
      |  |  +- org.seleniumhq.selenium:selenium-android-driver:jar:2.25.0:test
      |  |  |  \- org.seleniumhq.selenium:selenium-remote-driver:jar:2.25.0:test
      |  |  |     +- (org.apache.httpcomponents:httpclient:jar:4.1.2:test - omitted for conflict with 4.0.1)
      |  |  +- org.seleniumhq.selenium:selenium-htmlunit-driver:jar:2.25.0:test
      |  |  |  +- net.sourceforge.htmlunit:htmlunit:jar:2.9:test
      |  |  |  |  +- org.apache.httpcomponents:httpmime:jar:4.1.2:test
      |  |  |  |  |  +- (org.apache.httpcomponents:httpcore:jar:4.1.2:test - omitted for conflict with 4.0.1)
      |  |  |  |  +- (commons-codec:commons-codec:jar:1.4:test - omitted for conflict with 1.3)
      |  |  |  \- (org.apache.httpcomponents:httpclient:jar:4.1.2:test - omitted for conflict with 4.0.1)
```

In Maven build commons-codec:1.3, httpcore:4.0.1 and httpclient:4.0.1 versions are selected.

In SBT the above versions are selected for runtime ("dist" task for example) but: commons-codec:1.4, httpcore:4.1.2 and httpclient:4.1.2 are selected for testing.

When running tests with: commons-codec:1.3, httpcore:4.0.1 and httpclient:4.0.1 in Maven an error is being thrown:

```
Running IntegrationTest
[info] play - datasource [jdbc:h2:mem:play-test--1522106138;] bound to JNDI as DefaultDS
Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 1.844 sec <<< FAILURE!
test(IntegrationTest)  Time elapsed: 1.828 sec  <<< ERROR!
java.lang.RuntimeException: java.lang.RuntimeException: java.lang.NoClassDefFoundError: org/apache/http/conn/scheme/SchemeSocketFactory
	at java.net.URLClassLoader$1.run(URLClassLoader.java:202)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:190)
        ...
```

The newer versions can be forced by adding:

```
    <dependency>
        <groupId>commons-codec</groupId>
        <artifactId>commons-codec</artifactId>
        <version>1.6</version>
    </dependency>

    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpcore</artifactId>
        <version>4.1.3</version>
    </dependency>

    <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
        <version>4.1.2</version>
    </dependency>
```

but then these versions are being used in runtime too (when creating distribution package).

A workaround I used for now is to exclude Fluentium tests by default, and to create a profile with updated dependencies for running them in [this test project](https://play2-maven-plugin.googlecode.com/svn/tags/test-projects-1.0.0-alpha5/play21/java/computer-database-jpa/pom.xml), but I don't like this solution.

The worst thing is that you can create SBT project that passes all tests and does not work in production, because it requires something that is present in the newer versions of any of the three dependencies (just like Fluentium does).
I didn't test it, but will do soon.