LD_LIBRARY_PATH=/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/lib \
build/linux-x86_64-normal-server-slowdebug/jdk/bin/java -agentlib:minst -Xbootclasspath/a:/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/minst.jar -version

LD_LIBRARY_PATH=/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/lib \
gdbserver :1234 \
build/linux-x86_64-normal-server-slowdebug/jdk/bin/java -agentlib:minst -Xbootclasspath/a:/home/ubuntu/repo/openjdk-jdk8u/build/linux-x86_64-normal-server-slowdebug/jdk/demo/jvmti/minst/minst.jar -version