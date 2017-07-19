# Qualcomm Alljoyn note #
[TOC]

## Allseen
Developer:
https://allseenalliance.org/developers/download
Allseen郵件群組
https://lists.allseenalliance.org/mailman/listinfo
AllJoyn平台應用開發論壇
https://ask.allseenalliance.org/questions/
AllJoyn平台線上學習計畫
https://wiki.allseenalliance.org/training
Alljoyn WIKI
https://wiki.allseenalliance.org/

共同開發AllJoyn平台未來發展方向及可能性：
https://wiki.allseenalliance.org/?idx=tsc%3Atechnical_steering_committee

============================================================
## AllJoyn         
Ref: http://baike.baidu.com/view/11659412.htm
AllJoyn是一個合作的開源軟體框架，程式員可以很方便的編寫出搜索附近設備的應用應用程
式，並且無論對方的品牌、類別、系統都可以在不需要雲環境的情況下連接。
AllJoyn框架是非常靈活，能使物聯網實現願景。
### 目錄
- 概述
- 近端網
- 靈活
- 可選雲
- 勢頭
- 接下來的步驟

#### 概述
AllJoyn，由高通公司主導的高創新中心（Qualcomm Innovation Center）的開源項目開發的
，主要用於近距離無線傳輸，通過WiFi或藍牙技術，定位和點對點文件傳輸。該項目在2012
公開。

#### 近端網
在AllJoyn框架處理發現附近的設備，設備之間建立會話，這些設備之間的安全通信的複雜性
。它抽像出物理傳輸的細節，並提供了一個簡單易用的API。
多個連接會話拓撲的支援，包括點至點和小組會議。安全框架是靈活的，支援多種機制和信
任模型。
和傳輸的數據的類型也很靈活，支援原始套接字或抽像的對象具有良好定義的介面，方法，
屬性和信號。[1] 

#### 靈活
其中AllJoyn架構的定義特徵之一是其固有的靈活性。
它被設計為在多個平台上運行，從小型的嵌入式RTOS平台，全功能的作業系統。它支援多語
言綁定和運輸。
而且，由於AllJoyn框架是開源的，這種靈活性可以在未來進一步擴展，以支援更多的傳輸，
綁定和特點。
運輸：無線網路，以太網，串口，電源線（PLC）
綁定：C，C++，OBJ-C，Java的
平台：RTOS，Arduino的，Linux和Android的，iOS的，在Windows，Mac
安全性：對等網路加密（AES128）和認證（PSK，ECDSA）
對於物聯網通用語言
為了充分實現物聯網的願景，設備和應用程式需要一種通用的方式進行交互和對方說話。
我們認為，通用語言是AllJoyn框架：它用作膠水，以允許來自不同公司的設備，在不同的作
業系統，寫與不同語言綁定到所有運行說話在一起，只是工作。
該AllSeen聯盟，與開源社區，正在制定和實施，解決一個具體的用例常見的服務和介面，如
入職的新設備，第一次，發送通知和控制裝置的工作。
然後，開發人員可以利用這些服務，它們集成到他們的產品，並知道他們是與其他設備和應
用程式的生態系統AllJoyn相容。
除了常見的服務和介面，一個應用程式或設備也可以實現專用介面。因此，應用程式可以都
使用共同的服務和介面，以參加更大AllJoyn的生態系統，而在同一時間，使用AllJoyn框架
與應用程式和設備在專用的方式進行通信。
在AllJoyn框架使這種靈活性。

#### 可選雲
所述AllJoyn框架運行在本地網路上，並且不需要在雲起作用。應用程式和設備互相交談，直
接 - 快速，高效和安全。沒有必要走出去，等待雲時，該設備是你旁邊。
並在需要的雲計算的情況下，AllJoyn架構支援以及通過網關代理。這種結構的一個主要優點
是安全性：只有網關代理直接連接到互聯網，減少連接到因特網的設備的數量，並因此降低
了攻擊面。

#### 勢頭
作為協作的開源項目，該AllSeen生態系統持續增長和發展。更常見的服務被添加在每個版本
中，包括實現多個平台。有強勁的發展勢頭，並與您的幫助下，AllJoyn架構可以很好地成為
通用的語言文字的物聯網。

#### 接下來的步驟
瞭解更多關於用例。然後從頭瞭解整體架構，核心框架和基本服務。


============================================================
## 在UBUNTU 編譯alljoyn-suite-14.06.00a-src
ref: https://allseenalliance.org/developers/develop/building/linux
pwd: /home/Allplay/Project_JS/allplaySoftware/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn

### BUILDING LINUX
#### Setup
NOTE: The installation commands below refer specifically to Debian/Ubuntu Linux. Equivalent commands are available for other distributions of Linux.
1. Build tools and libs
```
   sudo apt-get install build-essential libgtk2.0-dev libssl-dev xsltproc ia32-libs libxml2-dev
```   
2. Install Python v2.6/2.7 (Python v3.0 is not compatible and will cause errors)
```
   sudo apt-get install python
```   
3. Install SCons v2.0
```
   sudo apt-get install scons
```   
4. OpenSSL
```
   sudo apt-get install libssl-dev
```   
5. Download the AllJoyn Source zip and extract source.

#### Building Samples
1. Switch to 
```
   cd /home/Allplay/Project_JS/allplaySoftware/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn
```   
2. build
```
   scons BINDINGS=cpp WS=off BT=off ICE=off SERVICES="about,notification,controlpanel,config,onboarding,sample_apps"
```   

#### Building the AllJoyn
##### framework for an existing app
1. Setup
```
  export AJ_ROOT=/home/Allplay/Project_JS/allplaySoftware/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn
```  
2. 
```
  # <TARGET CPU> can be either x86_64, x86, or whatever value you set for CPU= when running SCons.
  export AJ_DIST="$AJ_ROOT/core/alljoyn/build/linux/x86/debug/dist"
```  
3. Add header include directories
```
export CXXFLAGS="$CXXFLAGS \
    -I$AJ_DIST/cpp/inc \
    -I$AJ_DIST/about/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/notification/inc \
    -I$AJ_DIST/controlpanel/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/samples_common/inc"
```    
4. Configure linker to include required libs
```
export LDFLAGS="$LDFLAGS \
    -L$AJ_DIST/cpp/lib \
    -L$AJ_DIST/about/lib \
    -L$AJ_DIST/services_common/lib \
    -L$AJ_DIST/notification/lib \
    -L$AJ_DIST/controlpanel/lib"
```

============================================================
## 在UBUNTU 編譯alljoyn-suite-14.12.00-src ##
ref: https://allseenalliance.org/developers/develop/building/linux
pwd:
```
/home/Allplay/Project_JS/allplaySoftware/v14.12/alljoyn-14.12.00-scr
```
### BUILDING LINUX
Setup
NOTE: The installation commands below refer specifically to Debian/Ubuntu Linux. Equivalent commands are available for other distributions of Linux.
1. Build tools and libs
```
   sudo apt-get install build-essential libgtk2.0-dev libssl-dev xsltproc ia32-libs libxml2-dev
```
2. Install Python v2.6/2.7 (Python v3.0 is not compatible and will cause errors)
```
   sudo apt-get install python
```
3. Install SCons v2.0
```
   sudo apt-get install scons
```   
4. OpenSSL
```
   sudo apt-get install libssl-dev
```   
5. Download the AllJoyn Source zip and extract source.

### Building Samples
1. Switch to 
```
   cd /home/Allplay/Project_JS/allplaySoftware/v14.12/alljoyn-14.12.00-scrc
```   
2. build
```
   scons BINDINGS=cpp WS=off BT=off ICE=off SERVICES="about,notification,controlpanel,config,onboarding,sample_apps"
```
### Building the AllJoyn? 
1. Setup
```
  export AJ_ROOT=/home/Allplay/Project_JS/allplaySoftware/v14.12/alljoyn-14.12.00-scr
```  
2. <TARGET CPU> can be either x86_64, x86, or whatever value you set for CPU= when running SCons.
```
  export AJ_DIST="$AJ_ROOT/core/alljoyn/build/linux/x86/debug/dist"
```  
3. Add header include directories
```
export CXXFLAGS="$CXXFLAGS \
    -I$AJ_DIST/cpp/inc \
    -I$AJ_DIST/about/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/notification/inc \
    -I$AJ_DIST/controlpanel/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/samples_common/inc"
```    
4. Configure linker to include required libs
```
export LDFLAGS="$LDFLAGS \
    -L$AJ_DIST/cpp/lib \
    -L$AJ_DIST/about/lib \
    -L$AJ_DIST/services_common/lib \
    -L$AJ_DIST/notification/lib \
    -L$AJ_DIST/controlpanel/lib"
```

============================================================
## Library liballjoyn.so not found
Library liballjoyn.so not found
If the following error is returned:
```
error while loading shared libraries: liballjoyn.so:
cannot open shared object file: No such file or directory
```
As of AllJoyn 3.4.0 the SCons scripts have been modified for the Linux build system to build a shared library and link against that shared library. Add the library to the link path.
```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:<workspace>/build/{OS}/{CPU}/{VARIANT}/dist/cpp/lib
```
After adding the library LD_LIBRARY_PATH re-run the program that produced the error.
```
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/Allplay/Project_JS/allplaySoftware/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/build/linux/x86/debug/dist/cpp/lib
```

============================================================
## LINUX - RUNNING NOTIFICATION SAMPLE APPS
Running ConsumerService and ProducerBasic Sample Apps
Prerequisites
Open two terminal windows. In each, navigate to the AllJoyn? root dir, then:
```
export AJ_ROOT=`pwd`

# <TARGET CPU> can be either x86_64, x86, or whatever value you set for "CPU=" when running SCons.
export TARGET_CPU=x86
export LD_LIBRARY_PATH=$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/cpp/lib:$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/about/lib:$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/notification/lib:$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/services_common/lib:$LD_LIBRARY_PATH
```
Run the ConsumerService Sample App
In one of the terminal windows, run ConsumerService:
```
$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/notification/bin/ConsumerService
```
Run the ProducerBasic Sample App
In the other terminal window, run ProducerBasic:
```
$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/notification/bin/ProducerBasic
```

============================================================
## Build source code 
```
root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn# tree -L 1
.
├── alljoyn_c
├── alljoyn_core
├── alljoyn_java
├── alljoyn_js
├── alljoyn_objc
├── alljoyn_unity
├── build
├── build_core
├── build.xml
├── common
├── README.md
├── README.txt
├── SConstruct
└── services
10 directories, 4 files

root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core
/alljoyn# scons OS=linux CPU=x86 BINDINGS=c,cpp
scons: Reading SConscript files ...
Building bindings: cpp, c
Building services: about
BULLSEYE_BIN not specified
GTEST_DIR not specified skipping common unit test build
BULLSEYE_BIN not specified
GTEST_DIR not specified skipping alljoyn_core unit test build
GTEST_DIR not specified skipping alljoyn_c unit test build
GTEST_DIR not specified skipping About Service unit test build
scons: done reading SConscript files.
scons: Building targets ...
Install file: "build/linux/x86/debug/dist/cpp/inc/alljoyn/DBusStdDefines.h" as "alljoyn_c/inc/alljoyn_c/DBusStdDefines.h"
Install file: "build/linux/x86/debug/dist/cpp/inc/alljoyn/Status.h" as "alljoyn_c/inc/alljoyn_c/Status.h"
Install file: "build/linux/x86/debug/dist/cpp/inc/qcc/platform.h" as "alljoyn_c/inc/qcc/platform.h"
Install file: "build/linux/x86/debug/dist/cpp/inc/qcc/posix/platform_types.h" as "alljoyn_c/inc/qcc/posix/platform_types.h"
Install file: "alljoyn_c/inc/alljoyn_c/AuthListener.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/AuthListener.h"
Install file: "alljoyn_c/inc/alljoyn_c/AjAPI.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/AjAPI.h"
Install file: "alljoyn_c/inc/alljoyn_c/Message.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/Message.h"
Install file: "alljoyn_c/inc/alljoyn_c/MsgArg.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/MsgArg.h"
Install file: "alljoyn_c/inc/alljoyn_c/Session.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/Session.h"
Install file: "alljoyn_c/inc/alljoyn_c/Status.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/Status.h"
Install file: "alljoyn_c/inc/alljoyn_c/TransportMask.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/TransportMask.h"
        [CXX]     alljoyn_c/src/AuthListener.cc
        [CXX-SH]  alljoyn_c/src/AuthListener.cc
Install file: "alljoyn_c/inc/alljoyn_c/BusAttachment.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/BusAttachment.h"
Install file: "alljoyn_c/inc/alljoyn_c/BusListener.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/BusListener.h"
Install file: "alljoyn_c/inc/alljoyn_c/BusObject.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/BusObject.h"
Install file: "alljoyn_c/inc/alljoyn_c/InterfaceDescription.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/InterfaceDescription.h"
Install file: "alljoyn_c/inc/alljoyn_c/KeyStoreListener.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/KeyStoreListener.h"
Install file: "alljoyn_c/inc/alljoyn_c/ProxyBusObject.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/ProxyBusObject.h"
Install file: "alljoyn_c/inc/alljoyn_c/SessionListener.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/SessionListener.h"
Install file: "alljoyn_c/inc/alljoyn_c/SessionPortListener.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/SessionPortListener.h"
Install file: "alljoyn_c/inc/alljoyn_c/MessageReceiver.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/MessageReceiver.h"
        [CXX]     alljoyn_c/src/BusAttachment.cc
        [CXX-SH]  alljoyn_c/src/BusAttachment.cc
        [CXX]     alljoyn_c/src/BusAttachmentC.cc
        [CXX-SH]  alljoyn_c/src/BusAttachmentC.cc
        [CXX]     alljoyn_c/src/BusListener.cc
        [CXX-SH]  alljoyn_c/src/BusListener.cc
        [CXX]     alljoyn_c/src/BusObjectC.cc
        [CXX-SH]  alljoyn_c/src/BusObjectC.cc
        [CXX]     alljoyn_c/src/DeferredCallback.cc
        [CXX-SH]  alljoyn_c/src/DeferredCallback.cc
        [CXX]     alljoyn_c/src/InterfaceDescription.cc
        [CXX-SH]  alljoyn_c/src/InterfaceDescription.cc
        [CXX]     alljoyn_c/src/KeyStoreListener.cc
        [CXX-SH]  alljoyn_c/src/KeyStoreListener.cc
        [CXX]     alljoyn_c/src/Message.cc
        [CXX-SH]  alljoyn_c/src/Message.cc
        [CXX]     alljoyn_c/src/MsgArg.cc
        [CXX-SH]  alljoyn_c/src/MsgArg.cc
        [CXX]     alljoyn_c/src/MsgArgC.cc
        [CXX-SH]  alljoyn_c/src/MsgArgC.cc
Install file: "alljoyn_c/inc/alljoyn_c/PasswordManager.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/PasswordManager.h"
        [CXX]     alljoyn_c/src/PasswordManager.cc
        [CXX-SH]  alljoyn_c/src/PasswordManager.cc
        [CXX]     alljoyn_c/src/ProxyBusObject.cc
        [CXX-SH]  alljoyn_c/src/ProxyBusObject.cc
        [CXX]     alljoyn_c/src/SessionListener.cc
        [CXX-SH]  alljoyn_c/src/SessionListener.cc
        [CXX]     alljoyn_c/src/SessionOpts.cc
        [CXX-SH]  alljoyn_c/src/SessionOpts.cc
        [CXX]     alljoyn_c/src/SessionPortListener.cc
        [CXX-SH]  alljoyn_c/src/SessionPortListener.cc
Install file: "alljoyn_c/inc/alljoyn_c/version.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/version.h"
        [CXX]     alljoyn_c/src/version.cc
        [AR]      alljoyn_c/build/linux/x86/debug/obj/liballjoyn_c.a
        [RANLIB]  alljoyn_c/build/linux/x86/debug/obj/liballjoyn_c.a
        [CXX-SH]  alljoyn_c/src/version.cc
        [LINK-SH] alljoyn_c/build/linux/x86/debug/obj/liballjoyn_c.so
Install file: "alljoyn_c/inc/alljoyn_c/DBusStdDefines.h" as "build/linux/x86/debug/dist/c/inc/alljoyn_c/DBusStdDefines.h"
        [CC]      alljoyn_c/samples/basic/basic_c_client.c
Install file: "alljoyn_c/build/linux/x86/debug/obj/liballjoyn_c.a" as "build/linux/x86/debug/dist/c/lib/liballjoyn_c.a"
        [LINK]    alljoyn_c/build/linux/x86/debug/obj/samples/basic/basic_c_client
        [CC]      alljoyn_c/samples/basic/basic_c_service.c
        [LINK]    alljoyn_c/build/linux/x86/debug/obj/samples/basic/basic_c_service
        [CC]      alljoyn_c/samples/secure/DeskTopSharedKSClientC.c
        [LINK]    alljoyn_c/build/linux/x86/debug/obj/samples/secure/DeskTopSharedKSClientC
        [CC]      alljoyn_c/test/bbcclient.c
        [LINK]    alljoyn_c/build/linux/x86/debug/obj/test/bbcclient
        [CC]      alljoyn_c/test/bbcservice.c
        [LINK]    alljoyn_c/build/linux/x86/debug/obj/test/bbcservice
Install file: "alljoyn_c/build/linux/x86/debug/obj/test/bbcclient" as "build/linux/x86/debug/dist/c/bin/bbcclient"
Install file: "alljoyn_c/build/linux/x86/debug/obj/test/bbcservice" as "build/linux/x86/debug/dist/c/bin/bbcservice"
Install file: "alljoyn_c/build/linux/x86/debug/obj/samples/basic/basic_c_client" as "build/linux/x86/debug/dist/c/bin/samples/basic_c_client"
Install file: "alljoyn_c/build/linux/x86/debug/obj/samples/basic/basic_c_service" as "build/linux/x86/debug/dist/c/bin/samples/basic_c_service"
Install file: "alljoyn_c/inc/qcc/platform.h" as "build/linux/x86/debug/dist/c/inc/qcc/platform.h"
Install file: "alljoyn_c/inc/qcc/posix/platform_types.h" as "build/linux/x86/debug/dist/c/inc/qcc/posix/platform_types.h"
Install file: "alljoyn_c/build/linux/x86/debug/obj/liballjoyn_c.so" as "build/linux/x86/debug/dist/c/lib/liballjoyn_c.so"
Install file: "alljoyn_c/samples/basic/basic_c_client.c" as "build/linux/x86/debug/dist/c/samples/basic/basic_c_client.c"
Install file: "alljoyn_c/samples/basic/basic_c_service.c" as "build/linux/x86/debug/dist/c/samples/basic/basic_c_service.c"
wsbuild(["ws"], ["build_core/$DISTDIR"])
Evaluating whitespace compliance...
Config: /home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/build_core/tools/conf/ajuncrustify.cfg
Note: enter 'scons -h' to see whitespace (WS) options
whitespace.db not found a new one will be created.
It appears that 'uncrustify' is not installed or is not on your PATH. Please check your system and try again.
scons: *** [ws] Explicit exit, status 2
scons: building terminated because of errors.
root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn# $HOME
-bash: /root: Is a directory
root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn#
```

