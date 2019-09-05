# Android_Gradle_DSL_3.5
`com.android.tools.build:gradle:3.5.0`

`gradle-5.4.1-all`

# 参考 Android_Gradle_DSL_3.3
https://github.com/angcyo/Android_Gradle_DSL_3.3

# Gradle 常规操作

## 声明一个`task`

```groovy
task _test1(){
    
}
```

## 声明一个带`type`的`task`

```groovy
task _test2(type: Jar){
    
}
```

[所有可用`type`](https://docs.gradle.org/current/dsl/#N1042A)


## 监听`task``事件`

### 监听`task`添加

```
task _testTask() {
    println project.tasks.whenTaskAdded {
        println "添加任务:" + it.name + ":" + it.class + ":" + it
    }
}

```

