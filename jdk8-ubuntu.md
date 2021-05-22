# JDK8 BUILD Ubuntu 20.04 WSL

- source: jdk8-b120

- JDK7

    https://download.java.net/openjdk/jdk7u75/ri/jdk_ri-7u75-b13-linux-x64-18_dec_2014.tar.gz


> bash ./configure --with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri

checking for unzip... no
configure: Could not find unzip!
configure: error: Cannot continue
configure exiting with result code 1


> apt install unzip


checking for zip... no
configure: Could not find zip!
configure: error: Cannot continue
configure exiting with result code 1


> apt install zip

checking for X... no
configure: error: Could not find X11 libraries. You might be able to fix this by running 'sudo apt-get install libX11-dev libxext-dev libxrender-dev libxtst-dev libxt-dev'.
configure exiting with result code 1

> sudo apt-get install libx11-dev libxext-dev libxrender-dev libxtst-dev libxt-dev

checking for cups headers... no
configure: error: Could not find cups! You might be able to fix this by running 'sudo apt-get install libcups2-dev'.
configure exiting with result code 1

> sudo apt-get install libcups2-dev

configure: error: Can not find or use freetype at location given by --with-freetype
configure exiting with result code 1

> bash ./configure --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri

configure: error: Could not find freetype! You might be able to fix this by running 'sudo apt-get install libfreetype6-dev'.
configure exiting with result code 1s

> sudo apt-get install libfreetype6-dev

> bash ./configure --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri

configure: error: Could not find freetype! You might be able to fix this by running 'sudo apt-get install libfreetype6-dev'.
configure exiting with result code 1

> bash ./configure --with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri


configure: error: Could not find alsa! You might be able to fix this by running 'sudo apt-get install libasound2-dev'.
configure exiting with result code 1


> sudo apt-get install libasound2-dev

> bash ./configure --with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri


====================================================
A new configuration has been successfully created in
/mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug
using configure arguments '--with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri'.

Configuration summary:
* Debug level:    slowdebug
* JDK variant:    normal
* JVM variants:   server
* OpenJDK target: OS: linux, CPU architecture: x86, address length: 64

Tools summary:
* Boot JDK:       openjdk version "1.7.0_75" OpenJDK Runtime Environment (build 1.7.0_75-b13) OpenJDK 64-Bit Server VM (build 24.75-b04, mixed mode)  (at /home/ubuntu/java-se-7u75-ri)
* C Compiler:     x86_64-linux-gnu-gcc-9 (Ubuntu 9.3.0-17ubuntu1~20.04) version 9.3.0 (at /usr/bin/x86_64-linux-gnu-gcc-9)
* C++ Compiler:   x86_64-linux-gnu-g++-9 (Ubuntu 9.3.0-17ubuntu1~20.04) version 9.3.0 (at /usr/bin/x86_64-linux-gnu-g++-9)

Build performance summary:
* Cores to use:   11
* Memory limit:   12269 MB
* ccache status:  not installed (consider installing)

Build performance tip: ccache gives a tremendous speedup for C++ recompilations.
You do not have ccache installed. Try installing it.
You might be able to fix this by running 'sudo apt-get install ccache'.

WARNING: Your build output directory is not on a local disk.
This will severely degrade build performance!
It is recommended that you create an output directory on a local disk,
and run the configure script again from that directory.

cat: standard output: No such file or directory


> 参考 https://openjdk.java.net/groups/build/doc/building.html Disk Speed

> mkdir ~/repo/jdk-build
> ln -s ~/repo/jdk-build build


这个之后，没有local disk提示了

> 参考 https://github.com/libffi/libffi/issues/552 用以修复

cat: standard output: No such file or directory

> 在VM Ubuntu中，locate

ubuntu@amd:~/repo/openjdk$ locate config.log
/home/ubuntu/repo/openjdk/build/linux-x86_64-normal-server-release/config.log
ubuntu@amd:~/repo/openjdk$

ubuntu@amd:~/repo/openjdk$ grep -rn config.log common/
...
common/autoconf/generated-configure.sh:37321:if test -e ./config.log; then
common/autoconf/generated-configure.sh:37322:  $MV -f ./config.log "$OUTPUT_ROOT/config.log" 2> /dev/null