============================================================
## ALLJOYN export setting
```
root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn# export
declare -x AJ_DIST="/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist"
declare -x AJ_ROOT="/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn"
declare -x CXXFLAGS="     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/cpp/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/about/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/services_common/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/notification/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/controlpanel/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/services_common/inc     -I/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/samples_common/inc"
declare -x DISPLAY="localhost:11.0"
declare -x HOME="/root"
declare -x LANG="en_US.UTF-8"
declare -x LDFLAGS="     -L/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/cpp/lib     -L/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/about/lib     -L/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/services_common/lib     -L/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/notification/lib     -L/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn/core/alljoyn/build/linux/X86/debug/dist/controlpanel/lib"
declare -x LESSCLOSE="/usr/bin/lesspipe %s %s"
declare -x LESSOPEN="| /usr/bin/lesspipe %s"
declare -x LOGNAME="root"
declare -x LS_COLORS="rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lz=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.axa=00;36:*.oga=00;36:*.spx=00;36:*.xspf=00;36:"
declare -x MAIL="/var/mail/root"
declare -x OLDPWD="/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core"
declare -x PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games"
declare -x PWD="/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn"
declare -x SHELL="/bin/bash"
declare -x SHLVL="1"
declare -x SPEECHD_PORT="6560"
declare -x SSH_CLIENT="192.168.100.28 4554 22"
declare -x SSH_CONNECTION="192.168.100.28 4554 192.168.100.102 22"
declare -x SSH_TTY="/dev/pts/1"
declare -x TERM="xterm"
declare -x USER="root"
declare -x XDG_SESSION_COOKIE="67585c863e6a1ad8fc0932a84e59a3ec-1419642774.942283-524828344"
root@js-desktop:/home/Allplay/Project_JS/allplay Software/v14.06/alljoyn-suite-14.06.00a-src/core/alljoyn#
```

============================================================
## 【Android平台】Alljoyn學習筆記一 Alljoyn簡介
【什麼是Alljoyn】
AllJoyn官網中將其描述為"一個能夠使連接設備之間進行互操作的通用軟體框架和系統服務
核心集，也是一個跨製造商來創建動態近端網路的軟體應用"。
Linux基金會表示，該開源框架允許在特定的系統之間無縫發現、動態連接，並可以與附近的
產品進行交互，無論該產品是什麼品牌、傳輸層、平台或作業系統。
該框架不依賴於特定的通信協定，因此它可以工作在WiFi、藍牙、以太網或任何IP傳輸的環
境中。
在不久的將來，當你家裡冰箱中的牛奶剩餘不多的時候，冰箱可能會給你的手機發送消息提
醒你購買。
高通互動平台總裁Rob Chandhok表示，高通花費了大量的時間和數百萬美元去解決設備之間
的互操作問題，現在高通已經將項目捐贈給了AllSeen聯盟，高通和Linux基金會希望不同公
司和它的開發人員能夠參與進來，共同促進這一項目的發展。

AllJoyn的開發工具和教程
目前已經有一些應用通過AllJoyn構建，比如一個名片讀取器，可以讓你通過WiFi分享聯繫人
數據。遊戲平台聯合對戰可以通過Alljoyn實現
AllJoyn項目還針對Android、Arduino、iOS、OS X、Linux、Windows等平台以及Unity遊戲開
發引擎提供了SDK和API，並且還有一個教程，
以幫助開發人員在產品中集成AllJoyn的功能。

項目官網：https://www.alljoyn.org/
AllSeen Alliance官網：https://allseenalliance.org/about
文檔和SDK：https://www.alljoyn.org/docs-and-downloads
項目源碼：https://git.allseenalliance.org/gerrit/#/admin/projects/
Android 開發環境配置：http://wenku.baidu.com/link?url=de3b710tavJwy8aNocR7QYM35k4OQnAM7osJy0H1OY6THLhdK_1rH3sOZlEKVWfeWsyfeArrjqtp8LZarRaGmF2-KwNu1qPcD3UxNUyq8zC


============================================================
##Ubuntu下編譯AllJoyn源碼及遇到的問題          
ref: http://blog.csdn.net/huangjuegeek/article/details/38443515
環境：
作業系統 ubuntu-14.04-desktop-i386
到https://allseenalliance.org網站上下載源碼包 alljoyn-suite-14.06.00_beta-src.tar.gz
copy到/opt下，解壓，更名為/opt/alljoyn-14.06
下載好junit-4.9.jar
```
$ sudo cp junit-4.9.jar /usr/share/java/
```  
環境變數 
```
JAVA_HOME=/usr/java/jdk1.7.0_25
CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:/usr/share/java/junit-4.9.jar
PATH=$JAVA_HOME/bin:$PATH
AJ_ROOT=/opt/alljoyn-14.06
```
重要參考資料：Configuring the Build Environment (Linux Platform)
下面開始記錄過程
```
$ cd $AJ_ROOT/core/alljoyn  
```
查看該目錄結構，初始的內容如下
```
$ tree -L 1  
.  
├── alljoyn_c  
├── alljoyn_core  
├── alljoyn_java  
├── alljoyn_js  
├── alljoyn_objc  
├── alljoyn_unity  
├── build_core  
├── build.xml  
├── common  
├── README.md  
├── README.txt  
├── SConstruct  
└── services  
```
由於我不需要JavaScript, Objective-C, Unity的BINDINGS，我可以直接把這3個相關的目錄刪掉，也可以在編譯時指定參數，如
```
$ scons OS=linux CPU=x86 BINDINGS=c,cpp,java  
```
命令開始執行後，一開始編譯cpp時，進展還比較順利。可當編譯到Java時，輸出內容包括以下幾類資訊
（1）
```
warning: [path] bad path element "/usr/share/java/junit4.9.jar": no such file or directory  
alljoyn_java/test/org/alljoyn/bus/AddressBookTest.java:23: error: package junit.framework does not exist  
```
（2）
```
alljoyn_java/test/org/alljoyn/bus/MarshalTest.java:1153: warning: [rawtypes] found raw type: TreeMap  
        TreeMap<String, String>[] aaess = (TreeMap<String, String>[]) new TreeMap[2];  
                                                                          ^  
  missing type arguments for generic class TreeMap<K,V>  
  where K,V are type-variables:  
    K extends Object declared in class TreeMap  
    V extends Object declared in class TreeMap  
  
alljoyn_java/test/org/alljoyn/bus/MultipleReturnValuesTest.java:69: warning: [rawtypes] found raw type: HashMap  
            HashMap<String,String>[] hm = (HashMap<String,String>[]) new HashMap[2];  
                                                                         ^  
  missing type arguments for generic class HashMap<K,V>  
  where K,V are type-variables:  
    K extends Object declared in class HashMap  
    V extends Object declared in class HashMap  
```    
（3）(......前面還有若干行類似的)  
```
alljoyn_java/test/org/alljoyn/bus/ifaces/IntrospectableTest.java:54: warning: [rawtypes] found raw type: Class  
                                                         new Class[] { Introspectable.class });  
                                                             ^  
  missing type arguments for generic class Class<T>  
  where T is a type-variable:  
    T extends Object declared in class Class  
alljoyn_java/test/org/alljoyn/bus/ifaces/PeerTest.java:64: warning: [rawtypes] found raw type: Class  
                                                         new Class[] { Peer.class });  
                                                             ^  
  missing type arguments for generic class Class<T>  
  where T is a type-variable:  
    T extends Object declared in class Class  
100 errors  
93 warnings  
scons: *** [alljoyn_java/test/build/linux/x86/debug/obj/classes/org/alljoyn/bus/AddressBookInterface.class] Error 1  
scons: building terminated because of errors.  
```
第（1）類errors很多，都是跟junit相關的。其實我在閱讀官方文檔時已經注意到junit的問題了，junit-4.9.jar的包也下好了，也添加了相應的環境變數，可坑爹的是，我設置環境變數時少打了個"-"，囧rz。
如果你壓根沒下載junit的jar包，或者沒設置junit的環境變數，那麼編譯java的時候肯定是會報這些errors的。
第（2）（3）類warnings，一看就是泛型的問題，忽略之。
更正錯誤，在CLASSPATH環境變數裡面添加/usr/share/java/junit-4.9.jar後
再次輸入編譯命令
```
$ scons OS=linux CPU=x86 BINDINGS=c,cpp,java  
```
輸出資訊包括
```
wsbuild(["ws"], ["build_core/$DISTDIR"])  
Evaluating whitespace compliance...  
Config: /opt/alljoyn-14.06/core/alljoyn/build_core/tools/conf/ajuncrustify.cfg  
Note: enter 'scons -h' to see whitespace (WS) options  
whitespace.db not found a new one will be created.  
It appears that 'uncrustify' is not installed or is not on your PATH. Please check your system and try again.  
scons: *** [ws] Explicit exit, status 2  
scons: building terminated because of errors.  
```
查看官方文檔可以看到這麼一段：
```
Whitespace policy checker
By default the whitespace policy checker runs every time. If you continually get build errors associated with the whitespace.py script, it can be shut off using this command:
$ scons WS=off
If the whitespace policy checker reports a whitespace policy violation, it lists which files have the violation. To see the lines of code that are violating the AllJoyn whitespace policy, run:
$ scons WS=detail
Uncrustify can automatically fix your files to adhere to the whitespace policy.
$ scons WS=fix
```
於是將編譯命令改為
```
$ scons OS=linux CPU=x86 WS=off BINDINGS=c,cpp,java  
```
終於得到輸出
```
scons: done building targets.  
```
而且可以看到
```
spark@jaguarh:/opt/alljoyn-14.06/core/alljoyn/build/linux/x86/debug/dist/java/lib$ ls  
liballjoyn_java.so  
```
終於得到想要的liballjoyn_java.so，這是linux下的共享庫，有點類似Windows下的.dll文件。
用AllJoyn框架編寫的Java程式在需要運行時，會用到liballjoyn_java.so


============================================================
## AllJoyn Overview
#### AllJoyn是什麼？
- 2011年2月9日發佈，由 QuiC（高通創新中心）開發維護的開源軟體 項目，採用 Apache license 2.0 許可協定 
- AllJoyn名字的由來：All to Join in the fun 
- 面向移動設備的 secure, ad hoc, proximity-based P2P通信框架 
- 提供簡單的API，跨平台、設備無關，支援多種編程語言，易於集成 到現有應用中
      - 目前支援的OS：Linux, Android, WinXP, Win7 
      - 目前支援的編程語言：C++, Java (對JavaScript的支援正在開發中)
- 支援各種短距離無線通信技術，目前支援 WiFi 和 Bluetooth，下一 步會支援 WiFi-Direct，將來基於高通 FlashLinq 技術可擴展到 1km 範圍內 P2P 應用
- 官方網站：
      - https://www.alljoyn.org 
      - https://developer.qualcomm.com/develop/mobile-technologies/peer-peer-alljoyn

#### AllJoyn的特點
- 真正的P2P通信，無需3G網，無需訪問雲端，無需伺服器
      - Simple device and service discovery
      - Security framework for authenticated and encrypted communications per application/service
      - Managed networking and message routing
      - Object-oriented programming model
- 針對移動嵌入式環境而優化
    - Low latency
    - Header compression
    - Reliable and unreliable transport
    - Point-to-multipoint communications
- 主要應用場景
    - Secure file sharing
    - Multi-player gaming
    - Social media sharing
    - Multi-user productivity tools
AllJoyn與其他類似技術的區別
- 提供了完整全面的 P2P 解決方案，解決了移動設備間 P2P 通信中存在的很多問題：設備發現、配對、消息路由、 安全、與底層傳輸技術無關，等等
- 針對移動設備專門優化
- 支援認證和加密的安全機制 . 為開發者提供了簡單易用而功能強大的API
AllJoyn官方文檔
- Documentation
    -  Introduction to AllJoyn [PDF]
    - AllJoyn Android Environment Setup Guide [PDF]
    - Guide to AllJoyn Development Using the Java SDK [PDF]
    - AllJoyn Android C++ Sample Programs Walkthrough [PDF]
- API Reference
    - C++ API Reference Manual
    - Java API Reference Manual
    - C++ API changes between 2.2.0 and 2.3.0 [TEXT]
    - Java API changes between 2.2.0 and 2.3.0 [TEXT]
- Build Environment
    - Configuring the Build Environment (Linux Platform) [PDF]
    - Configuring the Build Environment (Windows Platform) [PDF]
AllJoyn官方技術博文
- What is AllJoyn? How can I use it?
  https://developer.qualcomm.com/blog/what-alljoyn-how-can-i-use-it
- Key Concepts of AllJoyn
  https://developer.qualcomm.com/blog/key-concepts-alljoyn
- Developing Peer-to-Peer Apps with AllJoyn - Let Us Do the Heavy Lifting
  https://developer.qualcomm.com/blog/developing-peer-peer-apps-alljoyn-%E2%80%93-let-us-do-heavy-lifting
- Making It Easy for Devices to Connect - The AllJoyn Peer-to-Peer Architecture
  https://developer.qualcomm.com/blog/making-it-easy-devices-connect-%E2%80%93-alljoyn-peer-peer-architecture
- Making It Easy for Devices to Connect - AllJoyn Code Snippet Walk-Through
  https://developer.qualcomm.com/blog/making-it-easy-devices-connect-%E2%80%93-alljoyn-code-snippet-walk-through
- Making It Easy for Devices to Connect - The AllJoyn Security Framework
  https://developer.qualcomm.com/blog/making-it-easy-devices-connect-%E2%80%93-alljoyn-security-framework
- Chinese Developers Showcase Apps Using AllJoyn
  https://developer.qualcomm.com/blog/chinese-developers-showcase-apps-using-alljoyn
AllJoyn FAQ
- https://developer.qualcomm.com/develop/mobiletechnologies/peer-peer-alljoyn/faq 
- https://www.alljoyn.org/forums/developers/faqs
AllJoyn基本概念（1）
- 總線(Bus)
    - 實現P2P通信的基礎 
    - AllJoyn 的底層協定類似於D-Bus，相當於是跨設備分佈式的 D-Bus
- 總線附件(Bus Attachment)
    - 每一個連接到總線上的Alljoyn應用程式被稱為總線附件，可用C++或Java編寫 
    - 每個總線附件有獨一的名稱(unique name)，當每次連接到總線時自動分配 
    - 每個總線附件可以有一個易讀的名稱(well-known name)，用於標識服務，例如 「org.alljoyn.bus.addressbook」
- 總線介面(Bus Interfaces)
    - 類似於Java中的介面，定義了方法、信號處理函數和屬性 
    - 所有總線方法(Bus Methods)可使用簡單或複雜的數據類型（數組、結構等）作為參數 和返回值
AllJoyn基本概念（2）
- 總線對像(Bus Objects)
    - 用於實現總線介面，每個總線對像實現一個或多個總線介面
    - 處理遠端方法調用(Remote Method Calls)和發出信號(signals)、消息(messages)
    - 總線對像通過總線附件註冊到總線上
    - 每個總線對像有一個類似於文件路徑的路徑名，例如/org/AllJoyn/Games/chess，用於遠端方法調用
- 代理總線對像(Proxy Bus Object)
    - 一旦總線附件之間建立連接，應用程式創建一個代理總線對像，實現遠端方法調用(Remote Method Calls)並準備好從總線上接收信號(signals)
    - 遠端方法調用是同步的，信號則是異步的且可以一對多（廣播）或一對一
- service 和 client
    - P2P 應用中提供服務的一方稱為 service，使用服務的一方稱為 client
    - 一個應用程式可以同時是 service 和 client（例如chat）
- session
    - 在宣告服務後，service 需創建一個或多個 session，client 發現服務後加入 session
    - 每個 session 有一個 session port，類似於 socket 通信中的 port
    - session 的兩種情形：
- point-to-point session：兩個 peer 之間交互 
- multipoint session：多個 peer 加入同一個 session，組成一個 group
AllJoyn基本概念（3）
- AllJoyn daemon——實現P2P通信的核心
    - daemon通過進程間通信（IPC）與應用程式通信，應用程式只與 daemon打交道
    - daemon提供一個抽像層處理所有的網路傳輸、消息路由、命名空間管理等
    - 整個AllJoyn系統相當於一個虛擬總線，連接多個AllJoyn daemons和總線附件
    - daemon是用 C++編寫的 native程式，運行在不同作業系統上的
    - daemons可實現互聯 在應用程式啟動之前必須先啟動daemon
- AllJoyn daemon 在 Android 上的三種實現形式
    - 第一種：Android app（AllJoyn.apk）
- 只支援 WiFi/TCP 傳輸 
- 無需 root 權限
    - 第二種：純C++編寫的可執行程式，在 adb shell 下運行（alljoyn-daemon）
- 若使用 WiFi 傳輸無需 root 權限 
- 若使用 Bluetooth 傳輸需 root 權限，且藍牙協定棧限定用 bluez 
- 可在 init.rc 中自動加載
    - 第三種：與應用程式捆綁在一起（bundle），不需要單獨啟動daemon
- 適用於發佈基於AllJoyn開發的應用程式
AllJoyn基本概念（4）
- 設備發現和建立連接的過程
    - 註冊(Register): 連接在總線上的對象為自身進行註冊 
    - 宣告(Advertise): 連接在總線上的對象通過IP組播（multicast）宣告自身的存在 
    - 發現(Discover): 發現其他對象的存在
- 在使用藍牙時借助藍牙本身的 SDP 進行發現
- 設備連接過程示意圖：
AllJoyn基本概念（5）
- 設備之間通信的方式
    - 遠端方法調用（同步） 
    - Signal（異步） 
    - Raw session（直接 socket 通信，應用程式可選擇基於 TCP 或 UDP ）
簡單應用程式代碼示例——echo
總線介面定義：
``` java
import org.alljoyn.bus.BusException; 
import org.alljoyn.bus.annotation.BusInterface; 
import org.alljoyn.bus.annotation.BusMethod; 
/* * This interface implements a simple echo method that returns the same string * that is receives. */ 
@BusInterface 
public interface EchoInterface {
    /* * Echo a string. * * inStr is the string to be echoed by the service, returns the echoed string. */ 
    @BusMethod(signature="s" replySignature="s") 
    public String Echo(String inStr) throws BusException;
}
```
- 簡單應用程式代碼示例——echo（續）
Service端：
```java
public class Service implements SimpleInterface, BusObject { 
    public static void main(String[] args) {
        /* Create a bus connection and connect to the bus */
        BusAttachment bus = new BusAttachment(Service.class.getName());
        bus.connect();
        /* Register the service */
        Service service = new Service();
        bus.registerBusObject(service, "/myobject");
        /* Request a well-known name */
        try {
            bus.RequestName("org.alljoyn.echo" REQUEST_NAME_NO_FLAGS);
        } catch (BusException ex) {
            return;
        }
        /* Echo until told to stop */
        while (!stop) { Thread.sleep(10000);
        }
    }
    /* Implementation of the echo method */
    public String Echo(String inStr) {
        return inStr;
    }
}
```
簡單應用程式代碼示例——echo（續）
Client端：
``` java
public class Client { 
    public static void main(String[] args) { 
        /* Create a bus connection and connect to the bus */ 
        BusAttachment bus = new BusAttachment(Client.class.getName()); 
        bus.connect(); 
        /* Get a remote object */ 
        Class[] ifaces = { EchoInterface.class }; 
        ProxyBusObject proxyObj = bus.getProxyBusObject("org.alljoyn.echo" "/myobject" ifaces); 
        SimpleInterface proxy = proxyObj.getInterface(EchoInterface.class);
        /* Call the ping method on the remote object */ 
        try { 
            String ret = proxy.Echo("Hello World"); 
            System.out.println(「Echo returned: " + ret); 
        } catch (BusException ex) { 
            return; 
        }
    } 
}
```
AllJoyn應用程式典型API調用流程示意
service端： client端：
```
registerBusListener
registerBusListener (callback:foundAdvertisedName, lostAdvertisedName)
registerBusObject connect connect findAdvertisedName requestName joinSession (callback: sessionLost) getProxyBusObject
bindSessionPort (callback: acceptSessionJoiner, sessionJoined)
advertiseName
Remote Method Calls
```
AllJoyn的安全機制
- AllJoyn的安全模型 —認證和加密(Authentication and encryption) 
- 認證和加解密是基於應用程式實現的，總線只負責傳輸和路由而並不參與認證和加解密
- 每個應用程式維護各自的 key store並採用密碼保護
- AllJoyn支援 3種安全機制，基於Transport Layer Security (TLS)協議，應用開發者根據應用程式的類型和所傳輸數據的種類來選擇 3種機制之一：
    - PIN-code 
    - logon 
    - certificate-based
