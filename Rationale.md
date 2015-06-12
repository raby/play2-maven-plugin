**Why I wrote this plugin**

1.

I know, the is already [one plugin](https://github.com/nanoko-project/maven-play2-plugin), but this is only a simple SBT wrapper.

The real Maven build has to use Maven dependency system. With SBT wrapper you have to maintain two builds: Maven and SBT, declare dependencies in two places: Maven pom.xml and SBT project/Build.scala files and keep them synchronized. Having two build systems in one project is strange.

I've tested if popular Maven reporting plugins (JXR, Javadoc, Findbugs, PMD, CPD, Cobertura, Surefire Report) work with that plugin. Surprisingly most of them do. The exceptions are: Surefire Report and Cobertura.

- Surefire Report shows no tests because they were not run by Maven Surefire plugin, so expected result files are not present

- Cobertura always shows 0% coverage because there is (or I don't know how to do it) no way to tell Play/SBT to run tests on Cobertura instrumented classes.

With native Maven plugin generated Surefire and Cobertura reports just work: [Cobertura](https://play2-maven-plugin.googlecode.com/svn/mavensite/test-projects/reporting/full/java/computer-database-jpa/1.0.0-alpha1/cobertura/index.html), [Surefire](https://play2-maven-plugin.googlecode.com/svn/mavensite/test-projects/reporting/full/java/computer-database-jpa/1.0.0-alpha1/surefire-report.html)

2.

Additionally, I see Play! users have many problems with SBT multimodule builds. I think, this is quite easy with Maven. See this extremely simple example:

https://play2-maven-plugin.googlecode.com/svn/trunk/test-projects/play21/multimodule

**How I wrote this plugin**

1.

I tried to write this plugin for Play! 2.0.x versions but found it impossible (or hard to achieve) to use some parts of Play! (assets compilers for example) without depending on Play! SBT Plugin (which wasn't even deployed as Maven artifact).

With the modularization introduced in Play! 2.1.x line it was possible to use some Play! code, for example routes and templates compilers.

2.

I was looking for effective Scala and Java compilation. The first candidate was [Maven Scala Plugin](http://scala-tools.org/mvnsites/maven-scala-plugin/), but it had no option to compile Scala and Java in one pass, and no SBT style incremental compilation.

Then I found [Zinc Compiler](https://github.com/typesafehub/zinc). It's a stand-alone version of SBT's incremental compiler, so its working and results should be the same as Play!'s.

**The future**

<font color='red'><strong>If there will be interest, I will keep on developing this plugin</strong></font>. Only this will give me enough power to spend more time working on it.

Based on my experience with [Play! 1.x Maven plugin](http://code.google.com/p/maven-play-plugin/) I know that there are many features that can be added to make this plugin at least as functional as the original Play! SBT Plugin.

What I need is user feedback with as many as possible sample projects showing bugs or possibility of new features.

Feel free to create issues. Maybe it will make sense to create a discussion group.

I say it once more, the plugin's future depends on its users.