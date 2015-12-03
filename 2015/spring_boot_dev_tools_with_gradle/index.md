# Continous Autoreload with Spring Boot + Developer tools and Gradle

With recent release of [Spring Boot 1.3](http://projects.spring.io/spring-boot/) there is new dependency in town [Spring Boot Dev Tools](https://spring.io/blog/2015/06/17/devtools-in-spring-boot-1-3). Which enable as to automatically reload Spring Boot application if some classes on class path has changed.

This is quite handy for local development, but still you need to triger build phase, to re/compile class. In this case we can use Gradle continous feature, and automatically rebuild our project, and Spring Boot DevTools will pickup changes and restart application.

One way to do it is add necessary dependencies to your ```build.gradle```:

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
		// Use Spring Boot DevTool only when we run gradle bootRun task
	    classpath = sourceSets.main.runtimeClasspath + configurations.dev
	}


And then open two terminals:

1. In first terminal start gradle build as continous task:
    ```gradle build --continuous```
2. In second terminal start gradle bootRun task: ```gradle bootRun```

Working example can be found [here](https://github.com/d-sauer/tests/tree/master/sbdt).


![Screenshot of two terminal](https://raw.githubusercontent.com/d-sauer/blog/master/2015/sbdt/console.png "Screenshot of two terminal")




