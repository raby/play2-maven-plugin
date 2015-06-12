This is [Maven](http://maven.apache.org) plugin for [Play! Framework](http://www.playframework.org).

It supports Play! **2.1.x**, **2.2.x**, **2.3.x** and **2.4.x** versions only (2.0.x versions are not supported).

Play! **1.x** plugin is available here http://code.google.com/p/maven-play-plugin



&lt;hr&gt;



<a href='https://www.yourkit.com/'><img src='https://www.yourkit.com/images/yklogo.png' /></a>

YourKit supports open source projects with its full-featured Java Profiler.
YourKit, LLC is the creator of [YourKit Java Profiler](https://www.yourkit.com/java/profiler/)
and [YourKit .NET Profiler](https://www.yourkit.com/.net/profiler/),
innovative and intelligent tools for profiling Java and .NET applications.



&lt;hr&gt;



If you are here for the first time, please read the [Rationale](Rationale.md) first.

<font color='red'><strong>Plugin's most important features</strong></font>:

- pure Maven build, no SBT project required, just **pom.xml** file,

- Play! Framework 2.1.x, 2.2.x, 2.3.x and 2.4.x versions supported,

- Eclipse IDE integration - see [wiki page](EclipseIntegration.md),

- IntelliJ IDEA IDE integration - see [wiki page](IDEAIntegration.md),

- multi-module builds - see [wiki page](MultiModuleBuilds.md),

- WAR packaging - see [wiki page](WarPackaging.md)

**What's not supported yet:**

- running with auto-reloading

**News:**

<font color='red'><strong>2015.05.19 - 1.0.0-beta2 version released</strong></font>

- Play! Framework versions used upgraded to 2.3.9 and 2.4.0-RC3

- injected (dynamic) router generation support (Play! 2.4.x only)

- all Play! 2.3.x sample projects ported to 2.4.x (all with injected router generation set to help with upgrading your projects to Play! 2.4.x because there are almost no official sample projects for Play! 2.4.x)

For detailed information about all fixed issues see this [issues page](http://code.google.com/p/play2-maven-plugin/issues/list?can=1&q=label%3AMilestone-1.0.0-beta2%20status%3AFixed)

Read about [migrating your projects](Usage.md) from 1.0.0-beta1 to 1.0.0-beta2 and from older versions of Play! to 2.4.x.

**Project documentation**

Release [notes](ReleaseNotes.md)

Plugin [usage](Usage.md)

Maven generated [plugin's site](https://play2-maven-plugin.googlecode.com/svn/mavensite/1.0.0-beta2/play2-maven-plugin/index.html) ([development version](https://play2-maven-plugin.googlecode.com/svn/mavensite/1.0.0-beta3-SNAPSHOT/play2-maven-plugin/index.html)). Most interesting is [plugin mojos (tasks) description page](https://play2-maven-plugin.googlecode.com/svn/mavensite/1.0.0-beta2/play2-maven-plugin/plugin-info.html) ([development version](https://play2-maven-plugin.googlecode.com/svn/mavensite/1.0.0-beta3-SNAPSHOT/play2-maven-plugin/plugin-info.html)).

Many working [example projects](http://play2-maven-plugin.googlecode.com/svn/tags/test-projects-1.0.0-beta2/) ([development version](http://play2-maven-plugin.googlecode.com/svn/trunk/test-projects/)).