# Checkstyle rules for Java projects

## Usage with Gradle

```groovy
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.ksprojects:java-code-style:1.0-SNAPSHOT'
    }
}

apply plugin: 'checkstyle'
checkstyle {
    config = resources.text.fromString(getClass().getResource("checkstyle.xml").text)
    toolVersion = '7.6.1'
    // Exclude generated code from Checkstyle checks
    checkstyleMain.source = "src/main/java"
    checkstyleTest.source = "src/test/java"
}
```

## Usage with Maven

TBD