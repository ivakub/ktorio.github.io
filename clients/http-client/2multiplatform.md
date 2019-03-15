---
title: Multiplatform
category: clients
permalink: /clients/http-client/multiplatform.html
caption: Multiplatform Http Client 
---

The HTTP Client supports several platforms, using the experimental [multiplatform support](https://kotlinlang.org/docs/reference/multiplatform.html)
that was introduced in [Kotlin 1.2](https://blog.jetbrains.com/kotlin/2017/11/kotlin-1-2-released/).

Right now, the supported platforms are JVM, Android and iOS, but in future versions, there will be more supported.

## Android

For Android, in your project's `build.gradle` (or `build.gradle.kts`) you just have include the following artifact to your `dependencies` block:

```kotlin
dependencies {
    // ...
    implementation("io.ktor:ktor-client-android:$ktor_version")
    // ...
}
```

You can then use Android Studio, or gradle to build your project.

## iOS

In the case of iOS, you have to use [Kotlin/Native](https://github.com/JetBrains/kotlin-native), and analogously
to android, you have to put this artifact as part of the `dependencies` block. 

```kotlin
dependencies {
    // ...
    implementation("io.ktor:ktor-client-ios:$ktor_version")
    // ...
}
```

In the case of iOS, we normally create a `.framework`, and the application project is a normal XCode project
written either in Swift or Objective-C that includes that framework.
So you first have to build the framework using the gradle tasks exposed by Kotlin/Native,
and then open or build the XCode project. 

## Common

For [multiplatform projects](https://kotlinlang.org/docs/reference/multiplatform.html) that for example
share code between Android and iOS, we can create a common module.
That common module can only access APIs that are available on all the targets.
Ktor HTTP Client exposes a common module that can be used for such projects:

```kotlin
dependencies {
    // ...
    implementation("io.ktor:ktor-client-core:$ktor_version")
}
```

## Samples

There is a full sample using the common client in the ktor-samples repository:

* [mpp/client-mpp](https://github.com/ktorio/ktor-samples/tree/master/mpp/client-mpp)

You can use this project as reference. This project also expose some experimental gradle tasks to build, install and run the
Android and iOS applications directly from gradle.

### Android:

* `:client-mpp-android:emulatorList` - lists all the available emulators
* `:client-mpp-android:emulatorStart` - starts the emulator (this would block gradle for now, so better to do in a separate terminal)
* `:client-mpp-android:emulatorInstall` - install the application inside the emulator
* `:client-mpp-android:emulatorRun` - executes the application inside the emulator

### iOS:

* `:client-mpp-ios:startSimulator` - starts the simulator
* `:client-mpp-ios:shutdownSimulator` - shutdowns the simulator
* `:client-mpp-ios:buildXcode` - builds the XCode project that uses the .framework from Kotlin/Native
* `:client-mpp-ios:installSimulator` - installs the application inside the simulator
* `:client-mpp-ios:launchSimulator` - executes the application inside the simulator

