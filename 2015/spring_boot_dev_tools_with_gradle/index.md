# Continuous Autoreload with Spring Boot Dev tools and Gradle

With the recent release of [Spring Boot 1.3](http://projects.spring.io/spring-boot/) there is a new dependency in town [Spring Boot Dev Tools](https://spring.io/blog/2015/06/17/devtools-in-spring-boot-1-3). Which enable us to automatically reload Spring Boot application if some classes in class path has changed.

This is quite handy for local development, but still you need to trigger build phase, to re/compile the class. In this case we can use [Gradle continuous build](https://docs.gradle.org/current/userguide/continuous_build.html) feature, and automatically rebuild our project, and Spring Boot DevTools will pick up changes and restart application.

One way to do it is add the necessary dependencies to your ```build.gradle```:

	buildscript {
	    dependencies {
	        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.0.RELEASE")
	    }
	    repositories {
	        mavenCentral()
	    }
	}
	
	apply plugin: 'java'
	apply plugin: 'spring-boot'
	
	repositories {
	    mavenCentral()
	    jcenter()
	}
	
	configurations {
	    dev
	}
	
	dependencies {
	    compile("org.springframework.boot:spring-boot-starter-web:1.3.0.RELEASE")
	    compile 'org.slf4j:slf4j-api:1.7.13'
	
	    dev("org.springframework.boot:spring-boot-devtools")
	}
	
	bootRun {
		// Use Spring Boot DevTool only when we run Gradle bootRun task
	    classpath = sourceSets.main.runtimeClasspath + configurations.dev
	}


We need to open two terminals:

1. At the first terminal start Gradle build as continuous task:
    ```gradle build --continuous```
2. At second terminal start the Gradle bootRun task: ```gradle bootRun```

A working example can be found [here](https://github.com/d-sauer/tests/tree/master/sbdt).


![Screenshot of two terminal](https://raw.githubusercontent.com/d-sauer/blog/master/2015/sbdt/console.png "Screenshot of two terminal")




