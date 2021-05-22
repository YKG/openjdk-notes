LD_LIBRARY_PATH=/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/lib gdbserver :1234 build/linux-x86_64-normal-server-slowdebug/jdk/bin/java -agentlib:minst -Xbootclasspath/a:/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/minst.jar -version


LD_LIBRARY_PATH=/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/lib gdbserver :1234 build/linux-x86_64-normal-server-slowdebug/jdk/bin/java -agentlib:minst -Xbootclasspath/a:/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/minst.jar -version


handle SIGSEGV nostop noprint pass


https://intellij-support.jetbrains.com/hc/en-us/articles/360001436079-Collecting-additional-logs-in-CLion-

#com.jetbrains.cidr.execution.debugger 


scp amd:/lib/x86_64-linux-gnu/libc.so.6 /d/repo/openjdk-jdk8u/sysroot/lib/x86_64-linux-gnu/libc.so.6

scp amd:/lib/x86_64-linux-gnu/* /d/repo/openjdk-jdk8u/sysroot/lib/x86_64-linux-gnu/


mkdir /d/repo/openjdk-jdk8u/sysroot/lib64
scp amd:/lib64/* /d/repo/openjdk-jdk8u/sysroot/lib64

这之后可以使用sysroot下断点了。


