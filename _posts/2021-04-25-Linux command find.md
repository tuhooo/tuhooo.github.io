---
layout: post
title: "Linux command find"
category: linux
---





## Use find and grep to search code

Use `find` and `grep` to search something in src tree is very quick and convenient.



```
find . -path ./build -prune -o  -path ./test -prune -o  -type f -regex ".*\.c\|.*\.cpp"  -print | xargs  grep "JNIEnv"  -n -s -I --color
find . -path ./build -prune -o  -path ./test -prune -o  -type f -regex ".*\.c\|.*\.cpp"  -print | xargs  grep "jni_environment"  -n -s -I --color
find . -path ./build -prune -o  -path ./test -prune -o  -type f -regex ".*\.h\|.*\.hpp"  -print | xargs  grep "jni_environment"  -n -s -I --color
```



Explain:

* `-path ./build -prune -o` : exclude ./build dir before search
* `-type f` : search document's type is file
* `-print` : output find result
* `xargs` : TODO
* `-n` : grep line number
* `-s` : silent
* `-I` : TODO
* `--color` : highlight search content
* `-regex ".*\.h|.*\.hpp"` : suffix filter



