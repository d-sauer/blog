# Introduction to Gradle

Brief history of building tools starts with Make, which is maybe an overly complex solution. And it’s not so platform independent. After that evolution continues with Ant, which is XML based and it has its pros and cons. Ant is still used for scriptings and there are still good use cases for it. 

Today we have more and more complex projects and we need to incorporate different technologies, languages and support all kinds build strategies. To support rapid changes of the landscape of modern software development, we are probably using Maven, as the next evolution step. We can easily incorporate different modules and libraries in our final product. Maven brings the philosophy of convention over configuration. And it brings lot advantages to JVM ecosystem, but XML is still here. One of Maven “killer feature” is that it will check your project dependencies and pull new versions from upstream. Maven also supports plugins, so you can extend the functionalities of your build process.

After all, we are coming to the Gradle, as the next evolutionary step in JVM build tools. As with each evolutionary step, Gradle has incorporate learned lessons from Ant and Maven, and move those concepts and best ideas to the next level.

First and main difference between Maven and Gradle, that there is no XML syntax anymore. Gradle allows declaratively modeling your problem domain using a powerful and expressive DSL implemented in Groovy as a first citizen language. And because is JVM native, it allows you to write custom logic in Java or Groovy. 
    
Gradle tends to be flexible as much as possible, by that you can change some of convention-over-configuration principles. For example, if you have a different project structure from convention, it’s possible to configure build script to be aligned with different folder structure, which is specially acceptable for older projects. Lots of project are using different technologies and languages on client and server side. And we always looking for the best way to incorporate those technologies in our final product. By that Gradle fits right into that place, by providing expressive DSLs and to abandon XML, and convention over configuration approach with the ability for to bend that rule if needed. And it also provides powerful dependency management.

![Picture 1. Union of Gradle technologies][image1]





[image1]: https://raw.githubusercontent.com/d-sauer/blog/7edbab9d5d7ea9b2689ecb69d9ed3b4f3f1f3801/2015/introduction_to_gradle/image01.png "Picture 1. Union of Gradle technologies"
