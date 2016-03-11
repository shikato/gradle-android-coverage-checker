# gradle-android-coverage-check

AndroidCoverageCheck is a gradle plugin to check coverage reports.  

![demo1](https://qiita-image-store.s3.amazonaws.com/0/47437/27441815-8d99-66cd-c214-02ff383c1ce8.png)
 
## Install
**build.gradle**  

Build script snippet for use in all Gradle versions:
```groovy
buildscript {
  repositories {
    maven {
      url "https://plugins.gradle.org/m2/"
    }
  }
  dependencies {
    classpath "gradle.plugin.org.shikato.gradle.android.coverage.check:gradle-android-coverage-check:0.0.5"
  }
}

apply plugin: "org.shikato.gradle.android.coverage.check"
```

Build script snippet for new, incubating, plugin mechanism introduced in Gradle 2.1:
```
plugins {
  id "org.shikato.gradle.android.coverage.check" version "0.0.5"
}
```

## Usage

### Task
* androidCovrageCheck - Checks coverage reports.  

#### Examples
##### Create coverage reports & check
Only at the time of "org.gradle.parallel=false".
```
./gradlew createDebugCoverageReport androidCoverageCheck  
```

##### Only check
report.xml should have already existed.
```
./gradlew androidCoverageCheck  
```

### Options
**build.gradle**

```groovy
// Excluded targets
// Default: []
String[] excludeFiles = ["**/*Activity.java",
                         "**/*Fragment.java",
                         "package/name/**/Shikato2.java"];

// coverage reports path
// If reports are plural, The task checks each.
// Default: ["**/coverage/**/report.xml"]
String[] reportXmlPath = ["hoge/fuga/**/report.xml"];

androidCoverageCheck {
    // If there are unsatisfied coverages, this option will make a build failure.
    // Default: true
    isBuildFailure false

    // minimum threshold of INSTRUCTION
    // Default: 20
    instruction 50

    // minimum threshold of BRANCH
    // Default: 20
    branch 50

    // set excluded targets
    excludes excludeFiles
    // set coverage report path
    reportXml reportXmlPath
}

```

## Documents
[Qiita](http://qiita.com/shikato/items/9869719ab5e22ee9d061)

## License
MIT
