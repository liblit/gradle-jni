# Gradle JNI

[![Build status](https://ci.appveyor.com/api/projects/status/4a80h0wnii4t7bf0/branch/master?svg=true)](https://ci.appveyor.com/project/ThadHouse/gradle-jni/branch/master)

gradle-jni is a utility library for enabling easy to build JNI compatible plugins

```gradle
plugins {
  id 'c' // use 'cpp' here instead of 'c' if implementing native methods using C++ instead of C
  id 'edu.wpi.first.GradleJni' version '0.2.1'
}

model {
  components {
    library(JniNativeLibrarySpec) { // Use JniNativeLibrarySpec to get a JNI library
      enableCheckTask true // Set to true to enable a JNI check task. This will search all generated JNI headers, and check to ensure their symbols exist in the native library
      javaCompileTasks << compileJava // set javaCompileTasks to any java compile tasks that contain your JNI classes. It is a list of tasks
      jniCrossCompileOptions << JniCrossCompileOptions('athena')
      // See below for more JniCrossCompileOptions
    }
  }
}
```

Below are the options for JniCrossCompileOptions
```
JNICrossCompileOptions('toolChainName') // Use this to match the cross compile options to a specific tool chain name
JNICrossCompileOptions('operatingSystem', 'architecture') // Use this to match the cross compile options to a specific tool chain arch and os.

// For both of these options, they take an optional last parameter of List<String> of directories
If this parameter is added, the directories passed in will be used for the include paths for the JNI headers. 
If this parameter is not passed in, for any matching toolchain, a set of headers included in the plugin will be used. These headers are standard for 32 bit embedded arm toolchains.
```