> 修改WSL中的 generated-configure.sh

ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$ vi common/autoconf/generated-configure.sh
... 
37320 # Try to move the config.log file to the output directory.
37321 #  $MV -f ./config.log "$OUTPUT_ROOT/config.log" 2> /dev/null
37322 if test -e ./config.log; then
37323   cp -f ./config.log "$OUTPUT_ROOT/config.log" 2> /dev/null
37324 fi


>  bash ./configure --with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri


...


====================================================
A new configuration has been successfully created in
/mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug
using configure arguments '--with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri'.

Configuration summary:
* Debug level:    slowdebug
* JDK variant:    normal
* JVM variants:   server
* OpenJDK target: OS: linux, CPU architecture: x86, address length: 64

Tools summary:
* Boot JDK:       openjdk version "1.7.0_75" OpenJDK Runtime Environment (build 1.7.0_75-b13) OpenJDK 64-Bit Server VM (build 24.75-b04, mixed mode)  (at /home/ubuntu/java-se-7u75-ri)
* C Compiler:     x86_64-linux-gnu-gcc-9 (Ubuntu 9.3.0-17ubuntu1~20.04) version 9.3.0 (at /usr/bin/x86_64-linux-gnu-gcc-9)
* C++ Compiler:   x86_64-linux-gnu-g++-9 (Ubuntu 9.3.0-17ubuntu1~20.04) version 9.3.0 (at /usr/bin/x86_64-linux-gnu-g++-9)

Build performance summary:
* Cores to use:   11
* Memory limit:   12269 MB
* ccache status:  not installed (consider installing)

WARNING: The result of this configuration has overridden an older
configuration. You *should* run 'make clean' to make sure you get a
proper build. Failure to do so might result in strange build problems.


> make

ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$ make
Building OpenJDK for target 'default' in configuration 'linux-x86_64-normal-server-slowdebug'

## Starting langtools
Compiling 2 files for BUILD_TOOLS
Compiling 31 properties into resource bundles
Compiling 777 files for BUILD_BOOTSTRAP_LANGTOOLS
Creating langtools/dist/bootstrap/lib/javac.jar
Updating langtools/dist/lib/src.zip
Compiling 780 files for BUILD_FULL_JAVAC
Creating langtools/dist/lib/classes.jar
## Finished langtools (build time 00:01:10)