- 安全和非安全應用程式的差別：
    - 前者在定義總線介面時需使用@Secure註釋符，後者無 
    - 前者需定義一個class實現AuthListener 介面，在該類中實現兩個方法：requested 和 completed
AllJoyn的安全機制（續）
安全機制工作原理：
加入安全機制的應用程式代碼示例
總線介面定義：
```java
import org.alljoyn.bus.BusException; 
import org.alljoyn.bus.annotation.BusInterface; 
import org.alljoyn.bus.annotation.BusMethod; 
import org.alljoyn.bus.annotation.Secure; 
@BusInterface(name = "org.alljoyn.bus.samples.secure.SecureInterface") 
/* * The @Secure annotation marks requests any method calls on this interface to first authenticate 
   * then encrypt the data between the AllJoyn peers. */ 
@Secure public interface SecureInterface { 
    @BusMethod String Ping(String inStr) throws BusException; 
}
```
加入安全機制的應用程式代碼示例（續）
Service端：
```java
...... 
/* * The main differences between a secure application and a plain application, besides the 
   * @Secure annotations of the interfaces, are encapsulated in the AuthListener. The 
   * BusAttachment calls the listener with various authentication requests in the process of 
   * authenticating a peer. The requests made are dependent on the specific authentication 
   * mechanism negotiated between the peers. 
   * 
   * This class, registered with the BusAttachment, supports all the available authentication 
   * mechanisms. */ 
class AuthListeners implements AuthListener { 
    /* * Authentication requests are being made. Contained in this call are the mechanism in use,
       * the number of attempts made so far, the desired user name for the requests, and the
       * specific credentials being requested in the form of AuthRequests.
       *
       * A true return value tells the BusAttachment that the requests have been handled.
       *
       * This simply defers to the specific listener based on the mechanism in use. */
    public boolean requested(String mechanism, String peer, int count, String userName, AuthRequest[] requests) { 
        .... .... 
    } 
    /* * An authentication attempt has completed, either successfully or unsuccessfully. 
       * This simply defers to the specific listener based on the mechanism in use. */ 
    public void completed(String mechanism, String authPeer, boolean authenticated) { 
        .... .... 
    } 
} 
......
```
開發工具
- scons：一個 Python寫的自動化構建工具，是對 gnu make 改進的替代工具 
- D-Feet：一個D-Bus調試工具
- C++ Code Generator Tool (ajcppgen)
    - 根據 service interface 定義自動生成 C++ 框架代碼的工具 
    - 輸入是XML文件，描述 service object(s) and interface(s) 
    - 輸出是C++ 文件，包括 service 端和 client 端
Ubuntu下 AllJoyn源碼編譯方法
- 預先準備工作：
    - 成功編譯過的完整 Android源碼，假設路徑為 /home/zhuangwf/android/ 
    - 安裝 JDK 1.6，假設安裝到 /usr/java/jdk1.6.0_30/ 
    - 設置如下環境變數（可加到 /etc/profile 或 ~/.bashrc 中）：
     export JAVA_HOME=/usr/java/jdk1.6.0_30 
     export CLASSPATH=$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:/home/zhuangwf/android/out/ host/linux-x86/framework/junit.jar 
     export PATH=$JAVA_HOME/bin:$PATH

安裝 Android NDK r7，假設安裝路徑為 /home/zhuangwf/android-ndk-r7/ 
安裝 scons：apt-get install scons 
安裝 uncrustify (版本0.57 is OK) AllJoyn源碼，假設路徑為 /home/zhuangwf/alljoyn/
. 編譯源碼的命令：
```
scons OS=android CPU=arm ANDROID_NDK=/home/zhuangwf/android-ndk-r7/ ANDROID_SRC=/home/zhuangwf/android/ ANDROID_TARGET=generic WS=off
```

Ubuntu下AllJoyn sample app編譯和運行方法
- 預先準備工作：
    - 安裝 eclipse 和 Android SDK
- 編譯 sample應用程式：
    - sample app 有C++寫的(帶java寫的UI) 也有純 Java 寫的，其中 Java sample app 源碼位於 /home/zhuangwf/alljoyn/alljoyn_java/samples/android/，經實際驗證OK 
    - 用 eclipse 編譯 sample app
- 運行 sample app方法：
    - 安裝 sample app 之 .apk 到各設備上 
    - adb push /home/zhuangwf/alljoyn/build/android/arm/debug/dist/bin/alljoyn-daemon 到各設備上 
    - 各設備連接 WiFi 
    - 在各設備 adb shell 下運行：alljoyn-daemon --internal –fork 
    - 在各設備上運行 sample app
AllJoyn應用案例
- NearVerse 公司，在其產品 LoKast 的 Android 版本上 使用了 Alljoyn 技術 
- Aliph公司，音樂共享軟體JamJoyn
- 一些 multi-player遊戲：例如 QwikDraw、Spudball
- 國內公司：
    - Tencent QQ Chat & Contact Share A-One Gaming Tapas Business Card Sharing DuoMi Music AliPay by Alibaba
- 此外，高通已在其參考設計 Qualcomm Reference Design (QRD)上將 AllJoyn集成到 Android中，作為缺 省的功能提供給設備製造商和應用開發者
存在的問題
- AllJoyn只提供了一個基本的通用的P2P框架，沒有提供針對特定應用類型的profile，例如象 DLNA 那樣專門面向
  媒體應用的框架或者象 bluetooth 那樣提供各種應用profile，需應用程式自己實現 
- AllJoyn框架中未定義類似於 UPnP 的設備描述、服務描 述機制，service的命名、方法的定義等也都沒有統一的 
  規範和標準，均需由應用程式自行約定（因此 service端 和 client端應用程式需由同一開發者開發維護）
- 在企業辦公環境中因 WiFi AP 往往被設為禁止轉發 IP 組 播包，因而 AllJoyn 設備發現失效（其他類似技術例如 UPnP也存在同樣問題）
- AllJoyn 主要解決設備發現和連接，比較適合基於簡單數 據傳輸的控制類應用，不適合實時大數據量傳輸應用（例 如流媒體），對這類應用需與其他技術相結合。


============================================================
## Alljoyn 怎麼利用Raw格式傳輸文件
這裡的利用到了demo中的RawClient和RawService。請參考SDK。
下面的是demo中傳輸一個字串所採用的方式：
```java
if(mIsConnected == false|| mStreamUp == false) {
    try{
        shortcontactPort = 888;
 
        SessionOpts sessionOpts = newSessionOpts();
        sessionOpts.traffic = SessionOpts.TRAFFIC_RAW_RELIABLE;
        Mutable.IntegerValue sessionId = newMutable.IntegerValue();
        Status status = mBus.joinSession(RAW_SERVICE_NAME, contactPort, sessionId, sessionOpts,newSessionListener());
        if(status != Status.OK) {
            break;
        }
        mRawSessionId = sessionId.value;
 
        Mutable.IntegerValue sockFd = newMutable.IntegerValue();
        status = mBus.getSessionFd(mRawSessionId, sockFd);
        if(status != Status.OK) {
            break;
        }
 
        Field field = FileDescriptor.class.getDeclaredField("descriptor");
        field.setAccessible(true);
        FileDescriptor fd = newFileDescriptor();
        field.set(fd, sockFd.value);

        mOutputStream = newFileOutputStream(fd);
        mStreamUp = true;
    }catch(Throwable ex) {
        Log.i(TAG,"ERROR "+ex);
    }
}
``` 
doSendFile(); 如果傳輸文件則替換下面的代碼為這個函數即可。
```
if(mStreamUp == true) {
    try{
    String string = "AllJoynis a peer-to-peer technology that enables ad hoc proximity-based";/*in my case I have a big string, something like 400 lines*/

        mOutputStream.write(string.getBytes());
        mOutputStream.flush();

    }catch(IOException ex) {
        logInfo("Exception writing and flushing the file");
    }
}
```
如果是傳輸文件的話，需要改寫，即把if(mStreamUp == true)後面的代碼改寫為如下的函數即可。
```
private void doSendFile(){
    Log.i(TAG,"doSendFile()");
    if(mStreamUp == true){

        try{
            String filepath = "/sdcard/Teste.jpg";
            file = newFile(filepath);
            mOutputStream.write(getBytesFromFile(file));
            mOutputStream.flush();
        }catch(Exception ex) {
            Log.i(TAG,"ERRO writing file "+ex);
        }
    }
}
 
public byte[] getBytesFromFile(File file) throwsIOException {
    Log.i(TAG,"getBytesFromFile()");
    InputStream is = newFileInputStream(file);
    longlength = file.length();
    if(length > Integer.MAX_VALUE) {
        System.out.println("Arquivo muito grande");
    }
    byte[] bytes = newbyte[(int) length];
    intoffset = 0;
    intnumRead = 0;
    while(offset < bytes.length && (numRead = is.read(bytes, offset, bytes.length - offset)) >=0) {
        offset += numRead;
    }
    if(offset < bytes.length) {
        thrownewIOException("Could not completely read file " + file.getName());
    }
    is.close();
    returnbytes;
}
```

============================================================
## Alljoyn伺服器框架二總線及會話
Alljoyn伺服器框架2總線及會話 
一個基本的alljoyn伺服器框架包含關於及通知伺服器，以及控制及配置伺服器（可選）。
最好重寫通知伺服器模組，編譯成用戶指定名稱。

1. 生成總線
伺服器/用戶端所需總線。
伺服器註冊一個發送方，用戶端需要一個接受方。
我用的名字是ChatServiceApp
``` java
BusAttachment* bus = newBusAttachment(「ChatServiceApp」, true);
QStatus status = bus->Start();
status = bus->Connect();
if (authListener)
{
status =::EnableSecurity(bus, authListener);
}
```
增加DBus路由：
```java
m_Bus->AddMatch(「Interface name」);
m_Bus->RegisterBusObject(*m_SuperAgent);
```
我想在總線廣播消息，因此初始化發送方或接收方：
```java
prodService->initSend(bus,propertyStoreImpl);
Receiver->setApplications(listOfApps.c_str());
conService->initReceive(busAttachment,Receiver);
```
一個應用要承載所有功能可不是個好主意。 
為伺服器/用戶端消息交換選用不同的名字。

2.會話：
設備向會話宣告一個獨有的名字，會話使用P2P通信。
```
m_Bus->JoinSession(name, PORT, this,s_sessionId, opts);
m_Bus->SetLinkTimeout(s_sessionId,timeout);
```
接收消息需註冊總線監聽器，如只是發送消息不需註冊總線監聽器。
Chat.cc演示如何在總線增加一個基體會話。但這是多對多拓撲，我希望生成一個C/S演示
當前會話向新用戶廣播到達通知。
最相似的演示為消費者與產品伺服器演示
原文鏈接：http://likall.com/blog/?p=65

Alljoyn伺服器框架2總線及會話（2） 
看起來一個總線似乎只支援一個會話，因此對 c/s模式而言，它需要至少兩個總線。一個用於廣播，另一個用於私有對話。
伺服器廣播在線客戶資訊，客戶通過心跳脈衝向伺服器發送自己的資訊。重寫通知伺服器很簡單，為其增加客戶屬性就能很好工作了。
當然，需要增加一個新消息處理程式。使用Jsoncpp來處理消息並在字典中存儲屬性是不錯的選擇。
上述示範代碼結構慘不忍睹，看起來像是用C編寫而成。我用OO進行重寫。目前，我得把注意力集中在會話傳輸上，也許需要一個抽像工廠類來生成應用會話。
目前一切都好。 
原文鏈接：http://likall.com/blog/?p=75

============================================================
## 編寫一個基於AllJoyn的APP
1. 裝載alljoyn庫文件
2. 連接 alljoyn deamon
3. 監聽設備
4. 創建本地 alljoyn bus介面
5. 進程實現 alljoyn bus介面，實現進程調用RPC
6. 獲取介面事例，調用實習數據傳輸

1. 裝載alljoyn_java.so庫文件
/libs/armeabi/liballjoyn_java.so
```
static {
System.loadLibrary("alljoyn_java");
}
```
2. 連接alljoyn bus
```
mBus = new BusAttachment("applicationName");
mBus.registerBusObject(this, "/servicepath");
mBus.connect();
int flags = 0; //no request name flags
mBus.requestName("com.my.well.known.name", flags);
```
3. 監聽獲取周圍設備資訊
```
private class ChatBusListener extends BusListener {
    public void foundAdvertisedName(String name, short transport, String namePrefix) {
        short contactPort = CONTACT_PORT;
        SessionOpts sessionOpts = new SessionOpts();
        Mutable.IntegerValue sessionId = new Mutable.IntegerValue();
        Status status = mBus.joinSession((String) msg.obj,contactPort,sessionId,
        sessionOpts,new SessionListener());
    }
        public void lostAdvertisedName(String name, short transport, String namePrefix) {
        //TODO
    }
}
```
4. 本地創建alljoyn bus介面
```
. @BusInterface (name = "org.my.interface.name")
. public interface SampleInterface {
  @BusMethod
   public String MyMethod(String inStr) throws BusException;
   @BusSignal
   public void MySignal(String inStr) throws BusException;
   @BusProperty
   public String GetMyProperty() throws BusException;
   @BusProperty
   public void SetMyProperty(String myProperty) throws BusException;
  }
```
5. 實現介面，遠端rpc
```
class SampleService implements SampleInterface, BusObject {
	public String MyMethod(String inStr) throws BusException{
		System.out.println(inStr);
	}
	@BusSignalHandler(iface = " org.my.interface.name ", signal = "MySignal")
	public void MySignal(String inStr) throws BusException{
		System.out.println(inStr);
	}
	...
}
```
6. 獲取alljoyn bus介面實例，實現名片交換
```
mProxyObj = mBus.getProxyBusObject("com.my.well.known.name",
"/MyService",sessionId.value,new Class[] { SampleInterface.class });
mSampleInterface = mProxyObj.getInterface(SampleInterface.class);
mSampleInterface.MyMethod(str);
```

============================================================
## 【AllJoyn框架-04】瘦用戶端在windows環境下的運行示例
alljoyn
1、介紹
thin client，顧名思義即瘦用戶端，主要是指運行小型嵌入式設備上的程式，類似於傳感網的一個節點，像前面文章講述的arduino due平台就是一個瘦用戶端。
由官方提供的SDK來看，它不僅可在arduino上跑，也可在windows、linux環境下運行。所以今天來初步學習一下其在windows環境下運行的範例basic。
2、下載源碼並編譯
在這裡可下載瘦用戶端ajtcl源碼，目前的版本已達14.02.下載成功後，解壓縮，從VS命令行進入源碼目錄，執行下面命令：
```
scons TARG=win32 VARIANT=debug MSVC_VERSION=11.0 WS=off > scons.txt
```
之所以將結果導入到scons.txt文件中，是我想知道編譯發生了什麼，你可不用這麼做，直接在終端輸出一大堆資訊。
編譯完成後就會有一些重要文件生成像ajtcl.lib以及test、sample目錄下的執行文件
3、稍加修改運行
之所以感覺要修改samples/basci程式，是因為發現函數調用AJ_InfoPrintf在終端沒有輸出，於是把AJ_InfoPrintf全部換成AJ_Printf，再重新執行scons編譯。
接下來就執行basic/basic_service.exe和basic/basic_client.exe。不過得先啟動另一個後台程式:SampleDaemon.exe，其在alljoyn-14.02.00-thin_client-sdk-windows.zip中，當然也可編譯SampleDaemon.cc得到。
下面是運行情況：
SampleDaemon:
```
D:\Alljoyn\ajtcl-14.02\samples>D:\alljoyn-sdk\alljoyn-14.02.00-thin_client-sdk-windows\bin\SampleDeamon.exe
AllJoyn Library version: v14.2.0
AllJoyn Library build info: AllJoyn Library v14.2.0 (Built Fri....)
RequestCredentials for authenticating using mechanism ALLJOYN_PIN_KEYX
RequestCredentials for authenticating using mechanism ALLJOYN_PIN_KEYX
8225.872 ******* ERROR ALLJOYN iodisp           ...\src\Message_Parse.cc:1008 | 0x0004
8225.872 ******* ERROR ALLJOYN iodisp           ...\src\RemoteEndpoint.cc:645 | 0x0004
RequestCredentials for authenticating using mechanism ALLJOYN_PIN_KEYX
```
basic_service:
```
<node name="/sample">
<interface name="org.alljoyn.Bus.sample">
  <method name="Dummy">
    <arg name="foo" type="i" direction="in"/>
  </method>
  <method name="cat">
    <arg name="inSttr1" type="s" direction="in"/>
    <arg name="inSttr1" type="s" direction="in"/>
    <arg name="outSttr" type="s" direction="out"/>
  </method>
</interface>
</node>
 StartServices returned 0, session_id=0
Accepted session session_id=2631034809 joiner=:QlsoMwz5.4
000.000 aj_guid.c:76 LookupName(): NULL
Session lost. ID = 2631034809, reason = 2AllJoyn disconnect.
StartService returned 0, session_id=2631034809
```
basic_client:
```
Error: LoadNVFromFile() failed
<node name="/sample">
<interface name="org.alljoyn.Bus.sample">
  <method name="Dummy">
    <arg name="foo" type="i" direction="in"/>
  </method>
  <method name="Dummy2">
    <arg name="fee" type="i" direction="in"/>
  </method>
  <method name="cat">
    <arg name="inSttr1" type="s" direction="in"/>
    <arg name="inSttr1" type="s" direction="in"/>
    <arg name="outSttr" type="s" direction="out"/>
  </method>
</interface>
</node>
 StartClient returned 0, sessionId=2631034809
'org.alljoyn.Bus.sample.cat' (path=/sample') returned 'Hello World!'.
Basic client exiting with status 0.
```
由上可知client端向service發送Hello和World，被返回了Hello World，隨後就退出了，連接中斷，服務端重新創建
4、三大部分作用簡介
Daemon：作用就是給兩個瘦用戶端連接用的，相當於preinstalled router.這在官方文檔中介紹較詳細
basic_service：首先調用AJ_Initialize()初使化，接著列印介面的描述資訊，以xml形式，同時註冊對象。在無限循環中，創建service端，等待客戶的消息。
    一旦消息到來，判斷其id，如果是我們自定義的BASIC_SERVICE_CAT，則執行AppHandleCat操作，連接兩個字串，最後將連接後的字元封裝成消息發送。
