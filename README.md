# Checkstyle rules for Java projects

## Usage

When you add checkstyle plugin to your project, build should fail 
if at lease one rule is violated.

### Gradle

```groovy
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath 'org.ksprojects:java-code-style:1.1'
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

### Maven

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-checkstyle-plugin</artifactId>
            <version>2.17</version>
            <executions>
                <execution>
                    <id>validate</id>
                    <phase>validate</phase>
                    <configuration>
                        <configLocation>checkstyle.xml</configLocation>
                        <encoding>UTF-8</encoding>
                        <consoleOutput>true</consoleOutput>
                        <failsOnError>true</failsOnError>
                        <!-- Exclude generated sources -->
                        <sourceDirectories>
                            <directory>${project.basedir}/src/main/java</directory>
                        </sourceDirectories>
                        <testSourceDirectories>
                            <directory>${project.basedir}/src/test/java</directory>
                        </testSourceDirectories>
                    </configuration>
                    <goals>
                        <goal>check</goal>
                    </goals>
                </execution>
            </executions>
            <dependencies>
                <dependency>
                    <groupId>com.puppycrawl.tools</groupId>
                    <artifactId>checkstyle</artifactId>
                    <version>7.6.1</version>
                </dependency>
                <dependency>
                    <groupId>org.ksprojects</groupId>
                    <artifactId>java-code-style</artifactId>
                    <version>1.1</version>
                </dependency>
            </dependencies>
        </plugin>
    </plugins>
</build>
```
