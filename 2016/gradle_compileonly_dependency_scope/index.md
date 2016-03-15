# Gradle compileOnly (provided) dependency scope for Java is here

I think this is long waiting one functionality for Gradle [Java](https://docs.gradle.org/2.12/userguide/java_plugin.html) plug-in, at least it is for me. In case if you are working on the libraries, and you don't want to force users to upgrade transitive dependencies.

What is this about... from Gradle version 2.12 and it's Java plug-in there is couple of new dependency configurations ```compileOnly```, ```compileClasspath```, ```testCompileOnly```, ```testClasspath```.
There are other useful new features like test filtering support, IDEA integration improvements, but for more details you can read [release notes](https://docs.gradle.org/2.12/release-notes)


Most important one are: 

  - compileOnly
  	
  	It will add dependency only for compile time, but those dependency will not be available during runtime. Important thing here is that those dependency are not available when compiling the tests. That's why there is _testCompileOnly_.
  	
  - testCompileOnly
    
    Is used to add dependency only for compile time, but for the test source


 I found those dependency declaration useful when I'm producing some kind of internal library, and that library has dependencies for which I know other component which will use that library are already using it. And I don't want to force other components to upgrade their dependencies, for example to the latest version of that dependency.

 Then you can use:

	dependencies {
	    compileOnly 'javax.servlet:servlet-api:3.1.0'
	}