basic_client：剛開始與service一樣，在循環中創建用戶端，如果連接成功，則將Hello及World封裝成消息發送。
    接著等待服務端的消息，收到後檢測其id，列印收到的字串


============================================================
##【AllJoyn框架-03】官方示例程式basic簡單剖析
不論是自己編譯源碼還是從官方下載SDK，在alljoyn_core\samples下的代碼很值得研究，有利於熟悉alljoyn框架的各種概念和編程套路。
今天我且對basic程式作下簡單剖析。只是簡單析一析，還不能深入到源碼級別。
讀者在熟悉之前請務必多讀幾遍官方對alljoyn framework的介紹文檔，裡面有相當多的抽像概念闡述，儘管讀了之後也不知道在說什麼，但還是讀一下為好。

分服務端和用戶端。首先看服務端：(我對示例代碼做了精簡，只保留最核心的API，這樣更能抓住主要矛盾又不影響分析)
```c
int main(int argc, char** argv, char** envArg)  
{  
    signal(SIGINT, SigIntHandler);//創建信號處理，類似於Linux中做法  
    /* 
        很多函數調用都返回了這種類型的值，與ER_OK進行比較 
        我在這裡就做了精簡，但具體寫時是需要進行異常檢測的 
    */  
    QStatus status = ER_OK;  
      
    /* 
        創建BusAttachment對像，myApp為應用程式名，且允許從遠端設備接收消息 
    */  
    s_msgBus = new BusAttachment("myApp", true);  
      
    /* 
        為總線創建介面，以INTERFACE_NAME為介面名，testIntf存儲介面描述資訊 
    */  
    InterfaceDescription* testIntf = NULL;  
    s_msgBus->CreateInterface(INTERFACE_NAME, testIntf);  
      
    /* 
        為介面添加方法，cat為方法名，後面為輸入、輸出參數及列表 
    */  
    testIntf->AddMethod("cat", "ss",  "s", "inStr1,inStr2,outStr", 0);  
      
    /* 
        介面在使用之前要先激活，激活之後不能再被修改 
    */  
    testIntf->Activate();  
      
    /* 
        註冊總線監聽對像，用以監聽總線上的事件通知 
        s_busListener是一個子對像，繼承自BusListener,SessionPortListener 
        重新實現了NameOwnerChanged，AcceptSessionJoiner等虛函數 
    */  
    s_msgBus->RegisterBusListener(s_busListener);  
      
    /* 
        啟動BusAttachment對像中獨立的線程，準備運行 
        它僅僅是啟動總線，發送和接收消息要在Connect之後才能開始 
        BusAttachment線程模型中有一個線程很特殊，它會給註冊的監聽對像發送callback（回調） 
        像BusAttachment的Start,Stop,Join方法都可看成是對底層線程方法的映射或叫封裝 
    */  
    s_msgBus->Start();  
      
    /* 
        BasicSampleObject是繼承BusObject的子類，它裡面實現了方法處理函數Cat 
    */  
    BasicSampleObject testObj;  
    //為對像添加介面  
    testObj.AddInterface(*testIntf);  
      
    //MethodEntry是個結構體  
    const MethodEntry methodEntries[] = {  
            { exampleIntf->GetMember("cat"), static_cast<MessageReceiver::MethodHandler>(&BasicSampleObject::Cat) }  
        };  
    //添加方法處理函數，即Cat  
    testObj.AddMethodHandlers(methodEntries, sizeof(methodEntries) / sizeof(methodEntries[0]));  
      
    // 為總線註冊總線對像  
    s_msgBus->RegisterBusObject(testObj);  
      
    /* 
        開始連接到alljoyn router，有一個給定的目的地。如果Connect調用沒有給參數，則試圖使用一個 
        bundled router，如果存在的話 
        可以接收和發送消息了 
    */  
    s_msbBus->Connect();  
      
    /* 
        開始發佈服務，分三步： 
        1、請求well-known name 
        2、創建會話 
        3、發佈服務名 
    */  
    const uint32_t flags = DBUS_NAME_FLAG_REPLACE_EXISTING | DBUS_NAME_FLAG_DO_NOT_QUEUE;  
    s_msgBus->RequestName(SERVICE_NAME, flags);  
      
    const TransportMask SERVICE_TRANSPORT_TYPE = TRANSPORT_ANY;  
    SessionOpts opts(SessionOpts::TRAFFIC_MESSAGES, false, SessionOpts::PROXIMITY_ANY, SERVICE_TRANSPORT_TYPE);  
    SessionPort sp = SERVICE_PORT;  
    // 綁定會話連接埠  
    QStatus status = s_msgBus->BindSessionPort(sp, opts, s_busListener);  
      
    s_msgBus->AdvertiseName(SERVICE_NAME, mask);  
      
    //等待信號，如果有中斷則退出  
    WaitForSigInt();  
      
    delete s_msgBus;  
    s_msgBus = NULL;  
  
    printf("Basic service exiting with status 0x%04x (%s).\n", status, QCC_StatusText(status));  
  
    return (int) status;  
}  
```
用戶端：
```c
int main(int argc, char** argv, char** envArg)  
{  
    signal(SIGINT, SigIntHandler);  
    QStatus status = ER_OK;  
    g_msgBus = new BusAttachment("myApp", true);  
    g_msgBus->CreateInterface(INTERFACE_NAME, testIntf);  
    testIntf->AddMethod("cat", "ss",  "s", "inStr1,inStr2,outStr", 0);  
    testIntf->Activate();  
      
    g_msgBus->Start();  
    g_msgBus->Connect();  
    static MyBusListener s_busListener;  
    g_msgBus->RegisterBusListener(s_busListener);  
    //前面的代碼與service一端差不多  
      
    //尋找發佈的服務  
    g_msgBus->FindAdvertisedName(SERVICE_NAME);  
    //等待接入會話  
    WaitForJoinSessionCompletion();  
      
    //創建代理對像進行遠端調用  
    ProxyBusObject remoteObj(*g_msgBus, SERVICE_NAME, SERVICE_PATH, s_sessionId);  
    const InterfaceDescription* alljoynTestIntf = g_msgBus->GetInterface(INTERFACE_NAME);  
  
    assert(alljoynTestIntf);  
    //給代理對像添加介面  
    remoteObj.AddInterface(*alljoynTestIntf);  
  
    Message reply(*g_msgBus);  
    MsgArg inputs[2];  
  
    inputs[0].Set("s", "Hello ");  
    inputs[1].Set("s", "World!");  
      
    //執行遠端調用，reply返回結果  
    QStatus status = remoteObj.MethodCall(SERVICE_NAME, "cat", inputs, 2, reply, 5000);  
      
    //輸出返回結果  
    if (ER_OK == status) {  
        printf("'%s.%s' (path='%s') returned '%s'.\n", SERVICE_NAME, "cat",  
               SERVICE_PATH, reply->GetArg(0)->v_string.str);  
   
    delete g_msgBus;  
    g_msgBus = NULL;  
  
    printf("Basic client exiting with status 0x%04x (%s).\n", status, QCC_StatusText(status));  
  
    return (int) status;  
}  
```
有一現象得說明一下：當我把MakeMethodCall方法裡的代碼放進main中時，程式在最後析構的時候會發生異常，不過最後返回值還是會列印出來。
若直接調用MakeMethodCall時就正常。

最後也順便說一下另外幾個工程，其實大致結構與上差不多，具體任務稍有差異
nameChanged_client是修改某個屬性名，以signal_service為服務；
signalConsumer_client是訂閱了某個屬性名信號，一旦名稱改變，它會有所反應，也以signal_servie為服務，若要看到現象，nameChanged_client也要參與進來。


============================================================
## AllJoyn Audio service compilation problems
I want to run an audio streaming server based on AllJoyn and the AllJoyn audio service doesn't seem to be buildable from the 
alljoyn/multimedia/audio folder (running scons in this folder always ends up in compilation errors). I'm building AllJoyn version 14.06.
Anybody successfully built the AllJoyn audio service on a Raspberry Pi (Raspbian)?
Thx a lot.

In order to compile the audio service you need to do it from the folder alljoyn/core/alljoyn/services/audio 
This is an example compilation command (targetting a Raspberry Pi) that also builds the audio samples:
```
scons OS=linux CPU=arm WS=fix BR=on SERVICES=about,audio BUILD_SERVICES_SAMPLES=on VARIANT=release BINDINGS=core,cpp OE_BASE=/usr
```
You'll have to install the packages libasound2 and libasound2-dev before compiling though. 
You can test if it works by running the file SinkService from the samples and streaming music to it from the Android app doubleTwist. 
If the music plays too fast make sure you modify the SConscript in alljoyn/multimedia/audio to include the asound library in the environment:
```
if audio_env['OS'] == 'linux':
        audio_env.AppendUnique(LIBS = [ 'asound' ])
```
If trying to build the audio service but for Android you should check this page. 
If you can't connect to the SinkService from doubleTwist after building see this page. 
If you can connect but SinkService hangs see this page.
If your intention is to build all AllJoyn services and bindings switch to alljoyn/core/alljoyn folder and try something like this:
```
scons OS=linux CPU=arm WS=fix BR=on SERVICES=about,audio,config,controlpanel,notification,onboarding BUILD_SERVICES_SAMPLES=on VARIANT=release BINDINGS=core,cpp,c,java,js,objc,unity OE_BASE=/usr
```

============================================================
## Alljoyn瘦用戶端庫介紹   http://www.cnblogs.com/alljoyn/p/3925910.html
1、簡介
　　本文檔對AllJoynTM瘦用戶端的核心庫文件（AJTCL）進行了詳盡的介紹。本文檔介紹了系統整體架構，AllJoyn框架
結構，並著重於介紹如何將嵌入式設備加入AllJoyn系統整體架構中。
1.1目的
　　本文檔介紹了如何使一個受限於功耗、計算能力和記憶體的設備（嵌入式設備）加入AllJoyn分佈式系統。具體而
言，本文檔包括了對AllJoyn面向嵌入式系統的方面的介紹，並著重描述了基於AllJoyn的系統的各個元件是如何與嵌入
式設備協作以構建一個基於接近式結構的，點對點的計算系統。
1.2適用人群
本文檔適用於任何想將嵌入式設備加入點對點網路的電子愛好者，包括應用開發人員、系統軟體開發人員、網路專家、
設備操作人員和系統經理。我們假設讀者已經對嵌入式系統有了基本的認識，並且已經理解了了
《Introduction to the AllJoyn Framework》（AllJoyn架構介紹）一文說描述的AllJoyn系統概況。

2、綜述
　　AllJoyn是一個開源的軟體系統，用於將運行在不同類別設備上的分佈式應用構建成一個分佈式環境，並著重於便攜
性、安全性和可動態配置性。AllJoyn不依賴於平台，即它的設計盡可能地獨立於其所運行的作業系統和軟硬體。
　　AllJoyn標準核心庫（AJSCL）被設計成可用於 Microsoft Windows、Linux、Android、iOS、OS X、OpenWRT和瀏覽
器插件的系統環境中。這些軟體系統的共同特點是它們運行於通用型電腦系統。通用型電腦通常擁有相當數量的記憶體
、足夠大的功耗和計算能力，甚至很多作業系統都支援多處理器、多線程和多語言環境。
　　與之相對的是，嵌入式系統往往只針對單一功能，並運行於某個設備中的嵌入式處理器中。由於其需要完成的功能
有限，工程師們往往通過減小記憶體容量、降低處理器速度和功耗、減少外設介面和用戶介面等方式來優化系統，以降
低產品成本和體積。AllJoyn 瘦用戶端核心庫（AJTCL）便是針對嵌入式系統的分佈式編程所設計。
　　由於AJTCL的運行環境資源有限，AllJoyn元件定會受到此系統的很多限制。具體來說，這意味著我們無法像編寫
AllJoyn路由程式一樣（需要多線程支援）使用多個網路連接和大量的RAM和ROM資源，也無法使用那些支援多語言的面向
對象的編程環境。鑒於這種情況，AJTCL僅僅包含了一些總線連接程式（參看《Introduction to the AllJoyn Framework》
一文），並完全由C語言寫成。其對應於介面、方法、信號、屬性和總線對象的數據結構都經過了大幅優化以減少空間佔
用，同時API（應用程式介面）也大不相同。
儘管AJTCL與AJSCL的API大不相同，但他們所有的核心概念都是相通的，AJTCL只是以一個更緊湊的形式出現，或者實際
上是遠端運行在一個（計算能力）更強的機器上。

3、概念性模型
　　如之前章節中所言，絕大多數在AJTCL中所使用的高度抽像的概念都與其在AJSCL系統中的概念相同。
《Introduction to the AllJoyn Framework》一文中「Conceptual Overview」一章已經向讀者介紹了這些概念。在本
章中，我們假設讀者已經對上文的相關概念有所熟悉，因此本章只介紹兩者的不同點，用於幫助讀者理解AJTCL的架構。
3、1 AllJoyn瘦用戶端核心庫仍然是AllJoyn
　　理解「AJTCL是AllJoyn架構的一部分」對於理解整個AllJoyn系統很重要。瘦用戶端的核心庫程式可完全地與AJSCL
互動。鑒於AllJoyn網路傳輸協定在兩種類型的庫中都有實現，AJSCL程式完全不用考慮他到底是在跟AJTCL程式對話還是
在跟AJSCL程式對話。
　　回顧《Introduction to the AllJoyn Framework》一文，AllJoyn分佈式總線的基本結構由幾個處於不同的、物理
上分離的電腦系統所構成，如圖1所示。

　　如圖所示，下標為Host A和Host B的兩個虛線框表示在給定的兩個主機（host computer）上的兩個總線段
（bus segment）。每個總線段都包含一個AllJoyn路由節點（以標注了D字母的圓圈表示）。一個主機上可能連接了多個
總線掛件（bus attachments），每個總線掛件都與一個本地的守護進程（以六邊形表示）相連接。這些總線掛件分為伺
服器（services）和用戶端（clients）兩類。
　　由於運行AJTCL的設備通常沒有足夠的資源運行路由程式，AllJoyn架構對瘦用戶端進行了一些改變，使運行瘦用戶
端的設備借助於分佈總線上其他主機上的AllJoyn路由程式連接到AllJoyn網路。具體方法如圖2所示。請注意嵌入式系統
A（Embedded System A）和嵌入式系統B（Embedded System B）與運行路由程式並管理該分佈式總線段的主機B（Host B）
並不是同一個設備。這些運行AJTCL的嵌入式系統與該總線段上的主機路由程式之間的連接通過TCP協定（傳輸控制協定，
Transmission Control Protocol）實現。

　　其中，嵌入式系統和路由節點之間的通信流稱為AllJoyn消息，如《Introduction to the AllJoyn Framework》一文
所述，包括總線方法、總線信號和對應於各個對話的屬性流。
　　在某些場合，我們允許AJTCL設備連接並借助附近尋找到的老式路由節點。我們稱這種連接關係為「不受信的關係」
（以路由節點的視角）。同樣在某些場合，我們只允許特定的AJTCL設備連接到特定的路由節點。我們稱這種關係為「受信
關係」（同樣從路由節點的視角）。
　　這些關係的建立依賴於一個在概念上與用戶端與伺服器之間的發現和連接過程相似的發現和連接過程。一個AllJoyn路
由節點通過廣播一個眾所周知的名稱來表達其對接管一類AJTCL設備的意願。這個廣播可能以路由配置包或以一個具體的
AllJoyn元件建立的廣播包的形式出現。緊隨其後的一個來自設備的連接請求將會使預備建立受信連接的路由節點開始詢問
發送該請求的AJTCL（或冒名頂替的AJTCL）以建立一個憑證。在建立非受信連接的情況下，路由節點將會允許任何連接請
求。對於非受信連接，路由節點不會允許AJTCL執行任何需要建立遠端對話的操作（和任何需要付費的操作）。
正如以上所引述的，一個AJTL設備建立連接的過程可以分為三個步驟：
發現過程
連接過程
認證過程
　　其中，發現過程除了兩種例外情況以外，都如《Introduction to the AllJoyn Framework》一文中所描述的那樣，就
像是某種服務廣播。第一種例外是AJTL發現廣播的方式通常是「靜默的」廣播。這表明路由節點不是無緣無故地發送此廣播。
　　第二種例外是對靜默廣播的響應通常是靜默的——我們稱之為「靜默響應」。這表明響應將被單播回發送者，而不是像
活躍廣播一樣被多播出去。這麼做的主要原因是為了使某些無法實現多播的嵌入式設備加入Alljoyn分佈式系統。

3.2什麼是AllJoyn瘦用戶端核心庫設備？
　　人們通常人為AJTCL設備和感測器網路（Wireless Sensor Network，WSN）中的感測器節點（Sensor Node，SN）在概念
上很相似。感測器節點通常是某些小體積、低功耗、低配置的感測器或者執行器件。它們通常可以檢測周圍環境、與外界通
信，甚至有可能在基於網路處理或外界事件的激勵下執行某種動作。這是一個非常寬泛的定義，下面舉的一部分設備的例子
適用於這個定義：
點燈開關、自動調溫器、空調、排風閥、煙霧感測器、運動檢測感測器、人體感測器、麥克風、揚聲器、
耳機、門、門鈴、烤箱、電冰箱、烤麵包機
　　關於無線感測器網路的文章一搜一大把。AllJoyn系統與之不同的是，無線感測器網路通常使用自組織、多跳、點對點
的無線網路（Self-organizing multi-hop ad hoc wireless networks），而不會主要關注安全問題；而AllJoyn架構就像
是運行於基礎模式的Wi-Fi網路，即給定的設備必須經過認證和組織。為了完成某個Wi-Fi網路的身份認證，AJTCL使用了一
個名為「onboarding」的過程。這個登陸服務的架構允許一個假定沒有友好的用戶介面的運行瘦用戶端的設備從他的目標網
路獲取足夠的資訊，用以完成加入目標網路所需的身份認證過程。這個登錄服務架構將在一個專門的文檔中定義並介紹。
　　如同一個感測器節點所扮演的角色一樣，一個AJTCL設備通常包含一項AllJoyn發現服務。該服務會以AllJoyn信號的形
式通過連接的硬體和通信事件探索自己的周圍環境。如《Introduction to the AllJoyn Framework》一文所描述，它可以
通過監聽其他設備發來的信號，或者響應其他AllJoyn用戶端的遠端方法，從而對外界事件進行響應。

