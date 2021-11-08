# java native interface -- example

## Prerequisites
* java JAVA_HOME maven
* c++ gcc cmake

## Quick start

### javah c++.h
```
 javah -d ../../../cpp com.lorne.jni.JNIDemo
 
```

### c++ impl
```
//
// Created by lorne on 2021/11/8.
//
#include "jni.h"
#include "stdio.h"
#include "com_lorne_jni_JNIDemo.h"
#include "cstring"

extern "C"{
    JNIEXPORT void JNICALL Java_com_lorne_jni_JNIDemo_hi(JNIEnv *env, jobject obj, jstring str){
        char* jnistr = (char *) env->GetStringUTFChars(str, NULL);
        printf("Hello, %s\n",jnistr);
    }

    JNIEXPORT jstring JNICALL Java_com_lorne_jni_JNIDemo_getName(JNIEnv *env, jobject obj){
         char* jnistr = "lorne";
         return env -> NewStringUTF(jnistr);
    }
}

```

### export lib (macos) 
```  

 gcc -fPIC -I$JAVA_HOME/include -I$JAVA_HOME/include/darwin -shared -o ../jnilib/libJNIDemo.jnilib.dylib JNIDemo.cpp

```

### jni test
```
mvn clean test
```
