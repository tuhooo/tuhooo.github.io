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
