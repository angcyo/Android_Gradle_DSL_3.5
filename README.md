# Android_Gradle_DSL_3.5
`com.android.tools.build:gradle:3.5.0`

`gradle-5.4.1-all`

# 参考 Android_Gradle_DSL_3.3
https://github.com/angcyo/Android_Gradle_DSL_3.3

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


## `task`的3个阶段

```groovy
task _testTask()
    doFirst{
        println "task first."
    }

    doLast{
        println "task last."
    }

    println "task配置结束."
}

```

> 1. 配置阶段, 任何时候都会执行
> 2. First阶段, 任务运行最开始会执行
> 3. Last, 任务运行最后面会执行

---

## 监听`task``事件`

### 监听`task`添加

```groovy
task _testTask() {
    project.tasks.whenTaskAdded {
        println "添加任务:" + it.name + ":" + it.class + ":" + it
    }
}

```

**示例**

正则匹配目标`task`, 追加命令

```groovy
task _testTask() {
    project.tasks.whenTaskAdded {
        def taskName = it.name
        if (taskName.endsWith("JavaWithJavac")) {
            def matcher = Pattern.compile("compile(.*)JavaWithJavac").matcher(taskName)

            if (matcher.find()) {
                println "匹配:" + taskName + "->" + matcher.group(1)
            }
        }
    }
}
```