4 瘦用戶端核心庫架構
　　由於AllJoyn瘦用戶端核心庫（AJTCL）必須運行在那些功耗受限、計算能力有限、資源緊缺的設備上，因此它無法像運
行在通用型電腦系統上那樣使用和AllJoyn標準核心庫（AJSCL）一樣的架構。
　　一個AJSL或服務進程的分層結構如圖3所示。《Introduction to the AllJoyn Framework》一文描述了這些層次結構的
更詳盡細節。需要特別注意的是， 每個Alljoyn用戶端或伺服器程式都會以這種層次結構來構建AllJoyn應用。
　　每個運行AJSCL的主機上至少都要運行一個路由程式。這個路由程式可以以單獨的路由進程形式運行，或者寄生於某個
應用程式中運行。AJSCL路由程式的分層結構如圖4所示。
　　注意到，路由程式可以為路由節點之間路由消息的傳遞提供額外的支援，並能支援如Wi-Fi Direct的多重網路傳輸機制
。這個功能可以有效地降低計算能力、功耗和記憶體的開銷。
　　我們很明顯無法在嵌入式系統中運行如此數量的程式，所以AJTCL最大程度地縮減了在給定設備上運行所需的代碼量。
AJTCL只使用最基礎的C運行環境，並通過借助其他設備的計算能力實現路由規則。如圖5所示，對比AJSCL，AJTCL捨去了大
部分AJSL系統開銷。AJTL僅僅為總線掛件提供少量必須的API（應用程式介面），並將AllJoyn消息介面直接提供給程式員，
而不是提供間接的介面函數。
　　消息層沒有提供抽像的傳輸機制，而是直接使用了用戶數據塊傳輸協定（UDP）和TCP協定。分層結構中的連接埠層非常
簡單，又幾個簡單必須的本地系統函數構成。為了是代碼體積最小化，其完全以C語言寫成。由於使用了這些優化機制，一
個AJTCL系統只需25K位元組的記憶體就可運行，而一個綁定了路由功能和C++版本用戶端和伺服器程式的應用可能需要十倍
數額的記憶體開銷，而一個Java語言版本的AllJoyn程式則需要40倍左右的開銷。

5 整合運行
　　為了使本章的討論更加具體，在此舉了兩個分佈式系統的例子。第一個例子是一個最小化的AllJoyn系統，由一個運行
在智慧手機上的AllJoyn應用程式和一個簡單的AJTCL設備構成。此例闡述了上文描述的受信路由關係。第二個例子稍微複雜
一些，包括一個運行在無線路由器上的路由程式。
　　註釋　　通常的情形是由一個運行OpenWRT系統的路由器來運行預裝好的AllJoyn路由程式。此路由程式接受那些連接到
Wi-Fi網路的瘦用戶端庫發來的非受信連接請求。
　　少量AJTCL設備連接到路由器，並在基於AllJoyn的無線感測器網路中扮演感測器節點的角色，而一個通用型電腦則完成
數據融合的工作。
　　註釋　　在無線感測器網路中，數據融合是將一些不同的節點收集到的結果整合到一起的過程，或者將其結果與其他傳
感節點獲得的結果融合到一起，以便做出決策。

5.1 一個最小化的瘦用戶端系統
　　一個最小化的使用AJTCL的系統包括一個運行AJSCL的主機和一個瘦用戶端設備。AJSCL給將要連接到它的瘦用戶端提供
AllJoyn路由功能，同時也為使用瘦用戶端的應用提供平台。就如之所說，瘦用戶端設備通常扮演感測器節點的角色，它向運
行在主機上的應用程式發送資訊。應用程式以某種方式處理這些資訊，並向感測器節點發送一些命令，使其應對當前環境。
　　考慮一種簡單但可能欠考慮的情況，一個壁掛式恆溫器控制著一個電爐，並在一個安卓設備上運行著一個控制應用。安
卓設備上運行AJSCL，而壁掛式恆溫器上運行著AJTCL。該系統可以用圖6來表示。
　　在本例中，一個需求是壁掛式恆溫器，其只能被安卓設備中對應的恆溫器控制程式所控制。
儘管在本例的需求中說明了恆溫器僅可被安卓設備控制，但需求也可以是恆溫器連接到某個路由節點，再由該路由節點連接
到應用程式。這意味著安卓應用程式應該與AllJoyn路由程式綁定在一起，而這個綁定在一起的路由程式和應用程式應該以一
個路由節點的身份提供給瘦用戶端使用。這種配置允許在AJTCL和路由節點/應用程式對中建立一種受信關係。
　　應用程式接著請求與他綁定的路由程式以一個眾所周知的命名方式向AJTCL發送一個「安靜的」廣播
（例如，com.company.BusNode<guid>）。路由程式接著準備響應那些以之前廣播的命名方式命名的安靜的（單播）的回復。
當瘦用戶端出現時，它應當在關聯的網路前綴（com.company.BusNode）上啟用發現過程，如圖7所示。
　　當路由節點收到一個對其之前「安靜地」廣播過的名字的明確的請求時，它將回應一個表明該名字是由此路由節點所廣
播的消息。接下來AJTCL會嘗試連接到這個響應的路由節點。過程如圖8所示。
　　這樣一來，一個邏輯上的AllJoyn總線就已經建立起來了，應用程式和瘦用戶端服務通過運行在安卓設備上的路由程式連
接起來。以在《Introduction to the AllJoyn Framework》一文中使用過的泡泡圖來表示該系統，這種配置看上去就像是
AllJoyn路由節點連接了伺服器程式和用戶端程式，如圖9所示。
　　此時，AJTCL已經連接到與應用程式綁定在一起的路由程式，但是應用程式和瘦用戶端互相都不知道對方的存在。一般在
此時，AJTCL便會請求一個眾所周知的總線名，並會在AllJoyn的感知下實例化一個服務。
如《Introduction to the AllJoyn Framework》一文所描述，瘦用戶端會使用瘦用戶端核心庫的API介面創建一個對話連接
埠並廣播一個眾所周知的名稱。這個名稱一般不會和路由節點廣播的名稱相同；它與瘦用戶端和應用間的用戶端/伺服器的關
係有關，而與路由節點—瘦用戶端間的關係無關。運行在安卓設備上的應用程式將會針對這個名稱運行發現服務，如圖10所示。
　　當運行在AJTCL上的服務被運行在安卓設備上的用戶端發現時，該用戶端會加入此服務創建的對話。
　　從這個角度來說，運行在安卓設備上的應用程式可以訪問到AJTCL的服務，而且可以是任何AllJoyn服務。它可能通報服務
發送的信號——在此例中，可能是包含當前溫度的週期信號。此應用可能構建一個用戶界面，允許用戶鍵入期望達到的溫度，
並將此溫度使用如《Introduction to the AllJoyn Framework》一文所描述的AllJoyn遠端方法發送給AJTCL。一旦收到一個
呼叫方法，運行在AJTCL上的服務程式便會將請求轉發到電爐以設置理想溫度。
在瘦用戶端上使用的API和在AJSCL或服務程式上使用的API有很大的不同；儘管在兩種情況下，傳輸協定是完全一樣的，但對於
其中一方而言，另一方元件的性狀是不可見的。從這方面而言，AllJoyn是獨一無二的，而之前框圖中的各個泡泡，包括瘦用戶
端，從其目的或行為來看都是沒有區別的。

5.2 一個基於瘦用戶端庫的無線感測器網路
　　本例描述了一個非常基礎的家庭管理系統。該系統的無線接入點是一個運行OpenWRT的路由器，在其上預裝了一個允許來自
瘦用戶端的非受信連接的AllJoyn路由程式。這樣AJTCL用戶端便可以通過連接到該路由節點接入系統。網路中的瘦用戶端設備
可以是溫度感測器、運動檢測感測器、電燈開關、熱水器、電爐或空調。
　　如之前所言，本例中的數據融合功能由一個運行在通用型電腦上的應用程式實現並整合顯示。這並不是說在該網路中一定
要有一個通用型電腦——數據融合可以以其他方式實現；但是，在本例中的通用型電腦可以幫助我們理解AJSCL和瘦用戶端設備
是如何互動的。整合顯示可以使用壁掛式的顯示設備，或者簡單地在家中的某個PC上顯示。舉例而言，該顯示程式可以提供不
同房間的溫控器和溫度計的用戶介面；或者是虛擬的電燈開關，或運動檢測儀。數據融合算法程式將會決定什麼時候開燈，如
何控制電爐或空調的開關，或者如何最有效地控制熱水器的溫度。
　　要考慮的第一個元件是如圖12所示的OpenWRT路由器。該路由器管控一個獨立的AllJoyn路由域（在圖中以黑色粗水平線表
示，代表一個AllJoyn分佈式軟體總線的一個總線段）。
　　在該路由器所在的總線段中有一個AllJoyn服務程式，該程式使用AllJoyn架構提供了一種方式來配置路由器和預裝在路由
器上的路由程式。此外，圖中的一些空槽表示與AJTCL之間的非受信連接。由於這是一個通用AllJoyn路由器，對應的軟體總線
可以被擴展到其他的總線段以形成如圖1所示的分佈式總線。
　　如之前的章節所述，AJTCL設備將會運行發現過程以搜尋他們能連接到的路由節點。儘管在此描述的是一個非受信關係，運
行在OpenWRT路由器上的AllJoyn路由程式可以配置成「安靜地」廣播一個通用的名稱，如org.alljoyn.BusNode，暗示該路由節
點是一個AllJoyn分佈式總線上的一個節點，並意圖接管瘦用戶端。
　　代表感測器節點的AJTL設備通過登錄過程接入無線網路。在此過程中，他們以所謂的友好的名稱（即有意義的名稱）來命
名。舉例說，一個電燈控制器（開-關-調光控制器）可能被命名為「廚房」，而另一個可能被命名為「臥室」。對應的瘦用戶
端節點開始探索他們連接的路由節點（可能是org.alljoyn.BusNode），並嘗試連接。儘管上圖中的很多「槽」假定是非受信的
，瘦用戶端設備還是可以如圖13所示那樣加入網路。
　　一旦瘦用戶端程式連接到了OpenWRT路由器所在的總線段，它們就會開始廣播其對應的服務。如之前所假設的，這是一個家
庭控制系統，連接到路由器提供的無線網路。該設備會嘗試發現服務，並在系統中尋找瘦用戶端庫提供的服務，如圖14所示。
一旦家庭控制系統發現了某個瘦用戶端廣播的服務，它將嘗試與該瘦用戶端開始對話。其結果是路由器所在的總線段和家庭控制
系統融合成一個虛擬分佈式總線。
　　當這個融合的總線完全形成時，連接到總線的設備就成了一個標準的AllJoyn用戶端或伺服器。布式設備上的其他部件不會
知道這些ALlJoyn瘦用戶端感測器/執行器實際上是嵌入式設備，並通過TCP協定連接到AllJoyn路由節點，也不會知道家庭控制程
式以Java編寫並運行在一個運行安卓系統的通用型電腦上。這些用戶端和伺服器僅僅只是執行遠端呼叫方法和收發信號。
　　讀者現在可以瞭解運行在數據融合節點上的算法。舉例說明。在分佈式總線上傳輸的一個重要的AllJoyn信號可能是與
CARBON-MONOXIDE-DETECTED（檢測到一氧化碳）對應的某種東西。這個信號將被家庭控制系統（數據融合中心）接收。家庭控制
系統收到這個信號以後，可能會發送一個遠端方法給某個執行節點，使其TURN-FAN_ON（打開風扇），它也可能發送一個遠端方
法給另一個執行節點，使其SOUND-ALARM（播放報警音），還可能發送短信給屋主，告訴他家中出現過量的一氧化碳。
　　更為常見的情形下，家庭控制系統還可能向電爐發送一個遠端方法，使其在房間中沒人的情況下（通過運動檢測裝置的檢測
結果和日程表判斷）降低房間溫度。房屋控制單元可能向熱水器發送一個消息，使其在工作時間和午夜降低水溫，而在午夜洗碗
器需要工作時向其發送一個呼叫方法使其提高水溫，這樣一來便可以在電費最低的時候工作。
　　所有這些家庭控制系統響應的信號和發送的呼叫方法都與信號發送/接受設備的類型完全無關。

6 總結
　　AllJoyn是一個綜合的系統，其設計目的是為了在成分各異的系統上開發分佈式應用程式。AJTCL使嵌入式設備可以加入
AllJoyn分佈式軟體總線，並能以忽略細節的方式在系統中存在，而這一點正是開發人員所頭疼的。這個成果可以讓應用開發者專
注於應用程式的內容，而不必考慮太多底層的、嵌入式系統網路方面的事情。
　　AllJoyn系統可以以一個整體共同工作，而不像點對點網路，不同節點間固有的不匹配會造成很多問題。我們相信，與在其他
平台上開發的應用相比，AllJoyn系統可以以更簡單的方式構建包含嵌入式設備的更為強大的分佈式應用。

瞭解更多
　　想要瞭解更多關於如何在開發中使用AllJoyn的資訊，請在AllSeen聯盟的網站上瀏覽並下載相關文檔：（www.allseenalliance.org）
　　　　介紹型說明書——描述了ALlJoyn技術和相關概念。
　　　　開髮型說明說——介紹了如何構建環境，並提供了對於特殊問題的解決方案，包括代碼片段的註釋。
　　　　API參考——提供了在所有支援的編程語言中使用AllJoyn源代碼編寫應用程式的相關細節。
　　　　下載——軟體開發包（SDK，Software Development Kits），提供了相關資源用於幫助用戶編譯、修改、測試和執行某個項目。

 
============================================================
## alljoyn_pi      
ref: https://gist.github.com/germanviscuso/30cfa7dfb041c12e6ba3#file-alljoyn_pi

INDEX
- BUILD IT YOURSELF
- BUILD THE AUDIO SERVICE
- BUILDING FOR ANDROID
- INSTALL WITHOUT BUILDING
 
### BUILD IT YOURSELF
make sure you have installed the latest Raspbian OS
similar instructions for Ubuntu are available here: https://allseenalliance.org/docs-and-downloads/documentation/configuring-build-environment-linux-platform
``` 
sudo apt-get install build-essential
sudo apt-get install maven
sudo apt-get install scons
sudo apt-get install git
sudo apt-get install curl
sudo apt-get install openssl
sudo apt-get install libssl-dev
sudo apt-get install libjson0
sudo apt-get install libjson0-dev

mkdir ~/bin
echo "export PATH=$PATH:~/bin" >> ~/.bashrc
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
source ~/.bashrc
mkdir -p ~/WORKING_DIRECTORY/alljoyn
cd ~/WORKING_DIRECTORY/alljoyn
git config --global user.name "YOUR_NAME_HERE"
git config --global user.email "YOUR_EMAIL_HERE"
repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest
repo sync
export AJ_ROOT=$(pwd)
sudo ln -s /usr/bin/g++ /usr/bin/arm-angstrom-linux-gnueabi-g++
sudo ln -s /usr/bin/gcc /usr/bin/arm-angstrom-linux-gnueabi-gcc
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn
scons OS=linux CPU=arm WS=off OE_BASE=/usr BINDINGS=cpp,c,java,js,objc,unity #please check the IMPORTANT comments below before running
sudo ln -sf ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/build/linux/arm/debug/dist/cpp/lib/liballjoyn.so /lib/arm-linux-gnueabihf/liballjoyn.so
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/build/linux/arm/debug/dist/cpp/bin
ldd alljoyn-daemon #daemon not available in latest versions of alljoyn, use BR=on with scons for embedded daemon
./alljoyn-daemon --version
``` 
After executing alljoyn-daemon --version, you should see something like the following:
``` 
AllJoyn Message Bus Daemon version: v0.0.1
Copyright (c) 2009-2014 AllSeen Alliance.
 
Build: AllJoyn Library v0.0.1 (Built Fri Aug 22 05:36:57 UTC 2014 by pi - Git: alljoyn branch: '(no branch)' tag: 'v14.06' (+146 changes) commit ref: d611c623c14fb4d404253f39a4641bee518708b9)
``` 
IMPORTANT:
In the line:
```
scons OS=linux CPU=arm WS=off OE_BASE=/usr BINDINGS=cpp,c,java,js,objc,unity
``` 
the BINDINGS determine which platforms you build for (options are cpp, c, objc, java js and unity).
 
CPP, C: For running the deamon you'll only need to build for cpp but maybe you also want the other platforms.
 
JAVA: don't use OpenJDK, set Java to oracle-java7-jdk as explained below:
```
sudo apt-get install oracle-java7-jdk
export JAVA_HOME="/usr/lib/jvm/jdk-7-oracle-armhf"
echo "export PATH=$PATH:$JAVA_HOME/bin" >> ~/.bashrc
```
JS: If you also want to compile for js you need to add js to the bindings but you'll have to download xulrunner from here:
http://ftp.mozilla.org/pub/mozilla.org/xulrunner/releases/1.9.2/sdk/xulrunner-1.9.2.en-US.mac-i386.sdk.tar.bz2
and set the GECKO_HOME variable to point to that uncompressed directory (only the headers are used).
 
UNITY: to compile for Unity you'll have to install the Mono runtime and gcms:
```
sudo apt-get install mono-runtime
sudo apt-get install mono-gmcs
```
GTEST: If you want to build all the unit tests please follow the section googletest in this document:
https://allseenalliance.org/sites/default/files/resources/config_build_environment_linux.pdf
and export GTEST_DIR with your path to the uncompressed file
 
BULLSEYE: References to missing variable BULLSEYE_BIN can be safely ignored. 
Bullseye is code coverage analysis tool used by the alljoyn team but unfortunately it's not free or open source so I couldn't download it: http://www.bullseye.com
 
SERVICES: you can specify which alljoyn services to build as a scons parameter ( eg. SERVICES=about,audio )
 
Thanks to Mike Young whose initial setup description helped create this updated guide:
http://wildernessvoice.com/2014/07/building-allseen-alliances-alljoyn-core-on-raspberry-pi/
 
### BUILD THE AUDIO SERVICE
-----------------------
Once you're all set up with the previous section you can also build AllJoyn audio service (enables audio streaming):
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/services/audio
scons OS=linux CPU=arm WS=off SERVICES=about,audio BUILD_SERVICES_SAMPLES=off BINDINGS=core,cpp OE_BASE=/usr
If you get a compilation error in the AudioMixerThread method (in file src/posix/ALSADevice.cc) locate the line with the error and remove the 3rd parameter (false) in the source code 
(leave the first 2 parameters only). 
 
### BUILDING FOR ANDROID
--------------------
Please follow the instructions here:
https://allseenalliance.org/developers/develop/building/android/build-source
and apply this patch if you need Android 5 support:
https://jira.allseenalliance.org/browse/ASACORE-1208
 
### INSTALL WITHOUT BUILDING
------------------------
 
