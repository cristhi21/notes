# [Gradle tutorial](https://www.youtube.com/watch?v=R6Z-Sxb837I)

### gradle wrapper

is not necessary install gradle in your local machine,
gladle wrapper can do the project run with the latest compiling version

### Install gradle with sdkman

```sh
sdk install gradle 8.2
```
### create new gradle project

```sh
# Init new gradle project
gradle init 

# Get gradlew version
./gradlew --version

# Get help
./gradlew help

# Run task
./gradlew tasks

# Get/update dependencies
./gradlew dependencies


ls -l
crvargas@LCO-PF1LPXZC:/mnt/c/projects/examples/get-going-with-gradle$ ls -l
total 16
-rwxrwxrwx 1 crvargas crvargas  201 Mar  6 18:53 build.gradle.kts -> the mann script
drwxrwxrwx 1 crvargas crvargas 4096 Mar  6 18:52 gradle
-rwxrwxrwx 1 crvargas crvargas 8527 Mar  6 18:52 gradlew
-rwxrwxrwx 1 crvargas crvargas 2868 Mar  6 18:52 gradlew.bat
-rwxrwxrwx 1 crvargas crvargas  359 Mar  6 18:53 settings.gradle.kts


# Compile java project
./gradlew compileJava

# Get resources in folder build
./gradlew ProcessResources

# Create jar file
./gradlew jar

# Run tests
./gradlew test
```

### Define dependencies

```kts
plugins {
    java
}

// To manifest main class
tasks.named<Jar>("jar") {
    manifest {
        attributes["Main-Class"] = "com.gradlehero.languageapp.Hello"
    }
}

repositories {
    mavenCentral()
}

dependencies {
    testImplementation("org.junit.jupiter:junit-jupiter:5.10.2")
}

// Adopted Junit5
tasks.named<Test>("test") {
    useJUnitPlatform()
}
```

implementation -> Para las dependencias requeridas durante la compilacion y ejecucion de su codigo

testImplementation -> Para las dependencias requeridas durante la compilacion y ejecucion de sus pruebas


[Setter a gradlew version](https://github.com/gradle/gradle/releases)
```sh
# Setter a gradlew version
./gradlew wrapper --gradle-version=8.7-rc-2

# See all tasks
./gradlew tasks --all

./gradlew compileJava

./gradlew processResources

./gradlew jar

# test
./gradlew test
# build/reports/tests/test/index.html
```

## See three dependencies
> gradle app:dependencies
