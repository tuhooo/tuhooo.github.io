---
layout: post
title: "OpenJDK main execute routine"
category: openjdk
---

## Entry point of main function

The very `entry point` is in file:
```
src/java.base/share/native/launcher/main.c
```

As shown below:

```
JNIEXPORT int
main(int argc, char **argv)
{
    printf("main函数开始了....\n");
    int margc;
    char** margv;
    int jargc;
    char** jargv;
    const jboolean const_javaw = JNI_FALSE;
#endif /* JAVAW */
    {
        int i, main_jargc, extra_jargc;
        
    // some code is omitted.
        
    printf("参数乱起八糟的都处理了, 现在准备进入到了JLI_Launch中.............\n");
    // TODO yangxu 2021/4/14 所以JLI究竟是什么意思？
    return JLI_Launch(margc, margv,
                   jargc, (const char**) jargv,
                   0, NULL,
                   VERSION_STRING,
                   DOT_VERSION,
                   (const_progname != NULL) ? const_progname : *margv,
                   (const_launcher != NULL) ? const_launcher : *margv,
                   jargc > 0,
                   const_cpwildcard, const_javaw, 0);

}
```

## Key node of runtime

```


main(int argc, char **argv)                 invoked in: src/java.base/share/native/launcher/main.c
return JLI_Launch(margc, margv              invoked in: src/java.base/share/native/launcher/main.c
InitLauncher(javaw)                         invoked in: src/java.base/share/native/libjli/java.c
CreateExecutionEnvironment(&argc, &argv     invoked in: src/java.base/share/native/libjli/java.c
LoadJavaVM(jvmpath, &ifn)                   invoked in: src/java.base/share/native/libjli/java.c
JVMInit(&ifn, threadStackSize               invoked in: src/java.base/share/native/libjli/java.c
ContinueInNewThread                         invoked in: src/java.base/unix/native/libjli/java_md.c
ifn->GetDefaultJavaVMInitArgs(&args1_1);    invoked in: src/java.base/share/native/libjli/java.c
CallJavaMainInNewThread                     invoked in: src/java.base/share/native/libjli/java.c
ThreadJavaMain                              invoked in: src/java.base/unix/native/libjli/java_md.c
JavaMain                                    invoked in: src/java.base/unix/native/libjli/java_md.c
InitializeJVM(&vm, &env, &ifn)              invoked in: src/java.base/share/native/libjli/java.c
ifn->CreateJavaVM(pvm,                      invoked in: src/java.base/share/native/libjli/java.c
   

```

`JLI_Launch` is defined in: `src/java.base/share/native/libjli/java.c`

`InitLauncher(javaw)` is defined in: ``


`jvmtype = CheckJvmType(pargc, pargv, JNI_FALSE);`


`GetJVMPath(jrepath, jvmtype, jvmpath, so_jvmpath)`


jvmpath="/home/egova/openjdk/build/linux-x86_64-server-slowdebug/jdk/lib/server/libjvm.so"


After `LoadJavaVM`, ifn gets three addresses:
* JNI_CreateJavaVM
* JNI_GetDefaultJavaVMInitArgs
* JNI_GetCreatedJavaVMs

