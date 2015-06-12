# IntelliJ IDEA IDE integration #

## Import steps: ##

### 1. Import the project as Maven project. ###

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp0.PNG

Click **Import Project**

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp1.PNG

Select **Maven** external model and click **Next**

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp2.PNG

Accept default values and click **Next**

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp3.PNG

Click **Next**

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp4.PNG

Click **Finish**

When import process finishes, the project looks like on the image below.

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp5.PNG

It requires two additional configuration steps.

### 2. Configure project after import ###

Open project's popup menu

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp6.PNG

and click **Maven/Generate Sources and Update Folders**

Maven generates Scala and Java sources from routes file and HTML templates and adds **target/src\_managed/main** as additional sources root

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp7.PNG

### 3. Add Scala support ###

Open project's popup menu

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp8.PNG

and click **Add Framework Support...**

http://play2-maven-plugin.googlecode.com/svn/wiki/images/idea/imp9.PNG

Select Scala support and click **OK**



That's all. Have a nice day :)