This is how you install the js version of AllJoyn without building it yourself (thx to oskarhane http://oskarhane.com/raspberry-pi-install-node-js-and-npm/ for the original instructions):
```bash 
#!/bin/bash
#Make a new dir where you'll put the binary
sudo mkdir /opt/node
#Get it
wget http://nodejs.org/dist/v0.10.28/node-v0.10.28-linux-arm-pi.tar.gz
#unpack
tar xvzf node-v0.10.28-linux-arm-pi.tar.gz
#Copy to the dir you made as the first step
sudo cp -r node-v0.10.28-linux-arm-pi/* /opt/node
#Add node to your path so you can call it with just "node"
cd ~
nano .bashrc
#Add these lines to the file you opened
PATH=$PATH:/opt/node/bin
export PATH
#Save and exit
#Install npm package of AllJoyn contributed by octoblu https://github.com/octoblu/alljoyn https://www.youtube.com/watch?v=OpjVzKeLpEQ
npm install -g alljoyn
#Warning: only discovery, messaging and notifications supported as of this writing
Important:
If node is not found even after adding it to the path maybe you're sudoing and the environment variables are not being passed. Try adding the path /opt/node/bin to the /etc/sudoers file


============================================================
##AllJoyn Bundled Daemon 使用方式研究     
ref: http://ziliao1.com/Article/Show/0F1310F4ACE5C51886A0D8A4590F625A.html
關於AllJoyn不多做介紹，請看官網：www.alljoyn.org/
 
0. 問題來源：
應用程式要使用AllJoyn庫，就必須啟動deamon。
目前有兩種方式：
使用standalone形式，單獨啟動alljoyn-daemon進程。
使用bundled daemon形式，應用程式在連接AllJoyn時自己啟動該deamon。
AllJoyn的開發者解釋如下：https://www.alljoyn.org/forums/developers/building-embedded-linux-system
The decision to use standalone or bundled daemon is made runtime but there is also an additional component that specifies whether an AllJoyn library supports bundled daemon at all. 
This the BD variable that we use when we build AllJoyn using scons.
More specifically, the check to choose which daemon is always made in the same manner irrespective of whether we have a standalone daemon or bundled daemon. 
The only thing BD signifies during build is whether the library will actually include code to run bundled daemon.
 An AllJoyn application will always see is there is a standalone daemon running. 
 If yes it will connect to that daemon else it will try and use the bundled daemon which may or may not be a part of the library depending on whether you said BD=on or off.
 
bundled daemon形式不需要單獨啟動進程，比較方便。因此就來研究如何使用該種方式。
1. 從入口看起:
```
BusAttachment::Connect()  {  
    #ifdef _WIN32      
    const char* connectArgs = "tcp:addr=127.0.0.1,port=9956";  
    #else      
    const char* connectArgs = "unix:abstract=alljoyn";  
    #endif      
    return Connect(connectArgs);  
}
```
很明顯，針對windows使用tcp transport，其他平台使用&ldquo;unix:abstract=alljoyn&ldquo;transport。
然後調用內部函數BusAttachment::Connect(const char* connectSpec)進行連接。
 
2. BusAttachment::Connect(const char* connectSpec)函數，重點如下：
```
    ...   this->connectSpec = connectSpec;          
    status = TryConnect(connectSpec);          
    /*           * Try using the null transport to connect to a bundled daemon if there is one           */          
    if (status != ER_OK && !isDaemon) { 
        printf("TryConnect() failed.\n");
        qcc::String bundledConnectSpec = "null:";              
        if (bundledConnectSpec != connectSpec) { 
            status = TryConnect(bundledConnectSpec.c_str());                  
            if (ER_OK == status) {                      
                this->connectSpec = bundledConnectSpec;     
            }              
        }          
    }  ...
```    
首先嘗試連接指定的"unix:abstract=alljoyn";
如果連接失敗就嘗試連接名為&rdquo;null:&rdquo;的transport（對應的類是NullTransport ）------該transport 即使用bundled daemon 
 
3. 再看BusAttachment::TryConnect(const char* connectSpec)函數，重點如下：
```
    ...  /* Get or create transport for connection */      
    Transport* trans = busInternal->transportList.GetTransport(connectSpec);      
    if (trans) {          
        SessionOpts emptyOpts;          
        status = trans->Connect(connectSpec, emptyOpts, tempEp);           
        ...       
    }  ...
``    
從busInternal中獲取指定的transport，再進行連接。
那麼busInternal是如何存儲transport的呢？
 
4. 看busInternal的初始化過程：
```
BusAttachment::Internal::Internal(const char* appName, 
    BusAttachment& bus, TransportFactoryContainer& factories, 
    Router* router, bool allowRemoteMessages, 
    const char* listenAddresses, 
    uint32_t concurrency) : application(appName ? appName : "unknown"), 
    bus(bus), listenersLock(), 
    listeners(), m_ioDispatch("iodisp", 16), 
    transportList(bus, factories, &m_ioDispatch, concurrency),      
    keyStore(application), authManager(keyStore),      
    globalGuid(qcc::GUID128()), msgSerial(1),      
    router(router ? router : new ClientRouter),      
    localEndpoint(transportList.GetLocalTransport()->GetLocalEndpoint()),      
    allowRemoteMessages(allowRemoteMessages),      
    listenAddresses(listenAddresses ? listenAddresses : ""),      
    stopLock(), stopCount(0) {    
        ...  
    }
```    
可以看到，這裡是通過TransportFactoryContainer（一組transport factory）對像來初始化所支援的transport list。
 
5.
```
QStatus TransportList::Start(const String& transportSpecs)  {  
    ...      
    for (uint32_t i = 0; i < m_factories.Size(); ++i) {
        TransportFactoryBase* factory = m_factories.Get(i);                                     
        if (factory->GetType() == ttype && factory->IsDefault() == false) {                                             
            transportList.push_back(factory->Create(bus));                                          
        }                       
    }  
    ...  
}
```
可以看到，這裡根據每個transport factory來創建對應的transport，並添加到transportList.中。
所以問題的關鍵在於：TransportFactoryContainer是如何初始化的呢（由transport factory 來決定支援的transport list）？
 
6. 再回過頭來看BusAttachment的構造函數:
```
BusAttachment::BusAttachment(const char* applicationName, 
    bool allowRemoteMessages, 
    uint32_t concurrency) :      
    isStarted(false),      
    isStopping(false),      
    concurrency(concurrency),      
    busInternal(new Internal(applicationName, *this, clientTransportsContainer, NULL, allowRemoteMessages, NULL, concurrency)),      
    joinObj(this)  {  
        ...  
    }
``` 
原來是BusAttachment在構造對像時初始化了Internal對像， 參數TransportFactoryContainer就是clientTransportsContainer
 
7. 繼續跟蹤clientTransportsContainer：
```
/*   * Transport factory container for transports this bus attachment uses to communicate with the daemon.   */   
static class ClientTransportFactoryContainer : public TransportFactoryContainer {    
    public:      ClientTransportFactoryContainer() : transportInit(0) { }        
    void Init()      {          
        /*           * Registration of transport factories is a one time operation.           */          
        if (IncrementAndFetch(&transportInit) == 1) {              
            if (ClientTransport::IsAvailable()) {                  
                Add(new TransportFactory<ClientTransport>(ClientTransport::TransportName, true));              
            }              
            if (NullTransport::IsAvailable()) {                  
                Add(new TransportFactory<NullTransport>(NullTransport::TransportName, true));              
            }          
        } 
        else {              
            DecrementAndFetch(&transportInit);          
        }      
    }      
    private:      
        volatile int32_t transportInit;  
} clientTransportsContainer;
``` 
可以看到這是一個靜態類，在初始化時檢查是否支援NullTransport，如果支援就將它添加到TransportFactoryContainer中，在start時就會創建對應的transport 對像，供connect進行連接。
所以，現在問題的關鍵在於：NullTransport::IsAvailable()是否返回true。
 
8. 跟蹤NullTransport::IsAvailable()函數：
```
/** * The null transport is only available if the application has been linked with bundled daemon
    * support. Check if the null transport is available.       *       
    * @return  Returns true if the null transport is available.       */      
static bool IsAvailable() { 
    return daemonLauncher != NULL; 
}    
```
該函數通過檢查daemonLauncher 變數是否為空，來決定是否支援NullTransport。
其聲明如下：  
```
class NullTransport : public Transport {   
    private:  ...  
    static DaemonLauncher* daemonLauncher; /**< The daemon launcher if there is bundled daemon present */  
};
```
初始化：
```
DaemonLauncher* NullTransport::daemonLauncher;
```
可知：daemonLauncher變數默認為空，即默認是不支援NullTransport的。
 
9. 檢查整個工程代碼，發現為其賦值的代碼如下：
```
BundledDaemon::BundledDaemon() : transportsInitialized(false), stopping(false), ajBus(NULL), ajBusController(NULL)  {
    NullTransport::RegisterDaemonLauncher(this);  
}  
void NullTransport::RegisterDaemonLauncher(DaemonLauncher* launcher)  {      
    daemonLauncher = launcher;  
}
```
說明：只有在聲明BundledDaemon對象的情況下daemonLauncher才不為空，才能支援NullTransport（即Bundled Daemon 模式）。
 
10. 查看文件daemon/bundled/BundledDaemon.cc230行,發現已聲明BundledDaemon 的靜態對像
static BundledDaemon bundledDaemon;
這是不是意味著，只需要連接該文件就可以聲明BundledDaemon 對像， daemonLauncher才不為空，進而支援NullTransport（即Bundled Daemon 模式）？
 
以AllJoyn自帶的chat做實驗，位於：alljoyn-3.3.0-src/build/linux/x86-64/debug/dist/samples/chat
修改Makefile的連接選項，發現只需要按如下順序添加連接選項：
LIBS = -lalljoyn ../../lib/BundledDaemon.o -lajdaemon -lstdc++ -lcrypto -lpthread &ndash;lrt
程式就會自動啟用Bundled Daemon，而不需要手動啟動alljoyn-daemon進程
```
$ ./chat -s 
a  BusAttachment started. 
RegisterBusObject succeeded.     
0.063 ****** ERROR NETWORK external          Socket.cc:249                 | Connecting (sockfd = 15) to @alljoyn : 111 - Connection refused: ER_OS_ERROR     
0.063 ****** ERROR ALLJOYN external          posix/ClientTransport.cc:258  | ClientTransport(): socket Connect(15, @alljoyn) failed: ER_OS_ERROR  Using BundledDaemon  
AllJoyn Daemon GUID = 8216a0fc60832b5f50c2111527f89fc1 (2MWyW3hV)  StartListen: tcp:r4addr=0.0.0.0,r4port=0  StartListen: ice:  
Connect to &lsquo;null:&rsquo; succeeded-----------------------------已經連上NullTransport
```
最終結論：
應用程式如果想使用Bundled Daemon，只需要在連接選項中添加如下庫即可（不可改變連接庫順序）：
```
-lalljoyn ../../lib/BundledDaemon.o -lajdaemon
```

============================================================
## AllJoyn Control Panel服務框架1.0最佳實踐
轉自: AllJoyn Control Panel Service Framework 1.0 Best Practices 
1 AllJoyn Control Panel服務框架 
1.1 目的 
1.2 範圍 
1.3 參考文獻 
1.4 縮寫詞和術語 

2 最佳實踐 
2.1 控制器 
2.1.1 顯示多重 Control Panel 
2.1.2 響應Control Panel的變化 
2.1.3 異常處理 
2.2 受控者 
2.2.1 受控者Control Panel命名規範 
2.2.2 Control Panel結構和佈局 
2.2.3 受控者的本地化處理 

1 AllJoyn Control Panel服務框架 
AllJoyn Control Panel服務框架使 一個設備應用程式宣佈一個虛擬Control Panel和另一個領近設備應用程式發現和顯示 Control Panel 相互作用。 
這個服務框架適用於一對一交互在一個設備(受控者)和控制應用程式(控制器)之間。 

受控者應用程式可以使用服務定義一組展示控制的「部件」,包括這些部件每個控件的使用和在顯示控制器上如何佈局的說明。 
一個控制器應用程式可以使用服務發現附近的受控者,獲得他們的 Control Panel,使用提供的適配器層在特定於目標平台創建控制UI元素。 

1.1 目的 
本文檔提供了執行AllJoyn Control Panel服務框架的最佳實踐。 

1.2 範圍 
本文是為想充分利用本服務提供的功能的原始設備製造商和開發者們而寫。 

1.3 參考文獻 
以下參考文檔基於AllSeen聯盟網頁Docs/Downloads章節： 
■ AllJoyn框架輔導 
■ AllJoyn精簡客服端入門指導 

文檔支援 Control Panel服務框架上市的平台比如Android，Linux，Thin Client等。 
■ AllJoyn Control Panel服務框架1.0入門指南 
■ AllJoyn Control Panel服務框架1.0入使用指南 

1.4 縮寫詞和術語 
術語                  定義 
---------------------------------------------- 
AllJoyn Service       實現使用提供特殊功能的 
frameworks            AllJoyn框架的全貌集合。 
                      這些構建模組被設備和應用 
                      構建相互結合在一起。 
----------------------------------------------- 
Adapter               Control Panel服務框架層翻譯接收 
                      到的UI元素到Android的UI元素 
----------------------------------------------- 
AllJoyn device        支援AllJoyn框架，能連接到 
                      私人網路的設備 
----------------------------------------------- 
Control panel         允許用戶與設備交互的部件集合。 
                      一個Control Panel被受控者定義和發佈， 
                      被控制器發現和顯示。一個設備 
                      能有多個，能被定義在預語言基礎上。 
----------------------------------------------- 
Controllable device   一個代表（代理）受控者的客服端。 
----------------------------------------------- 
Controllee            一個AllJoyn應用程式，發佈 
                      Control Panel介面，所以其他AllJoyn 
                      設備可以控制它。 
----------------------------------------------- 
Controller            一個AllJoyn應用程式控制另一個 
                      發佈Control Panel介面的AllJoyn設備 
----------------------------------------------- 
Widget                一個UI元素在Control Panel代表一個介面。 
                      它生動地表現一個用戶執行功能或使用內容。 
----------------------------------------------- 

2 最佳實踐 
本章節描述基於此服務框架功能的處理情景。 

2.1 控制器 
2.1.1 顯示多重 Control Panel 
有時， 一個受控者可能有復合 Control Panel。一些例子如下： 
■ 一些 Control Panel可能為整體設備的不同「單位」； 
■ 用戶的每天 Control Panel和技術員或修復個人的單獨的 Control Panel。 
因此,控制器應用程式應該提供用戶選擇的選項 
不僅可以與附近的受控者交互,也 Control Panel上他們想要與特定的受控者。 

2.1.2 反應 Control Panel的變化 
受控者提供的 Control Panel可能根據用戶交互,設備狀態,和其他因素改變。 
控制器有一個註冊在 Control Panel的適當的監聽器是很重要的, 
這樣它將被告知這些變化並相應更新 Control Panel的用戶界面。 

2.1.3 異常處理 
當發生錯誤,控制器試圖從受控者恢復部件,適配器將拋出一個異常, 
這樣應用程式可以處理錯誤並決定如何向用戶顯示錯誤。 
這些拋出的錯誤是有原因的,在不同的狀態,他們不應該被忽略。 

2.2 受控端 
2.2.1 受控端Control Panel命名規範 
當設計受控端發佈的Control Panel時,必須遵循一定的命名約定為單位的名稱和各個部件的名稱。 
此外,每個Control Panel的單元和小部件名稱必須是唯一的。 
單位名稱和部件名稱使用AllJoyn BusObject路徑的一部分, Control Panel服務框架會利用。 
命名約定如下: 
■只包含ASCII字元」[A-Z][a-z][0-9]_」 
■不能空字串 

2.2.2 Control Panel結構和佈局 
重要的是要記住,受控者發佈的Control Panel經常在一個移動設備的有限螢幕大小和可用螢幕空間上顯示。 
因此,Control Panel服務框架的容器部件應使用有效地組織和安排其他小部件的Control Panel。 

2.2.3 受控者的本地化處理 
開發人員創建一個受控者應用程式不應該依賴或計劃有控制器應用程式執行本地化(翻譯或口譯等)的內容。 
例如,如果一個受控者提供語言支援英文和西班牙的Control Panel, 
然後字串包含在不同的部件必須有正確的和完整的language-appropriate字串可用以便控制器應用程式可以簡單地顯示小部件。 
一個方法,比如有一個受控者小部件定義包含一個數字或代碼,然後用來查找或控制器轉換為一個特定於語言的字串是不可接受的。

============================================================
## AllJoyn on Raspberry Pi (Raspbian) and Windows 10       
ref: http://blog.rajenki.com/2015/05/alljoyn-on-raspberry-pi-raspbian-and-windows-10/
After the announcement of Windows 10 including out-of-the-box support for AllJoyn, I decided to 
try and connect my Raspberry Pi Model B+ running Raspbian to a Windows 10 PC to see how this all
 pans out. If you』re not familiar with AllJoyn: AllJoyn is a system that allows devices to 
 advertise and share their abilities with other devices around them. The beauty of AllJoyn is 
 that it can be used over a bunch of different transports (Wi-Fi, Bluetooth, RF, etc.) and will 
allow for interoperability between devices that may initially have not been designed to work 
together. This of course piqued my interest, with my continuous efforts in home automation. 
This blog post will outline the steps needed to get AllJoyn on Raspberry Pi up and running, as 
the process is quite lengthy and the available resources on the web didn』t cover the full 
installation in my particular case.

First of all, here are the resources that I found on the web, which covered 90% of the process 
I'm about to describe. I'm writing my own post to cover the remaining 10% and hopefully clear 
up some of the things that weren』t particularly evident to me while reading these resources, so
 hopefully you won't have to go through the same process.

German Viscuso』s GitHub Gist outlining the installation process
Mike Young』s blog post which the GitHub Gist is based upon
Martin Calsyn』s blog post, filling in a bunch of the missing bits and pieces for me
Compiling AllJoyn on Raspberry Pi
I'm going to assume you already have Raspbian running on your Raspberry Pi and know how to get 
to a terminal interface. If not, there』s very good documentation on the official Raspberry Pi 
website on how to do so. Let』s get started by installing the necessary packages to compile AllJoyn:
```
sudo apt-get install build-essential
sudo apt-get install maven
sudo apt-get install scons
sudo apt-get install git
sudo apt-get install curl
sudo apt-get install openssl
sudo apt-get install libssl-dev
sudo apt-get install libjson0
sudo apt-get install libjson0-dev
sudo apt-get install libcap-dev
```
Note the last package, which is missing on the GitHub Gist, but is needed to prevent a 
"sys/capability.h: No such file or directory" error popping up during compilation.

Now that we have all the necessary packages, let's get the source from the AllSeen Alliance's Git repository:
```
mkdir ~/bin
echo "export PATH=$PATH:~/bin" >> ~/.bashrc
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
source ~/.bashrc
mkdir -p ~/WORKING_DIRECTORY/alljoyn
cd ~/WORKING_DIRECTORY/alljoyn
git config --global user.name "YOUR_NAME_HERE"
git config --global user.email "YOUR_EMAIL_HERE"
repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest
repo sync
export AJ_ROOT=$(pwd)
sudo ln -s /usr/bin/g++ /usr/bin/arm-angstrom-linux-gnueabi-g++
sudo ln -s /usr/bin/gcc /usr/bin/arm-angstrom-linux-gnueabi-gcc
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn
```
Note the "WORKING_DIRECTORY" path in here, which should be replaced by something that makes sense in your case. I used "repos" on my Raspberry Pi.

Next up is the actual compilation, which can take quite some time, which is probably an understatement. I got to sneak in a bunch of Destiny matches on Xbox One, so you should probably prepare a seperate activity before compiling. These are the particular flags I used to get the basics set up, but you can refer to the GitHub Gist for more information on additional flags that may apply to your situation:
```
scons OS=linux CPU=arm WS=off OE_BASE=/usr BR=on BINDINGS=cpp CROSS_COMPILE=/usr/bin/arm-linux-gnueabihf-
sudo ln -sf ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/build/linux/arm/debug/dist/cpp/lib/liballjoyn.so /lib/arm-linux-gnueabihf/liballjoyn.so
```
When the compilation is finally finished (hopefully without errors), it』s time to build the additional services. You can also do this in one go by specifying the SERVICES parameter in the previous scons command, but I prefer the separation as it makes tracking down errors a bit more manageable. Note that this will also take quite a bit of time (less than the previous one, but get that Xbox One ready just in case):
```
scons OS=linux CPU=arm WS=off SERVICES=about,notification,controlpanel,config,onboarding,sample_apps BINDINGS=core,cpp OE_BASE=/usr CROSS_COMPILE=/usr/bin/arm-linux-gnueabihf-
```
After all this, you should have a completely compiled AllJoyn implementation available on your Raspberry Pi! You can test things out by navigating to the following directory and executing the daemon with the –version parameter:
```
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/build/linux/arm/debug/dist/cpp/bin
ldd alljoyn-daemon
./alljoyn-daemon --version
```
Testing it all out
As I mentioned, I』m using a PC running Windows 10 as the other node to connect to AllJoyn on Raspberry Pi. On the Windows IoT GitHub, there』s a bunch of documentation about AllJoyn on Windows 10. Additionally, a few samples are available near the bottom of the page, one of which is the AllJoyn Explorer. We can use the AllJoyn Explorer app on Windows 10 to listen for any AllJoyn capable devices advertising on the network. Follow the instructions to install it and launch it on your Windows 10 PC.

With AllJoyn Explorer running, go back to the Raspberry Pi and execute the following commands:
```
cd ~/WORKING_DIRECTORY/alljoyn/core/alljoyn/build/linux/arm/debug/dist/cpp/bin/samples
./AboutService
If all goes well, you should see a device pop up in AllJoyn Explorer and you can drill down into the device to view its capabilities! Hope this post helps you get things going in a reasonable time frame without having to spend a lot of time researching errors and quirks. If you find anything missing in this guide, please let me know and I』ll update it accordingly!
```

============================================================
## AllJoyn on Ubuntu by Dexter 2015-07-30
ref: https://wiki.allseenalliance.org/develop/downloading_the_source

#### Downloading the Source
Download the source by using the repo tool (works on Linux and Mac) or by running individual git commands (works on all platforms).
Additionally, some platforms have additional details:
#### OpenWRT
Download Using Repo
##### Install Repo
Follow these instructions to download the repo tool.
Create Working Directory
```
mkdir /home/allseen
cd /home/allseen
```
##### Init Repo Client
```
repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest
```
To sync with the most recent tags (including bugfix releases) for a given release number, e.g. v14.06 or v14.12:
```
repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest -b RB14.12 -m versioned.xml
```
Or, if you are working on a future release, run this to pull the tip from the release branch, e.g. RB15.04
```
repo init -u https://git.allseenalliance.org/gerrit/devtools/manifest -b RB15.04
```
Note, you can safely ignore these 「errors」:
curl: (22) The requested URL returned error: 404
Server does not provide clone.bundle; ignoring.
Download the Source
```
repo sync
```
##### Download Using Git
Run these commands to download the source by using individual git commands
```
mkdir WORKING_DIRECTORY
cd WORKING_DIRECTORY
git clone https://git.allseenalliance.org/gerrit/core/alljoyn.git core/alljoyn
git clone https://git.allseenalliance.org/gerrit/core/ajtcl.git core/ajtcl
git clone https://git.allseenalliance.org/gerrit/services/base.git services/base
git clone https://git.allseenalliance.org/gerrit/services/base_tcl.git services/base_tcl
git clone https://git.allseenalliance.org/gerrit/data/datadriven_api.git data/datadriven_api
git clone https://git.allseenalliance.org/gerrit/devtools/codegen.git devtools/codegen
```
Run these commands to optionally sync to a specific revision, like v14.06 or v14.02
```
export VER=v14.06
git -c core/alljoyn checkout -b $VER $VER
git -c core/ajtcl checkout -b $VER $VER
git -c services/base checkout -b $VER $VER
git -c services/base_tcl checkout -b $VER $VER
** note on Windows, the commands look like this...
set VER="v14.06"
git -c core/alljoyn checkout -b %VER% %VER%
```

#### Building and Running
Below are very basic instructions for building and running some AllJoyn core and services. This assumes the source code is in $AJ_ROOT (see Downloading the Source for more info).
Linux
```
cd $AJ_ROOT/core/alljoyn
scons BINDINGS=cpp WS=off BR=off ICE=off SERVICES="about,notification,controlpanel,config,onboarding"

pushd build/linux/x86_64/debug/dist/
export LD_LIBRARY_PATH=`pwd`/cpp/lib:`pwd`/about/lib:`pwd`/notification/lib:`pwd`/controlpanel/lib:`pwd`/config/lib:`pwd`/services_common/lib:$LD_LIBRARY_PATH
pushd notification/bin

./ConsumerService # run this in one terminal to receive notifications, press enter once after launching ConsumerService
./ProducerBasic   # run this in another terminal to send notifications
```

SCons Options
```
WS=off - This turns off the whitespace checker. The whitespace checker is for developers to ensure that the code they write conforms to our coding standard is not necessary for customers to use.
BR=off - This disables the bundled AllJoynrouter functionality. If you intend to use a stand-alone AllJoynRouter, this should be set to off.Setting it to 「on」 will include the AllJoynRouter - note that the default is 「on」.
OS=linux - This is for building AllJoyn for desktop Linux (and is the default).
CPU=x86_64 - This is for building 64-bit binaries. If you are running on a 32-bit Linux machine then set this to 「x86」.
BINDINGS=cpp - This controls what to build. By specifying just "cpp" , only the AllJoynRouter, C++ libraries, and C++ sample/test code is built. 
   Other bindings that can be built are C, Java, and a browser plugin for a JavaScript binding.
SERVICES=「notification,controlpanel,config,onboarding」 - This specifies the Service Frameworks to build. 「About」 is always built by default and doesn't need to be specified. 
The standard service framework options include "notification, controlpanel, config, onboarding".
VARIANT=release - This builds AllJoyn in release mode. If there is a need to get verbose debug messages and run AllJoyn code in a debugger, then this can be set to 「debug」.
```
Linux (AC Server Sample)
Emulates an AC device.
Uses the About Feature to advertise the capabilities
Has a Control Panel that can be interacted with to change the temp, etc.
Produces Notifications
* Go into the sample_apps dir and build. Note, remove "base" for pre-14.06 source.
```bash
cd $AJ_ROOT/services/base/sample_apps
scons BINDINGS=cpp WS=off ALL=1

pushd build/linux/x86_64/debug/dist/
export LD_LIBRARY_PATH=`pwd`/cpp/lib:`pwd`/about/lib:`pwd`/notification/lib:`pwd`/controlpanel/lib:`pwd`/config/lib:`pwd`/services_common/lib:$LD_LIBRARY_PATH
pushd sample_apps/bin

# Run the AC Sample App
./ACServerSample
```

============================================================
# LINUX - set env
```bash
#!/bin/bash

echo "=== SET ALLJOYN ENV ==="
export AJ_ROOT=`pwd`     #/home/allseen
export TARGET_CPU=x86
export AJ_DIST=$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist

export LD_LIBRARY_PATH=$AJ_DIST/cpp/lib:$AJ_DIST/onboarding/lib:$AJ_DIST/notification/lib:$AJ_DIST/config/lib:$AJ_DIST/services_common/lib:$LD_LIBRARY_PATH

export CXXFLAGS="$CXXFLAGS \
        -I$AJ_DIST/cpp/inc \
        -I$AJ_DIST/about/inc \
        -I$AJ_DIST/services_common/inc \
        -I$AJ_DIST/notification/inc \
        -I$AJ_DIST/controlpanel/inc \
        -I$AJ_DIST/services_common/inc \
        -I$AJ_DIST/samples_common/inc"

export LDFLAGS="$LDFLAGS \
        -L$AJ_DIST/cpp/lib \
        -L$AJ_DIST/about/lib \
        -L$AJ_DIST/services_common/lib \
        -L$AJ_DIST/notification/lib \
        -L$AJ_DIST/controlpanel/lib"
echo "=== SET Alljoyn Service env ==="
echo "=== END ==="
```

/******************************************************************************/
LINUX - RUNNING ONBOARDING SAMPLE APPS
/******************************************************************************/
pwd = /home/allseen

Running OnboardingClient and OnboardingService Apps
Prerequisites
Open two terminal windows. In each, navigate to the AllJoyn? root dir, then:
```bash
AJ_ROOT=`pwd`

# <TARGET CPU> can be either x86_64, x86, or whatever value you set for "CPU=" when running SCons.
export TARGET_CPU=x86
export LD_LIBRARY_PATH=$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/cpp/lib: \
                       $AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/about/lib: \
                       $AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/onboarding/lib: \
                       $AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/notification/lib: \
                       $AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/config/lib: \
                       $AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/services_common/lib:$LD_LIBRARY_PATH
```
Run the OnboardingService Sample App
In one of the terminal windows, run OnboardingService:
```
$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/onboarding/bin/OnboardingService
```
NOTE: The OnboardingService sample app is just a shell implementation - no onboarding actually occurs!

Run the OnboardingClient Sample App
In the other terminal window, run OnboardingClient:
```
$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/onboarding/bin/OnboardingClient
```
NOTE: The OnboardingClient sample app uses hard-coded Onboarding values (for example, SSID, passcode, authtype).

============================================================
AllJoyn Bundled Daemon 使用方式研究
關於AllJoyn不多做介紹，請看官網：www.alljoyn.org/
0. 問題來源：
應用程式要使用AllJoyn庫，就必須啟動deamon。
目前有兩種方式：
. 使用standalone形式，單獨啟動alljoyn-daemon進程。
. 使用bundled daemon形式，應用程式在連接AllJoyn時自己啟動該deamon。
AllJoyn的開發者解釋如下：https://www.alljoyn.org/forums/developers/building-embedded-linux-system
The decision to use standalone or bundled daemon is made runtime but there is also an additional 
component that specifies whether an AllJoyn library supports bundled daemon at all. This the BD 
variable that we use when we build AllJoyn using scons.
 More specifically, the check to choose which daemon is always made in the same manner irrespective 
 of whether we have a standalone daemon or bundled daemon. The only thing BD signifies during build 
 is whether the library will actually include code to run bundled daemon.
 An AllJoyn application will always see is there is a standalone daemon running. If yes it will 
 connect to that daemon else it will try and use the bundled daemon which may or may not be a part 
 of the library depending on whether you said BD=on or off.

bundled daemon形式不需要單獨啟動進程，比較方便。因此就來研究如何使用該種方式。
1. 從入口看起:
```
BusAttachment::Connect()  {  
    #ifdef _WIN32      
    const char* connectArgs = "tcp:addr=127.0.0.1,port=9956";  
    #else      
    const char* connectArgs = "unix:abstract=alljoyn";  
    #endif      
    return Connect(connectArgs);  
}
```
很明顯，針對windows使用tcp transport，其他平台使用&ldquo;unix:abstract=alljoyn&ldquo;transport。
然後調用內部函數BusAttachment::Connect(const char* connectSpec)進行連接。
 
2. BusAttachment::Connect(const char* connectSpec)函數，重點如下：
```
...   
this->connectSpec = connectSpec;
status = TryConnect(connectSpec);          /** Try using the null transport to connect to a bundled daemon if there is one  */
if (status != ER_OK && !isDaemon) {
    printf("TryConnect() failed.\n");
    qcc::String bundledConnectSpec = "null:";
    if (bundledConnectSpec != connectSpec) {
        status = TryConnect(bundledConnectSpec.c_str());
        if (ER_OK == status) {
            this->connectSpec = bundledConnectSpec;
        }
    }
}
...
```
首先嘗試連接指定的"unix:abstract=alljoyn";
如果連接失敗就嘗試連接名為&rdquo;null:&rdquo;的transport（對應的類是NullTransport ）------該transport 即使用bundled daemon 
 
3. 再看BusAttachment::TryConnect(const char* connectSpec)函數，重點如下：
```
...  
/* Get or create transport for connection */      
Transport* trans = busInternal->transportList.GetTransport(connectSpec);      
if (trans) {          
    SessionOpts emptyOpts;          
    status = trans->Connect(connectSpec, emptyOpts, tempEp);           
    ...       
}  
...
```
從busInternal中獲取指定的transport，再進行連接。
那麼busInternal是如何存儲transport的呢？
 
4. 看busInternal的初始化過程：
```
BusAttachment::Internal::Internal(const char* appName, BusAttachment& bus, TransportFactoryContainer& factories, 
    Router* router, bool allowRemoteMessages, const char* listenAddresses, uint32_t concurrency) : 
    application(appName ? appName : "unknown"), bus(bus), listenersLock(), listeners(), m_ioDispatch("iodisp", 16),      
    transportList(bus, factories, &m_ioDispatch, concurrency), keyStore(application), authManager(keyStore),      
    globalGuid(qcc::GUID128()), msgSerial(1), router(router ? router : new ClientRouter),      
    localEndpoint(transportList.GetLocalTransport()->GetLocalEndpoint()), allowRemoteMessages(allowRemoteMessages), 
           listenAddresses(listenAddresses ? listenAddresses : ""),      stopLock(),      stopCount(0)  {    ...  }
```           
可以看到，這裡是通過TransportFactoryContainer（一組transport factory）對像來初始化所支援的transport list。
 
5.
```
QStatus TransportList::Start(const String& transportSpecs)  {  
    ...      
    for (uint32_t i = 0; i < m_factories.Size(); ++i) {
        TransportFactoryBase* factory = m_factories.Get(i);                                     
        if (factory->GetType() == ttype && factory->IsDefault() == false) {                                             
            transportList.push_back(factory->Create(bus));                                          
        }                       
    }  ...  
}
```
可以看到，這裡根據每個transport factory來創建對應的transport，並添加到transportList.中。
所以問題的關鍵在於：TransportFactoryContainer是如何初始化的呢（由transport factory 來決定支援的transport list）？
 
6. 再回過頭來看BusAttachment的構造函數:
```
BusAttachment::BusAttachment(const char* applicationName, bool allowRemoteMessages, uint32_t concurrency) : 
    isStarted(false), isStopping(false), concurrency(concurrency), 
    busInternal(new Internal(applicationName, *this, clientTransportsContainer, NULL, allowRemoteMessages, NULL, concurrency)), 
    joinObj(this)  {  ...  }
```    
原來是BusAttachment在構造對像時初始化了Internal對像， 參數TransportFactoryContainer就是clientTransportsContainer
 
7. 繼續跟蹤clientTransportsContainer：
```
/*   * Transport factory container for transports this bus attachment uses to communicate with the daemon.   */   
static class ClientTransportFactoryContainer : public TransportFactoryContainer {    
    public:      ClientTransportFactoryContainer() : transportInit(0) { }        
    void Init()      {          
        /*           * Registration of transport factories is a one time operation.           */
        if (IncrementAndFetch(&transportInit) == 1) {
            if (ClientTransport::IsAvailable()) {
                Add(new TransportFactory<ClientTransport>(ClientTransport::TransportName, true));
            }
            if (NullTransport::IsAvailable()) {
                Add(new TransportFactory<NullTransport>(NullTransport::TransportName, true));
            }
        } else {
            DecrementAndFetch(&transportInit);
        }
    }
private:      volatile int32_t transportInit;  
} clientTransportsContainer;
```
可以看到這是一個靜態類，在初始化時檢查是否支援NullTransport，如果支援就將它添加到TransportFactoryContainer中，在start時就會創建對應的transport 對像，供connect進行連接。
所以，現在問題的關鍵在於：NullTransport::IsAvailable()是否返回true。
 
8. 跟蹤NullTransport::IsAvailable()函數：
```
/**       * The null transport is only available if the application has been linked with bundled daemon       
          * support. Check if the null transport is available.       *       
          * @return  Returns true if the null transport is available.       */      
static bool IsAvailable() { 
    return daemonLauncher != NULL; 
}    
```
該函數通過檢查daemonLauncher 變數是否為空，來決定是否支援NullTransport。其聲明如下：  
```
class NullTransport : public Transport {   
    private:  ...  static DaemonLauncher* daemonLauncher; /**< The daemon launcher if there is bundled daemon present */  
};
```
初始化：
```
DaemonLauncher* NullTransport::daemonLauncher;
```
可知：daemonLauncher變數默認為空，即默認是不支援NullTransport的。
 
9. 檢查整個工程代碼，發現為其賦值的代碼如下：
```
BundledDaemon::BundledDaemon() : transportsInitialized(false), stopping(false), ajBus(NULL), ajBusController(NULL)  {      
    NullTransport::RegisterDaemonLauncher(this);  
}  
void NullTransport::RegisterDaemonLauncher(DaemonLauncher* launcher)  {      
    daemonLauncher = launcher;  
}
```
說明：只有在聲明BundledDaemon對象的情況下daemonLauncher才不為空，才能支援NullTransport（即Bundled Daemon 模式）。
 
10. 查看文件daemon/bundled/BundledDaemon.cc230行,發現已聲明BundledDaemon 的靜態對像
static BundledDaemon bundledDaemon;
這是不是意味著，只需要連接該文件就可以聲明BundledDaemon 對像， daemonLauncher才不為空，進而支援NullTransport（即Bundled Daemon 模式）？
 
以AllJoyn自帶的chat做實驗，位於：alljoyn-3.3.0-src/build/linux/x86-64/debug/dist/samples/chat
修改Makefile的連接選項，發現只需要按如下順序添加連接選項：
LIBS = -lalljoyn ../../lib/BundledDaemon.o -lajdaemon -lstdc++ -lcrypto -lpthread &ndash;lrt
程式就會自動啟用Bundled Daemon，而不需要手動啟動alljoyn-daemon進程
```
$ ./chat -s a  
BusAttachment started.  
RegisterBusObject succeeded.     
0.063 ****** ERROR NETWORK external          Socket.cc:249                 | Connecting (sockfd = 15) to @alljoyn : 111 - Connection refused: ER_OS_ERROR     0.063 ****** ERROR ALLJOYN external          posix/ClientTransport.cc:258  | ClientTransport(): socket Connect(15, @alljoyn) failed: ER_OS_ERROR  Using BundledDaemon  AllJoyn Daemon GUID = 8216a0fc60832b5f50c2111527f89fc1 (2MWyW3hV)  StartListen: tcp:r4addr=0.0.0.0,r4port=0  StartListen: ice:  Connect to &lsquo;null:&rsquo; succeeded-----------------------------已經連上NullTransport
``` 
最終結論：
應用程式如果想使用Bundled Daemon，只需要在連接選項中添加如下庫即可（不可改變連接庫順序）：
```
-lalljoyn ../../lib/BundledDaemon.o -lajdaemon
```

============================================================
## AllJoyn軟體計劃對D2D發展之影響分析  作者：工業技術研究院　發表於2013/10/1 下午 08:57:06
ref : http://www.fbblife.com.tw/47049068/article/content.aspx?ArticleID=1693
        
一、AllJoyn計畫企圖簡化D2D研發設計
   D2D（Device to Device）通訊指裝置與裝置間可不必透過核心網路，透過無線技術即可
   直接於短距離內進行裝置通訊，其目的在因應不斷擴展的社群網路、物聯網
   （Internet of Things，IoT）等鄰近服務(Proximity-based Services，ProSe)的趨勢。
   行動晶片大廠高通（Qualcomm）於2013年MWC宣佈擴展AllJoyn計畫，該計畫是由其子公司
   高通創新中心（Qualcomm Innovation Center，QuIC）所主導開發的行動軟體開放原始碼
   專案，透過短距離無線傳輸如Wi-Fi或Bluetooth等技術，使得不同作業系統及不同設備商
   的裝置更容易進行D2D直接通訊，提供更好的使用者經驗，最終目的在於提供完整鄰近服
   務，以實現物聯網的願景。   

AllJoyn主張平台中立（platform-neutral），也就是朝向獨立於特定作業系統、硬體、軟體
的設計，並且能運作在Microsoft Windows、 Linux、 Android、iOS、 OS X、 OpenWRT等既
有軟體平台，如此可使不同廠商生產的平板、手機、電視、筆電等裝置能在短距離內直接通
訊。    

二、AllJoyn開放軟體架構對 D2D的影響
AllJoyn開放軟體架構包含應用服務、核心及精簡裝置三大部分（見圖一所示）。其中
AllJoyn應用服務由第三方公司自行開發應用程式，AllJoyn核心是涵蓋不同程式語言互通、
搜尋、連結及安全機制的開放原始碼。而AllJoyn精簡裝置（AllJoyn Thin Client）則是包
含可支援的低階記憶體嵌入式裝置，其中包含一些共同的AllJoyn連接協定和基本功能
（feature set）。

AllJoyn主要目的在實現以下四種應用服務：
終端管理（Onboarding）：設備或簡易型智慧裝置可經由如智慧型手機應用軟體等媒介調配
置或VPN設定，以適用於使用者的個人網路。
通知（Notifications）：以標準資料傳送、控制方式讓裝置傳送與接收簡訊、影像、以及多
媒體的訊息通知。
影音串流（Audio Streaming）：執行可相互操作、開放、無線的影音串流協定，讓使用者在
任何廠商的產品上進行影音及視訊傳遞。
控制（Control）：開放裝置的控制介面並加以整合，包括各式不同的影音或媒體傳輸介面。
   
由上述說明可知，AllJoyn架構對於D2D通訊最大的影響在於使得各種應用只需使用簡易的硬
體裝置，並支援傳統無線通訊技術如Wi-Fi、Bluetooth等便能進行裝置間直接通訊。應用此
一開放軟體架構，最容易作為連結各種不同裝置並進行訊息交換的核心設備便是如智慧手機
或平板等手持裝置。
對於研發裝置通訊應用程式者而言，主要障礙在於必須同時考慮快速搜尋（discovery）、配
對（pairing）、訊息路由傳遞（message routing）及安全機制（security）等複雜的通訊
設計，這對於不具通訊背景的應用程式設計者是一大挑戰；但是透過AllJoyn的開放軟體底層
架構，軟體研發人員只需專注於遊戲軟體等應用程式（apps）的上層軟體端
（upper layer software）開發，而不用花費心力在複雜的通訊技術設計。AllJoyn依據
Apache V2.0的開放原始碼授權規範，最新的SDK 3.3.0原始碼已經可以在官方網路下載取得。   
在可能的應用上，AllJoyn的應用情境可能是和鄰近的好友分享手機上的影音檔案及遊戲，或
是回到家中用平板控制家中電視機、DVD錄影機、數位相框或遊戲機等家電；亦或是提供使用
者即時的鄰近服務，例如轉發優惠券給週遭的親友或傳送電子名片給客戶。

三、IEK View
（一）AllJoyn軟體計畫有機會加速裝置間互通及互聯
目前物聯網的應用主要還是以局部小規模網路為主，像是一般的家庭、車隊、醫院等的連網
系統，仍未見在終端消費設備的大規模應用。其主因在於終端裝置無法透過共同的作業系統
及程式語言來進行搜尋與通訊，而AllJoyn軟體計畫企圖降低研發門檻與架構，或許有機會加
速裝置間互通及互聯。
（二）D2D通訊技術標準的競爭將愈趨激烈
高通在應用處理器與無線通訊領域一直扮演領導角色，其在國際標準組織3GPP中積極推動基
於D2D通訊及鄰近服務的LTE Direct無線通訊技術，加上AllJoyn軟體計畫的擴展，可以看出
高通計畫整合軟硬體能量而成為物聯網完整解決方案供應商的規劃佈局。
不過，其它競爭者如英特爾（Intel）及博通（Broadcom）等晶片廠商亦提出不同D2D解決方
案，以英特爾為例，其晶片開發策略是透過Wi-Fi Direct方式進行裝置通訊，與高通的
LTE Direct路線不同，兩者互為競爭關係。因此，未來除了D2D通訊技術標準競爭外，軟體相
容亦將是重要競爭重點。


============================================================
## [技術相關] 借助 AllJoyn 和 Kii 讓智慧設備連繫起來  
ref: http://bbs.blueidea.com/thread-3115973-1-1.html
AllJoyn 開源軟體讓你的物聯網項目繞開底層網路協定和硬體。
作為 AllSeen Alliance 成員，我們對 AllJoyn 的物聯網項目框架非常感興趣。AllJoyn 使
用面向對象的方式，將各種傳輸更加點對點化從而降低開發的複雜度。其核心是使用 C++ 編
寫，提供多語言捆綁（如Java、JavaScript、C＃、ObjC），並支援跨作業系統和晶片組開發。

以下是（在 nodejs ）使用 JavaScript 借助 AllJoyn 快速實現資訊交流。這裡也包括如何
通過在 Kii 上記錄所接收的消息並用於後續處理從而讓項目啟用雲計算。本教程中，我們將
發送文本消息，但是 Kii 可以使用更豐富的數據，例如音樂、照片、視頻等。你可以借助雲
存儲和分析發送歌曲給智慧音箱或發送照片給智慧電視。

AllJoyn 框架總覽 
在講解代碼前，你需要瞭解一些 AllJoyn 的基礎知識。一個 AllJoyn 會話中的所有節點
（peer）都必須通過一個（相對較底層的）總線（bus）來「交流」，可以把它看成是用於傳
輸所有 AllJoyn 消息的高速公路。首先，創建一個總線附件並將你的 App 連接到總線上。
通過一個總線節點可以參與 AllJoyn 會話中，但它必須通過一個具體的介面（interface）
來完成。該介面是在總線上被創建的，其目的是處理共享對像和發送到對象的信號（signal）
的。在我們的例子中，節點將在總線中共享一個聊天對象且發送給它的信號將被作為消息中
繼到其它節點。

接下來，你必須決定你的 App 是否加入並使用現有的伺服器或公告一個伺服器給其他節點加
入。假設你要公告一個伺服器，給它起一個方便識別的名稱。其他節點將嘗試使用這個名稱
找到你的伺服器。然後，綁定一個連接埠（例如：27）從而在總線上創建一個會話
（session）。
步驟如下：
創建一個 BusAttachment 並連接到 AllJoyn 框架從而與其他 AllJoyn App 通訊在總線
（Bus）中創建一個介面（Interface）並定義將要處理的信號（Signal）創建一個 
BusObject 並與介面配對（啟動總線後）定義一個 SignalHandler 用於發送信號到 
BusObject使用總線（Bus）註冊 BusObject 並連接如果公告伺服器 :
選擇一個唯一的標識符，創建一個唯一的名稱創建一個其他 App 可以進入的會話
（Session）通過公告該伺服器名稱告訴其他 App
7. 如果加入伺服器：
通過一個名稱前綴查找附近其他 App，在找到一個伺服器名稱後，定義一個 
BusListener 從而能夠加入到一個會話中加入到一個已找到的會話
8. 在你的群組中與其他 App 通信
不必驚慌！我們將在下文中遍歷所有步驟所需的代碼。

安裝和編譯 AllJoyn
在使用 AllJoyn 前需要先安裝它。你可以下載源碼並編譯它（例如用於 Raspberry Pi），
但最簡單的方法是使用 npm 包（這裡要感謝 Octoblu！）並通過 JavaScript
（需要 nodejs）來測試框架。安裝過程如下：
安裝 npm 和 nodejs（備選安裝請點擊這裡）
安裝 AllJoyn npm 包
安裝 node-jquery-xhr npm 包（Kii js SDK 會用到）
下載 Kii js SDK 並將其放入到欲運行的腳本所在的目錄中
測試 Octublu 提供的 example-host.js 和 example-client.js 確保正常運行
i)     Mac 上的腳本位於 /opt/local/lib/node_modules/alljoyn（如果使用 -g 全局安裝
的話）並可以借助 node 命令運行

