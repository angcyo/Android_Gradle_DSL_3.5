# Android_Gradle_DSL_3.5
`com.android.tools.build:gradle:3.5.0`

`gradle-5.4.1-all`

# 参考 Android_Gradle_DSL_3.3
https://github.com/angcyo/Android_Gradle_DSL_3.3

# Groovy

`gradle` 构建脚本使用的 `groovy` 语言编写.

官方地址:
[http://groovy-lang.org/documentation.html](http://groovy-lang.org/documentation.html)

API文档地址:
[http://groovy-lang.org/api.html](http://groovy-lang.org/api.html)

API扩展文档地址:
[http://groovy-lang.org/gdk.html](http://groovy-lang.org/gdk.html)

---

# Gradle

官方文档: [https://docs.gradle.org/current/userguide/userguide.html](https://docs.gradle.org/current/userguide/userguide.html)

接口/对象 | 默认实现
---|---
project | org.gradle.api.internal.project.DefaultProject
project.tasks | org.gradle.api.internal.tasks.DefaultTaskContainer
task | org.gradle.api.DefaultTask



任务类型(task type) | 默认实现
---|---
type: Jar | org.gradle.api.tasks.bundling.Jar
type: Copy | org.gradle.api.tasks.Copy
type: Zip | org.gradle.api.tasks.bundling.Zip
type: Delete | org.gradle.api.tasks.Delete
type: Exec | org.gradle.api.tasks.Exec
... | println it.class


`task` 官方介绍: 

https://docs.gradle.org/current/dsl/org.gradle.api.Task.html

---

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

## 声明一个带有依赖的`task`

```groovy
task _testTask(dependsOn: ['compileApkReleaseJavaWithJavac'], type: Jar) {

}
```

## 动态创建一个`task`

```groovy
def newTask = project.tasks.create("newTask")
newTask.doFirst {
    println "new task first." + it.name
}
newTask.doLast {
    println "new task last." + it.name
}
project.tasks.add(newTask)

```



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

### 系列`Gradle`操作文章

[https://angcyo.blog.csdn.net/article/category/9283298](https://angcyo.blog.csdn.net/article/category/9283298)

---

## 未完待续

持续更新...