## Starting hotspot
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
Warning: The jvmg target has been replaced with debug
Warning: Please update your usage
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
*** This OS is not supported: Linux LAPTOP-FLAE2TIK 5.4.72-microsoft-standard-WSL2 #1 SMP Wed Oct 28 23:40:43 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
make[5]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:234: check_os_version] Error 1
make[4]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:255: linux_amd64_compiler2/fastdebug] Error 2
make[3]: *** [Makefile:217: generic_build2] Error 2
make[2]: *** [Makefile:167: debug] Error 2
make[1]: *** [HotspotWrapper.gmk:45: /mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug/hotspot/_hotspot.timestamp] Error 2
make: *** [/mnt/d/repo/openjdk//make/Main.gmk:109: hotspot-only] Error 2
ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$


> vi hotspot/make/linux/Makefile

SUPPORTED_OS_VERSION = 2.4% 2.5% 2.6% 3% 5%

> make

ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$ make
Building OpenJDK for target 'default' in configuration 'linux-x86_64-normal-server-slowdebug'

## Starting langtools
## Finished langtools (build time 00:00:04)

## Starting hotspot
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
Warning: The jvmg target has been replaced with debug
Warning: Please update your usage
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating directory list ../shared_dirs.lst
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
/usr/bin/make: invalid option -- '/'
/usr/bin/make: invalid option -- 'a'
/usr/bin/make: invalid option -- '/'
/usr/bin/make: invalid option -- 'c'
Usage: make [options] [target] ...
Options:
  -b, -m                      Ignored for compatibility.
  -B, --always-make           Unconditionally make all targets.
  -C DIRECTORY, --directory=DIRECTORY
                              Change to DIRECTORY before doing anything.
  -d                          Print lots of debugging information.
  --debug[=FLAGS]             Print various types of debugging information.
  -e, --environment-overrides
                              Environment variables override makefiles.
  --eval=STRING               Evaluate STRING as a makefile statement.
  -f FILE, --file=FILE, --makefile=FILE
                              Read FILE as a makefile.
  -h, --help                  Print this message and exit.
  -i, --ignore-errors         Ignore errors from recipes.
  -I DIRECTORY, --include-dir=DIRECTORY
                              Search DIRECTORY for included makefiles.
  -j [N], --jobs[=N]          Allow N jobs at once; infinite jobs with no arg.
  -k, --keep-going            Keep going when some targets can't be made.
  -l [N], --load-average[=N], --max-load[=N]
                              Don't start multiple jobs unless load is below N.
  -L, --check-symlink-times   Use the latest mtime between symlinks and target.
  -n, --just-print, --dry-run, --recon
                              Don't actually run any recipe; just print them.
  -o FILE, --old-file=FILE, --assume-old=FILE
                              Consider FILE to be very old and don't remake it.
  -O[TYPE], --output-sync[=TYPE]
                              Synchronize output of parallel jobs by TYPE.
  -p, --print-data-base       Print make's internal database.
  -q, --question              Run no recipe; exit status says if up to date.
  -r, --no-builtin-rules      Disable the built-in implicit rules.
  -R, --no-builtin-variables  Disable the built-in variable settings.
  -s, --silent, --quiet       Don't echo recipes.
  -S, --no-keep-going, --stop
                              Turns off -k.
  -t, --touch                 Touch targets instead of remaking them.
  --trace                     Print tracing information.
  -v, --version               Print the version number of make and exit.
  -w, --print-directory       Print the current directory.
  --no-print-directory        Turn off -w, even if it was turned on implicitly.
  -W FILE, --what-if=FILE, --new-file=FILE, --assume-new=FILE
                              Consider FILE to be infinitely new.
  --warn-undefined-variables  Warn when an undefined variable is referenced.

This program built for x86_64-pc-linux-gnu
Report bugs to <bug-make@gnu.org>
make[5]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/top.make:91: ad_stuff] Error 2
make[4]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:289: debug] Error 2
make[3]: *** [Makefile:217: generic_build2] Error 2
make[2]: *** [Makefile:167: debug] Error 2
make[1]: *** [HotspotWrapper.gmk:45: /mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug/hotspot/_hotspot.timestamp] Error 2
make: *** [/mnt/d/repo/openjdk//make/Main.gmk:109: hotspot-only] Error 2
ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$


> vi hotspot/make/linux/makefiles/adjust-mflags.sh

L67 添加一个大写I

参考：https://developer.jdcloud.com/article/1628


> make

ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$ make
Building OpenJDK for target 'default' in configuration 'linux-x86_64-normal-server-slowdebug'

## Starting langtools
## Finished langtools (build time 00:00:03)

## Starting hotspot
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
Warning: The jvmg target has been replaced with debug
Warning: Please update your usage
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/adlparse.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/archDesc.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/arena.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/dfa.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/dict2.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/filebuff.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/forms.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/formsopt.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/formssel.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/main.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/opto/opcodes.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/output_c.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/output_h.cpp
Making adlc
warning: [options] bootstrap class path not set in conjunction with -source 1.6
warning: [options] bootstrap class path not set in conjunction with -source 1.6
1 warning
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnv.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnter.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnterTrace.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/bytecodeInterpreterWithChecks.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmti.h
1 warning
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnvRecommended.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceEventClasses.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceEventIds.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceTypes.hpp
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Making /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/sa-jdi.jar
warning: [options] bootstrap class path not set in conjunction with -source 1.6
Note: Some input files use unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
1 warning
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Generating precompiled header precompiled.hpp.gch
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/sharedHeap.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/gc_implementation/parallelScavenge/psParallelCompact.hpp:34,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/gc_implementation/shared/markSweep.inline.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/oop.inline.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classFileParser.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoader.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/systemDictionary.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciEnv.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciUtilities.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciNullObject.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciConstant.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciArray.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:33:
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/generation.hpp:421:17: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  421 |         warning("time warp: "INT64_FORMAT" to "INT64_FORMAT, _time_of_last_gc, now);
      |                 ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/generation.hpp:421:42: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  421 |         warning("time warp: "INT64_FORMAT" to "INT64_FORMAT, _time_of_last_gc, now);
      |                                          ^
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/gc_interface/collectedHeap.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/oop.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classFileParser.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoader.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/systemDictionary.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciEnv.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciUtilities.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciNullObject.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciConstant.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciArray.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:33:
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/threadLocalAllocBuffer.inline.hpp:97:25: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   97 |     gclog_or_tty->print("TLAB: %s thread: "INTPTR_FORMAT" [id: %2d]"
      |                         ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/threadLocalAllocBuffer.inline.hpp:98:25: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   98 |                         " obj: "SIZE_FORMAT
      |                         ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/threadLocalAllocBuffer.inline.hpp:99:25: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   99 |                         " free: "SIZE_FORMAT
      |                         ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/threadLocalAllocBuffer.inline.hpp:100:25: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  100 |                         " waste: "SIZE_FORMAT"\n",
      |                         ^
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/space.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/space.inline.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/gc_implementation/shared/cSpaceCounters.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/defNewGeneration.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/services/memoryPool.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/services/lowMemoryDetector.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/gc_interface/collectedHeap.inline.hpp:36,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/oop.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classFileParser.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoader.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/systemDictionary.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciEnv.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciUtilities.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciNullObject.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciConstant.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciArray.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:33:
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:156:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  156 |            err_msg("Attempt to access p = "PTR_FORMAT" out of bounds of "
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:157:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  157 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:157:69: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  157 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                                                                     ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:427:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  427 |            err_msg("Returning result = "PTR_FORMAT" out of bounds of "
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:428:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  428 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:428:69: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  428 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                                                                     ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:436:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  436 |            err_msg("Attempt to access p = "PTR_FORMAT" out of bounds of "
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:437:20: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  437 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                    ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/memory/cardTableModRefBS.hpp:437:69: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
  437 |                    " card marking array's _whole_heap = ["PTR_FORMAT","PTR_FORMAT")",
      |                                                                     ^
In file included from ../generated/tracefiles/traceEventClasses.hpp:19,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/trace/tracing.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/opto/compile.hpp:44,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/opto/node.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/opto/addnode.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:252:
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:45:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   45 |     _st.print("%s = "UINT32_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:49:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   49 |     _st.print("%s = "UINT32_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:53:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   53 |     _st.print("%s = "INT32_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:57:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   57 |     _st.print("%s = "UINT32_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:61:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   61 |     _st.print("%s = "INT32_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:65:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   65 |     _st.print("%s = "UINT64_FORMAT, label, val);
      |               ^
/mnt/d/repo/openjdk/hotspot/src/share/vm/trace/traceStream.hpp:69:15: error: invalid suffix on literal; C++11 requires a space between literal and string macro [-Werror=literal-suffix]
   69 |     _st.print("%s = "INT64_FORMAT, label, val);
      |               ^
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/relocInfo.hpp:367:27: error: friend declaration of ‘relocInfo prefix_relocInfo(int)’ specifies default arguments and isn’t a definition [-fpermissive]
  367 |   inline friend relocInfo prefix_relocInfo(int datalen = 0);
      |                           ^~~~~~~~~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/relocInfo.hpp:462:18: error: friend declaration of ‘relocInfo prefix_relocInfo(int)’ specifies default arguments and isn’t the only declaration [-fpermissive]
  462 | inline relocInfo prefix_relocInfo(int datalen) {
      |                  ^~~~~~~~~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/relocInfo.hpp:367:27: note: previous declaration of ‘relocInfo prefix_relocInfo(int)’
  367 |   inline friend relocInfo prefix_relocInfo(int datalen = 0);
      |                           ^~~~~~~~~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/constantPool.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/method.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/frame.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeBlob.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeCache.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/cpu/x86/vm/assembler_x86.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.inline.hpp:31,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:30:
/mnt/d/repo/openjdk/hotspot/src/share/vm/oops/cpCache.hpp:193:42: error: left operand of shift expression ‘(-1 << 28)’ is negative [-fpermissive]
  193 |     option_bits_mask           = ~(((-1) << tos_state_shift) | (field_index_mask | parameter_size_mask))
      |                                    ~~~~~~^~~~~~~~~~~~~~~~~~~
/mnt/d/repo/openjdk/hotspot/src/share/vm/oops/cpCache.hpp:193:104: error: enumerator value for ‘option_bits_mask’ is not an integer constant
  193 |     option_bits_mask           = ~(((-1) << tos_state_shift) | (field_index_mask | parameter_size_mask))
      |                                                                                                        ^
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/histogram.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/mutex.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoaderData.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayKlass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayOop.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/constantPool.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/method.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/frame.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeBlob.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeCache.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/cpu/x86/vm/assembler_x86.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.inline.hpp:31,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:30:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp: In static member function ‘static dirent* os::readdir(DIR*, dirent*)’:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp:142:18: error: ‘int readdir_r(DIR*, dirent*, dirent**)’ is deprecated [-Werror=deprecated-declarations]
  142 |   if((status = ::readdir_r(dirp, dbuf, &p)) != 0) {
      |                  ^~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/os/linux/vm/jvm_linux.h:44,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/prims/jvm.h:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/debug.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/globals.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/allocation.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/iterator.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/genOopClosures.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/klass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/handles.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/universe.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/oopRecorder.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/usr/include/dirent.h:183:12: note: declared here
  183 | extern int readdir_r (DIR *__restrict __dirp,
      |            ^~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/histogram.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/mutex.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoaderData.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayKlass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayOop.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/constantPool.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/method.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/frame.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeBlob.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeCache.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/cpu/x86/vm/assembler_x86.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.inline.hpp:31,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:30:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp:142:42: error: ‘int readdir_r(DIR*, dirent*, dirent**)’ is deprecated [-Werror=deprecated-declarations]
  142 |   if((status = ::readdir_r(dirp, dbuf, &p)) != 0) {
      |                                          ^
In file included from /mnt/d/repo/openjdk/hotspot/src/os/linux/vm/jvm_linux.h:44,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/prims/jvm.h:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/debug.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/globals.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/allocation.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/iterator.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/genOopClosures.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/klass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/handles.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/universe.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/oopRecorder.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/usr/include/dirent.h:183:12: note: declared here
  183 | extern int readdir_r (DIR *__restrict __dirp,
      |            ^~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/histogram.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/mutex.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoaderData.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayKlass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayOop.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/constantPool.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/method.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/frame.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeBlob.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeCache.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/cpu/x86/vm/assembler_x86.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.inline.hpp:31,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:30:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp:142:42: error: ‘int readdir_r(DIR*, dirent*, dirent**)’ is deprecated [-Werror=deprecated-declarations]
  142 |   if((status = ::readdir_r(dirp, dbuf, &p)) != 0) {
      |                                          ^
In file included from /mnt/d/repo/openjdk/hotspot/src/os/linux/vm/jvm_linux.h:44,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/prims/jvm.h:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/debug.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/globals.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/allocation.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/iterator.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/genOopClosures.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/klass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/handles.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/memory/universe.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/oopRecorder.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/codeBuffer.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:29:
/usr/include/dirent.h:183:12: note: declared here
  183 | extern int readdir_r (DIR *__restrict __dirp,
      |            ^~~~~~~~~
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciEnv.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciUtilities.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciNullObject.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciConstant.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/ci/ciArray.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:33:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp: At global scope:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp:169:59: error: left operand of shift expression ‘(-1 << 1)’ is negative [-fpermissive]
  169 |     all_types           = ((1 << TYPE_LIMIT) - 1) & ((-1) << FIRST_TYPE),
      |                                                     ~~~~~~^~~~~~~~~~~~~~
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp:169:72: error: enumerator value for ‘all_types’ is not an integer constant
  169 |     all_types           = ((1 << TYPE_LIMIT) - 1) & ((-1) << FIRST_TYPE),
      |                                                                        ^
cc1plus: all warnings being treated as errors
make[6]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/vm.make:297: precompiled.hpp.gch] Error 1
make[5]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/top.make:119: the_vm] Error 2
make[4]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:289: debug] Error 2
make[3]: *** [Makefile:217: generic_build2] Error 2
make[2]: *** [Makefile:167: debug] Error 2
make[1]: *** [HotspotWrapper.gmk:45: /mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug/hotspot/_hotspot.timestamp] Error 2
make: *** [/mnt/d/repo/openjdk//make/Main.gmk:109: hotspot-only] Error 2
ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$

需要降级gcc、g++

> sudo vi /etc/apt/sources.list

deb http://mirrors.ustc.edu.cn/ubuntu/ xenial main
deb http://mirrors.ustc.edu.cn/ubuntu/ xenial universe


sudo apt-get update
sudo apt install gcc-4.9 g++-4.9

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 50
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 50
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 20
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.9 20

sudo update-alternatives --config gcc
sudo update-alternatives --config g++

> make clean
> make

依旧是

/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp: At global scope:
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp:169:59: error: left operand of shift expression ‘(-1 << 1)’ is negative [-fpermissive]
  169 |     all_types           = ((1 << TYPE_LIMIT) - 1) & ((-1) << FIRST_TYPE),
      |                                                     ~~~~~~^~~~~~~~~~~~~~
/mnt/d/repo/openjdk/hotspot/src/share/vm/code/dependencies.hpp:169:72: error: enumerator value for ‘all_types’ is not an integer constant
  169 |     all_types           = ((1 << TYPE_LIMIT) - 1) & ((-1) << FIRST_TYPE),
      |                                                                        ^
cc1plus: all warnings being treated as errors
make[6]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/vm.make:297: precompiled.hpp.gch] Error 1
make[5]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/top.make:119: the_vm] Error 2
make[4]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:289: debug] Error 2
make[3]: *** [Makefile:217: generic_build2] Error 2
make[2]: *** [Makefile:167: debug] Error 2
make[1]: *** [HotspotWrapper.gmk:45: /mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug/hotspot/_hotspot.timestamp] Error 2
make: *** [/mnt/d/repo/openjdk//make/Main.gmk:109: hotspot-only] Error 2

想起来configure阶段是认了gcc版本的，重新configure

>  bash ./configure --with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri

====================================================
A new configuration has been successfully created in
/mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug
using configure arguments '--with-freetype-include=/usr/include/freetype2 --with-freetype-lib=/usr/lib/x86_64-linux-gnu --with-target-bits=64 --with-jvm-variants=server --with-debug-level=slowdebug --disable-zip-debug-info --with-boot-jdk=/home/ubuntu/java-se-7u75-ri'.

Configuration summary:
* Debug level:    slowdebug
* JDK variant:    normal
* JVM variants:   server
* OpenJDK target: OS: linux, CPU architecture: x86, address length: 64

Tools summary:
* Boot JDK:       openjdk version "1.7.0_75" OpenJDK Runtime Environment (build 1.7.0_75-b13) OpenJDK 64-Bit Server VM (build 24.75-b04, mixed mode)  (at /home/ubuntu/java-se-7u75-ri)
* C Compiler:     gcc-4.9 (Ubuntu 4.9.3-13ubuntu2) version 4.9.3 (at /usr/bin/gcc-4.9)
* C++ Compiler:   g++-4.9 (Ubuntu 4.9.3-13ubuntu2) version 4.9.3 (at /usr/bin/g++-4.9)

Build performance summary:
* Cores to use:   11
* Memory limit:   12269 MB
* ccache status:  not installed (consider installing)

WARNING: The result of this configuration has overridden an older
configuration. You *should* run 'make clean' to make sure you get a
proper build. Failure to do so might result in strange build problems.

> make clean
> make

ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$ make
Building OpenJDK for target 'default' in configuration 'linux-x86_64-normal-server-slowdebug'

## Starting langtools
Compiling 2 files for BUILD_TOOLS
Compiling 31 properties into resource bundles
Compiling 777 files for BUILD_BOOTSTRAP_LANGTOOLS
Creating langtools/dist/bootstrap/lib/javac.jar
Updating langtools/dist/lib/src.zip
Compiling 780 files for BUILD_FULL_JAVAC
Creating langtools/dist/lib/classes.jar
## Finished langtools (build time 00:01:04)

## Starting hotspot
make[2]: warning: -j1 forced in submake: resetting jobserver mode.
Warning: The jvmg target has been replaced with debug
Warning: Please update your usage
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating directory list ../shared_dirs.lst
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Creating Makefile ...
Creating flags.make ...
Creating flags_vm.make ...
Creating vm.make ...
Creating adlc.make ...
Creating jvmti.make ...
Creating trace.make ...
Creating sa.make ...
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/adlparse.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/archDesc.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/arena.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/dfa.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/dict2.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/filebuff.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/forms.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/formsopt.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/formssel.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/main.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/opto/opcodes.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/output_c.cpp
Compiling /mnt/d/repo/openjdk/hotspot/src/share/vm/adlc/output_h.cpp
Making adlc
warning: [options] bootstrap class path not set in conjunction with -source 1.6
warning: [options] bootstrap class path not set in conjunction with -source 1.6
1 warning
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnv.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnter.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnterTrace.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/bytecodeInterpreterWithChecks.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmti.h
1 warning
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/jvmtifiles/jvmtiEnvRecommended.cpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceEventClasses.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceEventIds.hpp
Generating /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/tracefiles/traceTypes.hpp
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Making /home/ubuntu/repo/jdk-build/linux-x86_64-normal-server-slowdebug/hotspot/linux_amd64_compiler2/debug/../generated/sa-jdi.jar
warning: [options] bootstrap class path not set in conjunction with -source 1.6
Note: Some input files use unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
1 warning
INFO: ENABLE_FULL_DEBUG_SYMBOLS=1
INFO: ALT_OBJCOPY=/usr/bin/objcopy
INFO: /usr/bin/objcopy cmd found so will create .debuginfo files.
INFO: STRIP_POLICY=min_strip
INFO: ZIP_DEBUGINFO_FILES=0
Generating precompiled header precompiled.hpp.gch
In file included from /mnt/d/repo/openjdk/hotspot/src/share/vm/utilities/histogram.hpp:32:0,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/mutex.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/classfile/classLoaderData.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayKlass.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/typeArrayOop.hpp:29,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/constantPool.hpp:32,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/oops/method.hpp:33,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/runtime/frame.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeBlob.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/code/codeCache.hpp:28,
                 from /mnt/d/repo/openjdk/hotspot/src/cpu/x86/vm/assembler_x86.inline.hpp:30,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/asm/assembler.inline.hpp:31,
                 from /mnt/d/repo/openjdk/hotspot/src/share/vm/precompiled/precompiled.hpp:30:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp: In static member function ‘static dirent* os::readdir(DIR*, dirent*)’:
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp:142:18: error: ‘int readdir_r(DIR*, dirent*, dirent**)’ is deprecated (declared at /usr/include/dirent.h:183) [-Werror=deprecated-declarations]
   if((status = ::readdir_r(dirp, dbuf, &p)) != 0) {
                  ^
/mnt/d/repo/openjdk/hotspot/src/os/linux/vm/os_linux.inline.hpp:142:42: error: ‘int readdir_r(DIR*, dirent*, dirent**)’ is deprecated (declared at /usr/include/dirent.h:183) [-Werror=deprecated-declarations]
   if((status = ::readdir_r(dirp, dbuf, &p)) != 0) {
                                          ^
cc1plus: all warnings being treated as errors
make[6]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/vm.make:297: precompiled.hpp.gch] Error 1
make[5]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/makefiles/top.make:119: the_vm] Error 2
make[4]: *** [/mnt/d/repo/openjdk/hotspot/make/linux/Makefile:289: debug] Error 2
make[3]: *** [Makefile:217: generic_build2] Error 2
make[2]: *** [Makefile:167: debug] Error 2
make[1]: *** [HotspotWrapper.gmk:45: /mnt/d/repo/openjdk/build/linux-x86_64-normal-server-slowdebug/hotspot/_hotspot.timestamp] Error 2
make: *** [/mnt/d/repo/openjdk//make/Main.gmk:109: hotspot-only] Error 2
ubuntu@LAPTOP-FLAE2TIK:/mnt/d/repo/openjdk$


> vi hotspot/make/linux/makefiles/gcc.make

L207 #WARNINGS_ARE_ERRORS = -Werror

注释掉

> make