公告聊天伺服器
接下來看看我們的 nodejs 腳本。它可以在主機模式運行，以公告一個聊天伺服器讓其他節
點加入；也可以作為用戶端運行，根據主機在網路上公告的名稱查找伺服器，然後連接到該
伺服器。這裡可以有多個用戶端，但是主機只能有一個。主機和用戶端使用一個腳本的原因
是95%的代碼都可共享（見下文）。
一旦連接完成，所有節點（主機和用戶端）的行為都相同，即監聽和顯示發來的消息並可以
發送消息給其他節點。另外，將主機和用戶端所有發來的消息記錄在 Kii Cloud 用於後續
的分析。

Kii 的初始化和認證 
在 developer.kii.com 中創建一個 Kii App 後，寫下 App ID 和 Key 從而初始化 Kii：
Kii 初始化後，通過命令行嘗試使用節點名和密碼登錄。如果失敗了，則第一時間嘗試在
 Kii 伺服器上註冊：
需要注意，Kii API 在它的方法中提供了異步調用方法（使用 callbacks），這些方法控制
起來更加簡便，且在用戶登錄或註冊的同時腳本可以繼續運行。

設置 AllJoyn 總線
所有想使用 AllJoyn 參加會話的節點都需要做一些總線設置：
一個聊天對像被當作節點間的公共結構用於接收信號。信號處理器將信號解釋為消息。
在主機上公告伺服器
掛接到某一 AllJoyn 總線後，主機將公告伺服器名稱，以及一個會話、連接埠和連接埠監聽
回調：
主機將在連接埠 27 上有效地監聽用戶端連接，並為每個連接執行連接埠監聽回調。

