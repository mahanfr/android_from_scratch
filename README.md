# Android from Sgroovygroovygroovygroovycratch

A Template of a very basic android app made without using android studio

This repository serves as a template for Android projects, configured with best practices and solutions to common issues encountered during setup.

## 📁 Project Structure

``` txtgroovygroovy
android_project_template/
├── app/
│   ├── build.gradle        # Module-level Gradle config
│   ├── src/
│   │   ├── main/
│   │   │   ├── AndroidManifest.xml
│   │   │   ├── java/       # Main Java/Kotlin source code
│   │   │   └── res/        # Resources (layouts, strings, etc.)
│   └── proguard-rules.pro  # Obfuscation rules
├── build.gradle            # Project-level Gradle config
├── settings.gradle         # Project modules definition
├── gradle.properties       # Gradle and Android properties
└── README.md               # This file
```

## 🛠️ Configuration Files Explained
1. settings.gradle

Defines project modules and plugin repositories:
``` groovy
pluginManagement {
    repositories {
        google()  // Android Gradle Plugin
        mavenCentral()
    }
}

dependencyResolutionManagement {
    repositories {
        google()  // AndroidX libraries
        mavenCentral()
    }
}

include ':app'  // Main application module
```

2. gradle.properties

Project-wide Gradle settings:

``` groovy
# AndroidX configuration
android.useAndroidX=true
android.enableJetifier=true

# Gradle performance
org.gradle.jvmargs=-Xmx2048m -Dfile.encoding=UTF-8
org.gradle.parallel=true
```

3. Project-level build.gradle

``` groovy
buildscript {
    repositories {
        google()
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:7.4.2'  # AGP version
    }
}

allprojects {
    repositories {
        google()
        mavenCentral()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

4. Module-level app/build.gradle

``` groovy

plugins {
    id 'com.android.application'
}

android {
    namespace 'com.example.template'
    compileSdk 34

    defaultConfig {
        applicationId "com.example.template"
        minSdk 21
        targetSdk 34
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_11
        targetCompatibility JavaVersion.VERSION_11
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.9.0'
}
```

## 🚨 Common Issues & Solutions
1. Manifest Merging Errors

Problem:

Manifest merger failed : android:exported needs to be explicitly specified

Solution:
Add android:exported to all components with intent filters:

``` xml

<activity 
    android:name=".MainActivity"
    android:exported="true|false">
```

2. Dependency Resolution Failures

Problem:

Could not resolve com.android.tools.build:gradle:X.X.X

Solutions:

    Verify google() repository is declared

    Check internet connection/proxy settings

    Run ./gradlew --refresh-dependencies

3. Java Version Conflicts

Problem:

Could not determine Java version from '17.0.X'

Solutions:

    Update Gradle wrapper to version 8.x+

    Or downgrade to JDK 11 (LTS version)

4. Missing SDK Components

Problem:

Failed to find target with hash string 'android-34'

Solution:
Install missing SDK platforms:

``` bash
sdkmanager "platforms;android-34" "build-tools;34.0.0"
```

## 🏗️ How to Use This Template

    Create new repository using this template

    Update configuration:

        Change namespace in app/build.gradle

        Update applicationId in defaultConfig

    Sync Gradle and start coding!

## 🔧 Recommended Tools

    JDK: 11 or 17 (set JAVA_HOME)

    Android Studio: Latest stable version

    Gradle: Wrapper included (v8.0+)

## 📜 License

This template is open-source and available under the MIT License.

This README provides comprehensive documentation while addressing the specific issues you encountered during project setup. The template includes all necessary configurations with explanations for each critical file.
