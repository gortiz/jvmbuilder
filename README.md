# JvmBuilder
[ ![Download](https://api.bintray.com/packages/jffiorillo/jvmbuilder/jvmbuilder/images/download.svg) ](https://bintray.com/jffiorillo/jvmbuilder/jvmbuilder/_latestVersion)

A source code generator for [Kotlin](https://kotlinlang.org/) data classes to automatically create a Builder class. 

# How to use JvmBuilder

When annotating a Kotlin `data class` with `@JvmBuilder` 
``` 
@JvmBuilder
data class Test(val foo: Int = 1, val bar: String)
```

The following class is generated 
```
// Code auto-generated by JvmBuilder. Do not edit.
package com.example

import kotlin.Int
import kotlin.String

class JvmBuilder_Test {
    private var foo: Int? = null

    private var bar: String? = null

    fun foo(foo: Int): JvmBuilder_Test {
        this.foo = foo
        return this
    }

    fun bar(bar: String): JvmBuilder_Test {
        this.bar = bar
        return this
    }

    fun build(): Test {
        var result = com.example.Test(bar = this.bar!!)
        result = result.copy(foo = this.foo ?: result.foo)
        return result
    }
}
```

This provides a `Builder` class that can be used in Java to create your Kotlin `Test` `data class` using the default values and following a [`Builder Pattern`](https://en.wikipedia.org/wiki/Builder_pattern).

The following Java code generates a `Test` instance with `foo = 1` (taking the 1 from the default `Kotlin` constructor) and `bar = "bar"`.
```
new Jvm_Builder().bar("bar").build()
```

## Gradle

Gradle users should add the dependencies in their `build.gradle` file:

```
dependencies {
  implementation "io.github.jffiorillo:builder-annotations:<latest_version>"
  kapt "io.github.jffiorillo:builder:<latest_version>"
}
```

## Maven

Maven users should add the dependencies in their `pom.xml` file:

```
<dependency>
  <groupId>io.github.jffiorillo</groupId>
  <artifactId>builder-annotations</artifactId>
  <version>{latest_version}</version>
</dependency>
<dependency>
  <groupId>io.github.jffiorillo</groupId>
  <artifactId>builder</artifactId>
  <version>{latest_version}</version>
  <scope>provided</scope>
</dependency>
```


## Benefit 

  * In order to have a good Kotlin interoperability with [Java](https://en.wikipedia.org/wiki/Java_(programming_language)), you can use 
  this tool to generate automatically generate Builders for your data classes that are accessible from Java consumers.
  * The time of executing the annotation processor is really slow because uses the [kotlin-metadata](https://github.com/Takhion/kotlin-metadata) instead of reflection.
   