在用戶端上查找服務
用戶端完成與主機相同的總線設置並遍歷該總線。與主機不同的是用戶端不公告伺服器而是
查找伺服器（使用相同的伺服器名）：
對於用戶端來說，總線監聽回調是關鍵，因為它定義了當一個服務名被找到後需要做些什麼
。下例中，當伺服器被找到時，我們告訴用戶端加入一個會話：

發送、接收以及記錄消息
主機和用戶端對發送和接收消息的處理方式是相同的。首先，一個共享的總線對像在總線上
被創建，然後每個節點訂閱通過一個信號處理器發送到該總線對象的信號。
為了發送消息，節點需要從標準輸入輸出（stdin）輸入並發送信號給共享的聊天對像：
為了接收消息，每個節點都有一個信號處理器，該信號處理器會將信號解釋為收到的消息。
將消息發送給控制台並將其記錄到 Kii 上：
請注意：為了儲存 Kii 數據，你需要在一個 App 級 Bucket 中創建一個 KiiObject 並同 
Key/Value 存儲一樣設置收到消息的所有資訊。之後，你可以節省 Kii 對象與異步調用，
並用 Kii Data Browser 在 developer.kii.com看到存儲的消息：
就是這樣。請記住，節點將消息解釋為文本從而顯示在螢幕上，但是這些交換的資訊可以擁
有更加複雜的結構、命令等等從而使用於所有類型的物聯網方案。甚至二進位格式的文件也
可以作為資訊交換並作為文件保存到 Kii 上。當然，除了可以將數據保存到 Kii Cloud 上
，你還可以通過其提供的強力查詢系統檢索數據。
使用 AllJoyn 十分容易，在此感謝 js npm 包。由於 Kii 提供的 JavaScript SDK 集成了
該包，你不但可以創建一個 AllJoyn 聊天服務還可以擁有雲記錄並在任何時候運行它。請記
住，節點可以是簡單的物聯網設備，將消息解釋為命令從而做一些有意義的事情或是交換更
豐富的數據例如流媒體音樂（更多關於這部分的資訊將在 Kii 的微博、微信、博客上發佈）。

主機和用戶端的完整源碼在這裡。使用方法很簡單：
```
 node peer.js [MODE] [YOUR_APP_ID] [YOUR_APP_KEY] [USERNAME] [PASSWORD]
```
MODE 可以是 「host」 或 「client」。先使用主機（host）模式運行，然後打開另一個程
式並使用用戶端（client）模式運行（由於嵌入的 AllJoyn 後台程式會使用相同的地址，所
以如果提示地址已經被使用的錯誤，請嘗試從網路上的另一台機器上運行）。請注意，你只
能運行一個主機，但是可以有任意多用戶端。參數 YOUR_APP_ID 和 YOUR_APP_KEY 可以在 
developer.kii.com 上創建 App 後獲得。你還可以隨意設置你的用戶名和密碼，如果憑據在
 Kii 上不存在，則將在第一時間被創建。我們建議每個運行的腳本使用不同的用戶名（否則
 ，無論用戶端還是主機都會在同一個用戶下記錄數據）。


============================================================
## SOME error message
```
2704.163 ****** ERROR ALLJOYN_OBJ JoinS-63      .../router/AllJoynObj.cc:1009 | SessionHost endpoint (org.alljoyn.About.sl.yviWz01tJ.x0) not found: ER_BUS_NO_ENDPOINT
2704.165 ****** ERROR SESSIONLESS lepDisp1_2    ...ter/SessionlessObj.cc:1031 | JoinSessionAsync to org.alljoyn.About.sl.yviWz01tJ.x0 failed: ER_ALLJOYN_JOINSESSION_REPLY_FAILED
2706.567 ****** ERROR ALLJOYN_OBJ JoinS-64      .../router/AllJoynObj.cc:1009 | SessionHost endpoint (org.alljoyn.About.sl.yPIl1ksDz.x0) not found: ER_BUS_NO_ENDPOINT
2706.569 ****** ERROR SESSIONLESS lepDisp1_2    ...ter/SessionlessObj.cc:1031 | JoinSessionAsync to org.alljoyn.About.sl.yPIl1ksDz.x1 failed: ER_ALLJOYN_JOINSESSION_REPLY_FAILED
 306.465 DEBUG    Notification lepDisp1_0       ...ionTransportConsumer.cc:77 | Received Message from producer.
End handling notification!!!
2712.970 ****** ERROR ALLJOYN_OBJ JoinS-68      .../router/AllJoynObj.cc:1009 | SessionHost endpoint (org.alljoyn.Notification.sl.yPIl1ksDz.x2) not found: ER_BUS_NO_ENDPOINT
2712.973 ****** ERROR SESSIONLESS lepDisp1_0    ...ter/SessionlessObj.cc:1031 | JoinSessionAsync to org.alljoyn.Notification.sl.yPIl1ksDz.x3 failed: ER_ALLJOYN_JOINSESSION_REPLY_FAILED
 309.893 DEBUG    Notification lepDisp1_0       ...ionTransportConsumer.cc:77 | Received Message from producer.
End handling notification!!!
 310.307 DEBUG    Notification lepDisp1_0       ...ionTransportConsumer.cc:77 | Received Message from producer.
End handling notification!!!
2714.382 ****** ERROR NETWORK iodisp1_0         common/os/posix/Socket.cc:463 | Shutdown socket (sockfd = 54): 107 - Transport endpoint is not connected: ER_OS_ERROR
```

============================================================
## [Alljoyn] Build from source - Linux
最近因為工作需要，所以在研究Alljoyn
至於Alljoyn是什麼，我這裡暫時就先不說明，有興趣的可以先辜狗找找資料
之後如果有空我會將看完官方的文件再寫一篇介紹與心得
這篇主要是先寫怎麼樣build code，由於官方的文件尚未完善，按照文件上build code可能會失敗
因此我修正了一些官方文件可能有問題的部分，以下是我的執行步驟：
OS: Ubuntu-14.04.3-desktop-i386
Reference:  http://allseenalliance.org/developers/develop/building/linux
Build tools and libs(need take off ia32-libs)
```
# sudo apt-get install build-essential libgtk2.0-dev libssl-dev xsltproc libxml2-dev
```
Build ia32-libs by Synaptic
1.點選「Ubuntu軟體中心」
2.搜尋「synaptic」
3.點選「安裝」
4.開啟synaptic
5.搜尋ia32-libs
6.勾選ia32-libs-multiarch
7.安裝
Install Python v2.6/2.7 (Python v3.0 is not compatible and will cause errors)
```
# sudo apt-get install python
```
Install SCons v2.0
```
# sudo apt-get install scons
```
OpenSSL
```
# sudo apt-get install libssl-dev
```
Download Using Git
```
mkdir WORKING_DIRECTORY
cd WORKING_DIRECTORY

git clone https://git.allseenalliance.org/gerrit/core/alljoyn.git core/alljoyn
git clone https://git.allseenalliance.org/gerrit/core/ajtcl.git core/ajtcl
git clone https://git.allseenalliance.org/gerrit/services/base.git services/base
git clone https://git.allseenalliance.org/gerrit/services/base_tcl.git services/base_tcl
git clone https://git.allseenalliance.org/gerrit/data/datadriven_api.git data/datadriven_api
git clone https://git.allseenalliance.org/gerrit/devtools/codegen.git devtools/codegen
```
The tree should look like below. Note, extra directories may exist.
```
root-source-dir/
  core/
      alljoyn/
      ajtcl/
  services/
      base/
      base_tcl/
```
Build Samples
```
cd <root dir of source>/core/alljoyn
scons BINDINGS=cpp WS=off BT=off ICE=off SERVICES="about,notification,controlpanel,config,onboarding,sample_apps"
```
Build AC Server Sample
The AC Server Sample app uses all of the base services to simulate an AC device.
Note, exclude the "base" dir for pre-14.06 source
```
cd $AJ_ROOT/services/base/sample_apps
scons BINDINGS=cpp WS=off ALL=1
```
Add the AllJoyn? framework to an existing app
Setup
```
  export AJ_ROOT=~/alljoyn

  # <TARGET CPU> can be either x86_64, x86, or whatever value you set for CPU= when running SCons.
  export AJ_DIST="$AJ_ROOT/core/alljoyn/build/linux/<TARGET CPU>/debug/dist"
```
Add header include directories
```
export CXXFLAGS="$CXXFLAGS \
    -I$AJ_DIST/cpp/inc \
    -I$AJ_DIST/about/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/notification/inc \
    -I$AJ_DIST/controlpanel/inc \
    -I$AJ_DIST/services_common/inc \
    -I$AJ_DIST/samples_common/inc"
```
Configure linker to include required libs
```
export LDFLAGS="$LDFLAGS \
    -L$AJ_DIST/cpp/lib \
    -L$AJ_DIST/about/lib \
    -L$AJ_DIST/services_common/lib \
    -L$AJ_DIST/notification/lib \
    -L$AJ_DIST/controlpanel/lib"
```    
Running The AC Server Sample
Prerequisites
Navigate to the AllJoyn root dir, then:
```
export AJ_ROOT=`pwd`

# Set $TARGET CPU to the "CPU=" value used when running scons, e.g. x86_64, x86.
export TARGET_CPU=x86

export LD_LIBRARY_PATH=$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/cpp/lib:$AJ_ROOT/core/alljoyn/build/linux/$TARGET_CPU/debug/dist/about/lib:$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/controlpanel/lib:$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/notification/lib:$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/services_common/lib:$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/config/lib:$LD_LIBRARY_PATH
```
Run the AC Server Sample App
```
$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/sample_apps/bin/ACServerSample --config-file=$AJ_ROOT/services/base/sample_apps/build/linux/$TARGET_CPU/debug/dist/sample_apps/bin/ACServerSample.conf
```

============================================================
## END