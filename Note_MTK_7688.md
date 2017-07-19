# NOTE MT7688 #
[TOC]

## reference docs ##
https://iamblue.gitbooks.io/linkit-smart-nodejs/content/zh-TW/intro/spec.html
login as: root
password: 0222709599

============================================================
## Linklt Smart 7688: MPU only. Powered by Media Tek MT7688. ##
- FEATURES
    - Single input single output(1T1R) Wi-Fi 802.11 b/g/n.
    - Pin-out for GPIO, I2C, I2S, SPI, UART, PWM and Ethernet Port.
    - 580 MHz MIPS CPU.
    - 32MB flash and 128MB DDR2 RAM.
    - USB host.
    - Micro SD slot.

- SPECIFICATION
```
Category			Feature				Specification
    - MPU			Chipset				MT7688AN
					Core				MIPS24KEc
					Clock speed			580MHz
					Working voltage		3.3V
    - PCB Size		Dimensions			55.7 x 26 mm
    - Memory		Flash				32MB
					RAM					128MB DDR2
    - Power Source	USB Power			5V (USB micro-B)
					VCC					3.3V (Pin Breakout)
    - GPIO			Pin Count			22 (MT7688AN)
					Voltage				3.3V
    - PWM			Pin Count			4 (MT7688AN)
					Voltage				3.3V
					Max. Resolution		7 bits (customizable)
					Maximum Frequency	100kHz@1-bit 
					@Resolution			50kHz@2-bit 
										25kHz@3-bit 
										12.5kHz@4-bit 
										6.25kHz@5-bit 
										3.125kHz@6-bit 
										1.5625kHz@7-bit (Standard mode)
										40MHz@1-bit 
										20MHz@2-bit 
										10MHz@3-bit 
										5MHz@4-bit 
										2.5MHz@5-bit 
										1.25Mhz@6-bit 
										625kHz@7-bit (Fast mode)
    - External Interrupts	Pin Count	22 (MT7688AN)
    - SPI			Set count			1 (MT7688AN)
					Pin numbers			P22, P23,P24 (Shared with on-board flash), P25
					Max. Speed			25 MHz
    - SPI Slave		Set count			1 (MT7688AN)
					Pin numbers			P28, P29, P30, P31
					Max. Speed			25 MHz
    - I2S			Set count			1 (MT7688AN)
					Pin numbers			P10, P11, P12, P13
    - I2C			Set count			1
					Pin numbers			P20, P21
					Speed				120K/400K
    - UART Lite		Set count			3 (MT7688AN)
					Pin numbers			P8, P9, P16, P17, P18, P19
					Max. Speed			0.5Mbps
    - USB Host		Set count			1 (MT7688AN)
					Pin numbers			P6, P7
					Speed				Micro-AB
    - Communication	Wi-Fi				1T1R 802.11 b/g/n (2.4G)
					Ethernet			1-port 10/100 FE PHY
					Pin numbers			P2, P3, P4, P5
    - User Storage	SD Card				Micro SD SDXC
```

============================================================
## Building a firmware ##
1)  install virtual machine if your host environment isn’t Ubuntu. 
    The disk space you should reserve is about 50GB 
    - Get the Ubuntu 14.04.3 LTS from http://www.ubuntu.com 
    - Install Virtual Box from http://virtualbox.org  
2)  Building a firmware requires installing prerequisite packages.  
```
$ sudo apt-get install git g++ libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip 
```
Ubuntu 64bit:
```
sudo apt-get install build-essential subversion libncurses5-dev zlib1g-dev gawk gcc-multilib flex git-core gettext libssl-dev
```
3)  Download the OpenWrt CC source code; it includes the full OpenWrt environment to build the firmware
```
$ git clone git://git.openwrt.org/15.05/openwrt.git 
$ git clone http://git.openwrt.org/15.05/openwrt.git 
```
4)  Create a configuration file feeds.conf by copying from the default template file feeds.conf.default  
```
$ cd openwrt 
$ cp feeds.conf.default feeds.conf 
```
5)  Add the LinkIt Smart 7688 feed to feeds.conf 
```
$ echo src-git linkit https://github.com/MediaTek-Labs/linkit-smart-7688-feed.git >> feeds.conf 
```
6)  Update the feed information for all packages needed to build firmware 
```
$ ./scripts/feeds update 
  ./scripts/feeds update -a
```
7)  Install all packages  
```
$ ./scripts/feeds install –a 
```
8)  Prepare the kernel configuration file for informing OpenWrt the intention to build a firmware for LinkIt Smart 7688   
```
$ make menuconfig 
```
9)   Select  options to set target profile per below: 
o  Target System: Ralink RT288x/RT3xxx 
o  Subtarget: MT7688 based boards 
o  Target Profile: LinkIt 7688 
10)  Save the options and exit (use the default config file name without changing it) 
11)  Start the firmware compilation process with make 
```
$ make V=99
```
12) After the compilation process completes, the resulting firmware file will be under bin/ramips/openwrt-ramips-mt7688-LinkIt7688-squashfs-sysupgrade.bin 
13)  Now you can use this file to do the firmware upgrade through Web UI or rename it to lks7688.img and use it to upgrade firmware through a USB drive. 

============================================================
## linkit-smart-feed ##
ref : https://github.com/MediaTek-Labs/linkit-smart-7688-feed
- Steps
In the Ubuntu system, open the Terminal application and type the following commands:
Install prerequisite packages for building the firmware:
```
$ sudo apt-get install git g++ make libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip wget python xz-utils
```
Download OpenWrt CC source codes:
```
$ git clone git://git.openwrt.org/15.05/openwrt.git
```
Prepare the default configuration file for feeds:
```
$ cd openwrt
$ cp feeds.conf.default feeds.conf
```
Add the LinkIt Smart 7688 feed:
```
$ echo src-git linkit https://github.com/MediaTek-Labs/linkit-smart-7688-feed.git >> feeds.conf
```
Update the feed information of all available packages for building the firmware:
```
$ ./scripts/feeds update
```
Install all packages:
```
$ ./scripts/feeds install -a
```
Prepare the kernel configuration to inform OpenWrt that we want to build an firmware for LinkIt Smart 7688:
```
$ make menuconfig
```
Select the options as below:
Target System: Ralink RT288x/RT3xxx
Subtarget: MT7688 based boards
Target Profile: LinkIt7688
Save and exit (use the deafult config file name without changing it)
Start the compilation process:
```
$ make V=99
```
After the build process completes, the resulted firmware file will be under bin/ramips/openwrt-ramips-mt7688-LinkIt7688-squashfs-sysupgrade.bin. Depending on the H/W resources of the host environment, the build process may take more than 2 hours.
You can use this file to do the firmware upgrade through the Web UI. Or rename it to lks7688.img for upgrading through a USB drive.

============================================================
## Building a bootloader ##
The LinkIt Smart 7688/7688 Duo development platform supports Makefile-based builds, which allows you to build bootloader with the make command.  
The instructions in this section apply for an Ubuntu Linux 14.04.3 environment. 
1)  Please refer to section 7.1, “Building a firmware” for preparing the environment for building bootloader.  
2)  Download the bootloader source codeby typing the following command: 
```
$ git clone https://github.com/MediaTek-Labs/linkit-smart-uboot.git  
```
3)  Change to the LinkIt Smart 7688 bootloader source code folder 
```
$ cd linkit-smart-uboot 
```
4)  Install the tool-chain needed for building bootloader, this tool-chain is provided in 32-bit executable 
$ sudo tar xjf buildroot-gcc342.tar.bz2 -C /opt/ 
5)  Install additional packages to execute the tool-chain in a 64-bit machine  
```
$ sudo dpkg --add-architecture i386 
$ sudo apt-get update 
$ sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 
```
6)   Start the bootloader compilation process
```
$ make 
```
7)  After the compilation process finishes, the resulting bootloader file is   uboot.bin 
8)  Now you can rename this file to lks7688.ldr and use it to upgrade bootloader through a USB drive. 

============================================================
## OpenWrt 建置 – 安裝 ##
https://wiki.openwrt.org/zh-tw/doc/howto/buildroot.exigence
OpenWrt Buildroot 偏好使用 toolchain 來建置OpenWrt。建議你使用一個 GNU/Linux Distribution，不論是獨立安裝的， 或是執行於虛擬環境的 (VMware 或 Qemu)上。

Cygwin 無法正常的運作，也不保證可以成功的建置於 ~BSD 或 MacOSX 系統上。 你可以試試，並回報你的結果。不要忘了先閱讀 問題排除.

- 先前準備
350 MB 的硬碟空間供下載原始碼
3-4 GB 的硬碟空間供OpenWrt的建置

- 程序
1. 不要使用 root帳號
2. 所有的命令必須在 <buildroot dir> 目錄底下執行, 如 ~/openwrt/trunk/ 
3. 不要在完整路徑名中有空白的資料夾下建置
安裝 subversion (short: svn), 來下載OpenWrt的原始碼較為便利，且安裝 build tools 來幫助編彙程序:
sudo apt-get update
sudo apt-get install subversion build-essential
subversion請參見 svn 和 subversion documentation (multiple languages)

- 建置工具請參見 make 和 build-essential
使用svn下載OpenWrt的原始碼
```
mkdir ~/openwrt
cd ~/openwrt
svn co svn://svn.openwrt.org/openwrt/trunk/
cd trunk
```
這會產生 'trunk'資料夾，為OpenWrt原始碼主要的資料夾。
以版本 R27988來說，全部有14,382個檔案，總大小約 150 MiB
包含OpenWrt Buildroot system.
請參照Downloading Sources.
使用feeds script下載並安裝 feeds。(選擇性)
```
./scripts/feeds update -a
./scripts/feeds install -a
```
版本 7367之後，trunk資料夾已包含 26,650 個檔案，總大小約 302 MiB (如需安裝個別套件: ./scripts/feeds install PACKAGENAME)
使用以下其中一個命令，可以檢查是否你的建置OpenWrt的環境中有遺漏的套件:
```
make defconfig
make prereq
make menuconfig
```
這會列出需要建置OpenWrt的系統中遺漏的套件。
使用 package management commands安裝遺漏的套件。參照以下的範例表。
執行 build 或 在Mac OS X 10.7 Lion建置OpenWrt
:!: 在設定並執行編譯後 (如 這裡所描述), trunk資料夾包含 244,451 個檔案，總大小為 3.2GiB!

============================================================
## OpenWrt 建置 – 使用方法 ##
from : https://wiki.openwrt.org/zh-tw/doc/howto/build

- 先前準備
Install OpenWrt Buildroot and its prerequisites on your OS.
- 程序
1. 不要使用 root帳號
2. 所有的命令必須在 <buildroot dir> 目錄底下執行, 如 ~/openwrt/trunk/
- 設定套件
開始編譯。這會自動編譯toolchain，編譯原始碼，封裝套件，最後產生可以刷新的映像擋。
開始進行 安裝OpenWrt

- 更新原始碼:
```
svn update
```
OpenWrt的原始碼很常更新。建議使用最新的原始碼。

- 更新feeds:
```
./scripts/feeds update -a
```
安裝下載的套件:
注意: 在 ./scripts/feeds中顯示的installing 表示 "讓這個套件可以在 make menuconfig中選擇"。而不是真的編譯和安裝套件。
安裝單一套件:
```
./scripts/feeds install <PACKAGENAME>
```
或安裝全部的套件:
```
./scripts/feeds install -a
```
- Image Configuration
開始OpenWrt Buildroot的 ncurses text-based 設定界面:
```
make menuconfig
```
就像Linux kernel 設定，每一個選項大致有三種，y, m, n 分別表示:
按 y 設定成 <*> 標籤 
這個套件將包含在映像檔裡
按 m 設定成 <M> 標籤 
這個套件會被編譯 (to be installed with opkg after Flashing OpenWrt) but the package will not be included in the firmware-image
按 n 設定成 < > 標籤 
這個套件不會被編譯
儲存設定後， ~/openwrt/trunk/.config 會依據你所選的設定產生。
編譯環境會提供OpenWrt的 'Backfire' 10.03.1 設定檔，如 for ar71xx.
上面這個選單可以讓你選擇目標的平台，你想使用的toolchain以及你想要包進映像檔的套件。
更新原始碼和feeds後再執行這個設定界面，以確保是最新的套件設定。

- Defconfig
選定好target後再執行defconfig
```
make defconfig
```
這會產生標準的設定，包含檢查相依性和建置的環境等。 會檢查相依性，是否有安裝遺漏的並再執行一次。

- 整體設定
Menuconfig 提供一個文字的選單介面，可以選擇要編譯成韌體的目標、套件和一些核心選項。
```
make menuconfig
```
會自動更新現存的設定和相依性來建置更新後的映像檔。
為了簡化強大的編譯環境來產生個別的OpenWrt映像檔，發展了'menuconfig'。透過menuconfig的幫助，可以解決客製化的設定需求。依照特定的目標平台，套件需求和核心模組。標準的設定流程修改的部分包含:
目標系統(Target system)
套件選擇(Package selection)
建置系統設定(Build system settings)
核心模組(Kernel modules)
目標系統的選擇可以依照你手上的設備選擇支援的平台，可以是通用或特定的設置。 選擇套件可以選'selecting all package'來選定所有的套件，但這或許在特定狀況下才可被實現。預設的套件已經足夠，或可以再選定個別的套件。要注意的是，某些套件的組合會導致建置中斷，所以要做些測試來達到預期的結果。也因此OpenWrt的開發者們只有維護最小的預設套件組合。不過feeds-script可以讓建置過程中的套件整合和維護簡單化。

最常用的三個選項:
< > 這個原始碼不會被處理
<M> 這個套件的原始碼會被編譯成二進制檔和一個opkg套件檔。這個套件檔會放在 /buildsystem/bla/bla/bla，但是ImageGenerator並不會把這個套件放到韌體的映像檔中!
<*> 這個套件會被放入韌體中 (在SqashFS 分割區)
在開始編譯前的最後一步，離開 'menuconfig' – 這包含儲存設定或載入已存在的版本和設定。
離開文字選單並選擇 save 來儲存設定。

核心設定
如果不想要標準的核心設定，你可以用:
make kernel_menuconfig
注意: make kernel_menuconfig 會修改核心設定的模版，清空 build_dir 並不會回復。 修改的部分可以參考 svn diff target/linux/ 並可以下 svn revert -R target/linux/ 來回復。
參照: Customizing the kernel options

原始碼鏡射位置
'Build system settings' 包含會影響套件位置的選項，以便於操控本地端的套件組:
套件原始碼的本地端鏡射位置
下載資料夾
第一個選項，你只需要輸入那個套件原始碼的完整的ftp或web伺服器位址。下載資料夾會一樣的放在你本地端的路徑資料夾。如果是ftp或web伺服器提供TAR封裝檔，OpenWrt的建置系統會先嘗試下載在Makefile裡描述的位址。也可以指定在建置系統上的下載資料夾。
如果你需要特定或非標準的驅動程式，必須到'Kernel modules'選定。這通常是需要USB模組或是特定的網路介面的驅動程式等。

客製化檔案
在許多狀況，可能需要一個已被預先設定好的客製化映像檔。可以放置你的客製化檔案到
<buildroot dir>/files/
例如，你想要先設定好/etc/config/firewall，那就把修改好的firewall設定檔放到:
<buildroot dir>/files/etc/config/
例如，你的<buildroot dir> 是 /openwrt/trunk。如果你想把某些檔案放到映像檔中的/etc/config資料夾，就把這些檔案放到 /openwrt/trunk/files/etc/config.

- 建置映像檔
當全部都準備好可以建置映像檔了，只要下這麼一個命令:
make
這個命令會開始一連串的活動，如你所知的
編譯 toolchain
用toolchain做跨平台編譯原始碼
產生opkg套件
產生可以flashed的韌體映像檔
Make 選項
多核心CPU建置
建置的程序可以透過多個非同步的程序來加速，使用 -j選項:
make -j 3
使用標準的公式 <CPU核心數目 + 1>
如果會發生不固定建置錯誤，請試著拿掉 -j選項後再編譯一次。
背景建置
如果你希望建置的過程中還可以使用你的系統，你可以讓建置的程序只使用閒置的 I/O 和 CPU 資源 (雙核心 CPU):
ionice -c 3 nice -n 20 make -j 2
建置單一套件
在開發OpenWrt套件的時候，僅編譯套件是來得方便多的 (例如建置套件 cups):
make package/cups/compile V=s
如套件 mc (midnight commander)包含feed packages 的套件:
make package/feeds/packages/mc/compile V=s
注意:啟始路徑為package 目錄和 package/feeds 的或許不會和feeds的結構相同。 如套件 ~/openwrt/trunk/feeds/packages/net/snort 要用 make ~/openwrt/trunk/package/feeds/packages/snort/compile V=s來編譯。
建置錯誤
如果因為某些原因建置錯誤了，最簡單的方式就是使用:
make V=s 2>&1 | tee build.log | grep -i error
這個命令會記錄全部的建置輸出到 /openwrt/trunk/build.log 並顯示error的部分到螢幕上。
另一個範例:
ionice -c 3 nice -n 20 make -j 2 V=s CONFIG_DEBUG_SECTION_MISMATCH=y 2>&1 | tee build.log | egrep -i '(warn|error)'
這個命令在雙核心CPU環境用背景建置並記錄全部的建置輸出到 build.log 且顯示warnings和error的部分到螢幕上。
使用beep聲提示
依照你的使用的CPU，建置程序需要一些時間或更久。你可以使用 echo -e '\a'來做聲音的提示:
make V=s ; echo -e '\a'

- 映像檔位置
建置成功後，最新的映像檔會放在 <buildroot dir>/bin 資料夾。編譯過的檔案會依照目的平台來放置，如韌體是給ar71xx裝置的，就會被放在 <buildroot dir>/bin/ar71xx 資料夾裡。
例:假設你的 <buildroot dir> 是 /openwrt/trunk 這個二進制檔就在 /openwrt/trunk/bin/ar71xx.
清除編譯
如果需要清除建置環境的時候，以下的make參數可以使用:
清除
make clean
刪除 bin 和 build_dir 目錄內容。
清除目錄
make dirclean
除了刪除 /bin 和 /build_dir 的內容，並包含 /staging_dir 和 /toolchain (跨平台編譯的工具). 'Dirclean' 是基本的清除指令。
清除編譯
make distclean
消滅所有的已編譯的部分或設定，並刪除以下載的套件和原始碼。
注意: 請小心使用，這個命令會 移除你的建置設定(.config)，toolchain和其他所有的原始碼!
在OpenWrt的建置環境中還有很多的功能，以上已包含部分的概念。
建置範例
https://forum.openwrt.org/viewtopic.php?pid=129319#p129319
https://forum.openwrt.org/viewtopic.php?id=28267
問題排除
首先使用"make V=s"選項來取得更多資訊。
Missing source code file, due to download problems
先檢查Makefile裡的URL路徑的結尾是否包含斜線，試著將它移除。 或是手動下載原始碼，並放到 "dl" 資料夾。
Compilation errors
試著更新原始碼和所有的feeds (注意! 可能會導致其他問題)。 檢查是否有相關的臭蟲 (TRAC), 可以使用filter來搜尋。 或是直接在那裏回報問題，請提供套件名稱，目的CPU和映像檔等以及原始碼和套件版本。 使用 make -j … 有時會發生不固定的錯誤。回報前請先不使用-j選項編譯。
Bad environment variables
GREP_OPTIONS 不應該有 –initial-tab 或是其他會影響輸出的選項。
SED 不應該被設定。如果已存在編譯前請執行 `unset SED` 。 (參照 Ticket 10612.)
I can't find my <package> in menuconfig
請先試過這個命令 See this.
./scripts/feeds install <package>
也許你找錯子目錄了。請參考套件的 Makefile 。
cat package/feeds/packages/<package>/Makefile
找到如下:
define Package/<package>/Default
  SUBMENU:=Firewall
  SECTION:=net
  CATEGORY:=Network
Error: No rule to make target...
請確認路徑是以 package 資料夾開始，並確認資料夾存在。feeds 和 package/feeds 資料夾的結構是不一樣的。 See this.
錯誤: make feeds/packages/utils/screen/compile V=s
正確: make package/feeds/packages/screen/compile V=s
WARNING: skipping <package> -- package not selected
執行 make menuconfig 並開啟這個套件。 把它標記為 <*> 或 <M> 讓編譯正常. See this.

============================================================
## openwrt學習：make menuconfig的一些筆記 ##
本文記錄openwrt編譯配置的一些筆記，這些配置只是筆者的一個實踐例子，當然，還有更多的配置選擇，那是諸君之事了。
一、介紹
make menuconfig不僅僅配置內核，還有rootfs(實際為busybox)、app(系統庫、界面工具。內核配置位於：chaos_calmer\package\kernel\linux。不同的驅動配置在不同的文件，具體根據文件名稱可識別出。
```
ls chaos_calmer/package/kernel/linux/modules/
001-depends.mk  crypto.mk    hwmon.mk  leds.mk        netfilter.mk   other.mk   spi.mk    virtual.mk   wpan.mk
block.mk        firewire.mk  i2c.mk    lib.mk         netsupport.mk  pcmcia.mk  usb.mk    w1.mk
can.mk          fs.mk        input.mk  netdevices.mk  nls.mk         sound.mk   video.mk  wireless.mk
```
二、配置
下面簡單列出筆記的配置的一部分內容。
1、平台類型
Target System (x86)  --->
這裡只選擇x86。根據平台類型的不同，後面的選項也有不同。
2、目標板鏡像文件
生成的鏡像文件的相關配置。
```
Target Images  --->
[*] tar.gz  # 壓縮包格式
[*] ext4  ---> # 可選ext4的最大節點數以及block大小
[*] Build GRUB images (Linux x86 or x86_64 host only)
[*]   Use Console Terminal (in addition to Serial)   # 開啟串口調試終端
(ttyS0) Serial port device # 串口設備名，一般為ttyS0
(115200) Serial port baud rate # 波特率，選擇的與串口工具設置的波特率必須一致
(3)   Seconds to wait before booting the default entry # grub倒計時，單位為秒
(4) Kernel partition size (in MB)  # 內核的大小，單位為MB，一般3、4MB足夠
(64) Root filesystem partition size (in MB) # 
```
根文件系統大小，這個值越大，鏡像體積越大，一般路由系統幾十MB足夠
3、鏡像配置(系統腳本及IP配置)
```
[*] Image configuration  --->
--- Preinit configuration options
  [*]   Suppress stderr messages during preinit
  (2)   Failsafe wait timeout
  [ ]   Show all preinit network messages
  [ ]   Suppress network message indicating failsafe
  ()    Preinit network interface  # 默認IP地址
  (192.168.1.1) IP address for preinit network messages
  (255.255.255.0) Netmask for preinit network messages
  (192.168.1.255) Broadcast address for preinit network messages
```
4、基礎系統
本配置項為構建基本的文件系統，基本工具，庫，等。默認即可。
```
Base system  --->     
<*> base-files................................... Base filesystem for OpenWrt # 基本文件系統
<*> dropbear........................................ Small SSH2 client/server #ssh伺服器
-*- libc........................................................... C library # C庫
-*- libgcc............................................... GCC support library # gcc支援庫
-*- libpthread.......................................... POSIX thread library # 線程庫
-*- librt................................ POSIX.1b RealTime extension library# 運行時庫
```
5、root權限命令
如sudo等命令
Administration  --->  
6、Boot Loader
此項無內容
Boot Loaders  ---->    
7、開發相關
開發專用，會安裝如gcc、gdb、ar、patch、binutils等工具，普通用戶無須關注。
Development  --->    
8、固件
個別模組的固件，如是，則要加入內核。X86平台，無須理會。
Firmware  --->        
9、內核模組
真正的內核配置在此處。本模組較重要，內容較多。但本文使用的X86平台上需要配置的東西不多。
Kernel modules  --->  
9.1、塊設備
Block Devices  --->
```
-*- kmod-scsi-core....................................... SCSI device support
```
9.2、文件系統
本次移植使用的文件系統為EXT4。其它不需要。
```
Filesystems  --->
<*> kmod-fs-ext4..................................... EXT4 filesystem support
-*- kmod-fs-nfs....................................... NFS filesystem support
-*- kmod-fs-nfs-common......................... Common NFS filesystem modules
```
9.3、硬體監控模組
如LM75，不使用。
Hardware Monitoring Support  --->   
9.4、I2C支援
該X86平台使用IGB網路驅動，需要I2C的支援，故選擇。
```
I2C support  --->
<*> kmod-i2c-core................................................ I2C support
```
9.5、輸入模組
如USB滑鼠、鍵盤，等。
```
Input modules  --->    
-*- kmod-hid..................................................... HID Devices
<*> kmod-hid-generic.............................. Generic HID device support
-*- kmod-input-core........................................ Input device core
-*- kmod-input-evdev...................................... Input event device   
```
9.6、本地語言支援
```
Native Language Support  --->
-*- kmod-nls-base.................................... Native Language Support
```
9.7、netfilter擴展
iptables的選項需要內核的支援，在此進行選擇。文本使用預設值。
Netfilter Extensions  --->
9.8、網路設備
該X86平台使用的網路設備驅動為IGB，其它不選。
```
Network Devices  --->  
-*- kmod-ifb........................... Intermediate Functional Block support
<*> kmod-igb....... Intel(R) 82575/82576 PCI-Express Gigabit Ethernet support # IGB驅動
-*- kmod-libphy.................................................. PHY library # PHY庫，必須
-*- kmod-mii..................................................... MII library
```
9.9、網路支援
對網路的支援，比如8021q、DNS、ipv6。
```
Network Support  --->
<*> kmod-8021q........................................... 802.1Q VLAN support
-*- kmod-dnsresolver.................................. In-kernel DNS Resolver
-*- kmod-ipv6................................................... IPv6 support
```
9.10、其它模組
openwrt的menuconfig涉及大量其它東西，而內核只是其中一部分，故不像真正的kernel的menuconfig那樣分類詳細。很多字元類設備都在此選項。比如MMC、EEPROM、RTC、串口。
```
Other modules  --->
<*> kmod-serial-8250.............................................. 8250 UARTs   # 串口設備
```
9.11、SPI支援
SPI驅動，不使用。
SPI Support  --->
9.12、音頻支援
不使用音頻驅動。
Sound Support  --->
9.13、USB支援
USB介面輸入設備，U盤支援，在此處選擇。
```
USB Support  --->    
-*- kmod-usb-core............................................ Support for USB
<*> kmod-usb-ohci............................... Support for OHCI controllers
<*> kmod-usb-storage..................................... USB Storage support
```
9.14、視頻支援
不使用視頻功能。
Video Support  --->
9.15、無線驅動
不使用無線驅動。
Wireless Drivers  --->
10、編程語言
如Java、Lua、PHP、Perl、Python、Ruby。由於openwrt使用Lua，建議選上。
Languages  --->       
11、庫
常用庫。如壓縮為libbz2、SSL庫、libexif，等，使用默認選項。SSL建議選擇。
Libraries  --->       
12、界面選項配置
openwrt的界面使用LuCI，功能項、工具在此配置。內容較龐大、較重要。
```
LuCI  --->
1. Collections  ---> 
2. Modules  --->     
3. Applications  --->
4. Themes  --->      
5. Protocols  --->   
6. Libraries  --->   
9. Freifunk  --->
```
12.1、綜合
1. Collections  --->     
```
-*- luci   
<*> luci-ssl......................... Standard OpenWrt set with HTTPS support
```
12.2、模組
LuCI基本模組在此配置。包含各種語言支援。
2. Modules  --->
```
-*- luci-base............................................ LuCI core libraries
Translations  --->
<*> Chinese (zh-cn)        # 中文支援
-*- luci-mod-admin-full. LuCI Administration - full-featured for full control
```
12.3、應用程式
界面上的應用程式在此配置。如防火牆、QOS、NTP同步，等。
```
3. Applications  --->    
-*- luci-app-firewall................ Firewall and Portforwarding application
<*> luci-app-ntpc.............. NTP time synchronisation configuration module
<*> luci-app-qos..................... Quality of Service configuration module
<*> luci-app-vnstat.................................. LuCI Support for VnStat
```
12.4、主題
默認主題為luci-theme-bootstrap。
```
4. Themes  --->      
-*- luci-theme-bootstrap........................... Bootstrap Theme (default)
<*> luci-theme-freifunk-bno.................... Freifunk Berlin Nordost Theme
<*> luci-theme-freifunk-generic....................... Freifunk Generic Theme
<*> luci-theme-openwrt................................ LuCI OpenWrt.org theme
```
12.5、協定
如3G、ipv6、PPP。
```
5. Protocols  --->   
<*> luci-proto-3g............................................. Support for 3G
-*- luci-proto-ipv6........... Support for DHCPv6/6in4/6to4/6rd/DS-Lite/aiccu
-*- luci-proto-ppp.......................... Support for PPP/PPPoE/PPPoA/PPtP
```
12.6、庫
```
6. Libraries  --->   
-*- luci-lib-ip....... Lua library for IP calculation and routing information
-*- luci-lib-nixio....................................... NIXIO POSIX library  
```
13、郵件
郵件服務。不使用。
Mail  --->            

14、多媒體
多媒體配置，如ffmpeg、流媒體播放工具。不使用。
Multimedia  --->      

15、網路
本項為網路相關工具、模組的配置。內容較多，也較重要。
```
Network  --->
SSH  --->
-*- openssh-client............................................ OpenSSH client
-*- openssh-keygen............................................ OpenSSH keygen
<*> openssh-server............................................ OpenSSH server
Time Synchronization  ---> # 時間同步
-*- ntpclient............................. NTP (Network Time Protocol) client
<*> ntpdate..................................................... ISC ntp date
VPN  ---> # VPN，不使用
Web Servers/Proxies  --->
-*- uhttpd........................ uHTTPd - tiny, single threaded HTTP server # 小型web伺服器
<*> ethtool......................... Display or change ethernet card settings
<*> iperf
<*> tcpdump..................... Network monitoring and data acquisition tool
```
16、音頻
不使用音頻相關工具、庫，不用配置。
```
Sound  --->           
```
17、其它工具
一些其它小工具在此。內容較雜。有的是boot loader，有的是壓縮庫，有的是編輯器(vim)。還有其它工具，如minicom、grep、tar、bash、file，等。根據實際選擇。
```
Utilities  --->    
Editors  --->  # 編輯器
<*> vim.............................. Vi IMproved - enhanced vi editor (Tiny)
Terminal  --->  # 終端工具
<*> minicom....................................... Terminal emulation program
database  --->  # 數據庫，如mysql、sqlite
zoneinfo  --->  # 時區資訊
<*> bash.......................................... The GNU Bourne Again Shell
<*> grep.................................. grep search utility - full version
<*> hwclock.................................. query or set the hardware clock
<*> tar.............................................................. GNU tar
```

```
make V=99
/usr/bin/pod2man bin/guards > bin/guards.1
make[4]: *** No rule to make target `compat/column.in', needed by `po/quilt.pot'.  Stop.
make[4]: Leaving directory `/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt/build_dir/host/quilt-0.63'
make[3]: *** [/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt/build_dir/host/quilt-0.63/.built] Error 2
make[3]: Leaving directory `/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt/tools/quilt'
make[2]: *** [tools/quilt/compile] Error 2
make[2]: Leaving directory `/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt'
make[1]: *** [/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt/staging_dir/target-mipsel_24kec+dsp_uClibc-0.9.33.2/stamp/.tools_install_yynyynynynyyyyyyyyynyyyyyyyyynyyyyynnyyynnyynnnyy] Error 2
make[1]: Leaving directory `/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt'
make: *** [world] Error 2
jazzhipster@ubuntu:/media/Rd353Backup/DexterBackup/MTK7688_SDK/openwrt$ ^C
```
[Solve]
检查编译环境，若可进行编译则生成默认配置： 
make defconfig 
若defconfig回显提示缺少软件包或编译库等依赖，则按提示安装所缺软件包或库等即可

[SOLVE]
將缺少的軟體包或librayr等相依軟體，安裝or複製到以下路街徑。
openwrt/staging_dir/target-mipsel_24kec+dsp_uClibc-0.9.33.2/

============================================================
## DIY a Wi-Fi Speaker ##
There's few steps to follow:
1. Connect 7688 to a Wi-Fi router
```
# vi /etc/config/wireless
config wifi-iface 'sta'
	option device 'radio0'
	option mode 'sta'
	option network 'wan'
	option ifname 'apcli0'
	option led 'mediatek:orange:wifi'
	option ssid 'UplinkAp'    # Setting SSID
	option key 'SecretKey'    # Setting paas word
	option encryption 'psk'
	option disabled '0'       # Enable setting
Save and exit
# wifi down
# wifi up   
wait for WiFi connecting</p>
```
2. Install shairport
```
# opkg updat
# opkg install avahi-daemon dbus libao libavahi libavahi-client libdbus libexpat shairport
```
3. Enable startup running
```
# /etc/init.d/shairport enable
# /etc/init.d/shairport start
```
4. Change shairport Configuration
```
# echo “” > /etc/config/shairport
# vi /etc/config/shairport
config shairport
         option name 'Shairport_lks7688'
         option password ''
         option port '5002'
         option buffer '256'
         option log '/var/log/shairport'
         option cmd_start ''
         option cmd_stop ''
         option cmd_wait '0'
         option audio_output ''
         option mdns ''
# reboot
```
5. Now use iphone to push music to Shairport_lks7688
6. Code to display music and IP address through Grove - LCD RGB Backlight
```
# Copy and save code bellow to /root/ rgb_lcd_display_mpc_music.js

function ledStrip_init(){
    var m = require("mraa");
    i2c =  new m.I2c(0);                          
                                              
    i2c.address(0x23);                            
    var buf1 = new Buffer([0x80, 0, 0xCC, 0, 0xCC])
    var buf2 = new Buffer([0x80, 1, 0xCC, 0, 0xCC])
    var buf3 = new Buffer([0x80, 2, 0xCC, 0, 0xCC])
    var buf4 = new Buffer([0x80, 3, 0xCC, 0, 0xCC])
    var buf5 = new Buffer([0x80, 4, 0xCC, 0, 0xCC])
    i2c.write(buf1);
    i2c.write(buf2);
    i2c.write(buf3);
    i2c.write(buf4);                  
    i2c.write(buf5);
};
setTimeout(ledStrip_init, 2000);
var LCD = require('jsupm_i2clcd');
// Initialize Jhd1313m1 at 0x62 (RGB_ADDRESS) and 0x3E (LCD_ADDRESS)
var myLcd = new LCD.Jhd1313m1 (0, 0x3E, 0x62);
myLcd.setCursor(0,0);
// RGB Blue
//myLcd.setColor(53, 39, 249);
// RGB Red
function clear_lcd(line){
    myLcd.setCursor(line, 0);
    myLcd.write("                ");
    myLcd.setCursor(line, 0);
}
var musicName = "";
var ipAddr = "";
function display_music_name(){
    var exec = require('child_process').exec;
    exec('mpc status | awk \'{if(NR==1) print}\'',function(error, stdout, stderr){
        if(musicName != stdout) {
            console.log(stdout);
            clear_lcd(0);
            myLcd.write(stdout);
        }
        musicName = stdout;
    });
   
    exec('ifconfig | awk \'{if(NR==2) print $2}\'', function(error, stdout, stderr){
        if(ipAddr != stdout) {
            console.log(stdout);   
            clear_lcd(1);
            myLcd.write(stdout.slice(4));
        }
        ipAddr = stdout;
    });
}
setInterval(display_music_name, 1000);
7. Copy and save Startup running
script /etc/init.d/rgb_lcd_mpc 
#!/bin/ash /etc/rc.common<br>START=99
start() {
        sleep 5   # make sure boot process is done, no more console msgs
        . /etc/profile
        echo $PATH
        node /root/rgb_lcd_display_mpc_music.js
}
stop() {
         killall node
}

Step 8 – Enable startup running script
# /etc/init.d/ rgb_lcd_mpc enable
# /etc/init.d/ rgb_lcd_mpc start&
```
Finally, connect cables and restart lks7688.
Step 8: Play a Music
Picture of Play a Music
Now, open your music player and enjoy.

============================================================
## LinkIt Smart 7688 問題匯總 ##
1. 系統編譯
1.1 .config文件
openwrt中，make menuconfig生成.config文件後，我們如何對.config中自定義的差異內容進行進行備份，方便移植到其它的系統中，這是一個問題。當然，有人說有很多簡單的方法。但是這些都不是Openwrt開發著所希望看到的。對於Openwrt，開發團隊創建了簡單的工具scripts/diffconfig.sh`。我們可以採用這個工具進行配置保存工作。
有一個簡單的方法，生成diff文件，然後通過git進行操作，這樣我們可以對我們自己的openwrt進行定制備份了。
1.1.1 如何創建config diff文件
```
  $./scripts/diffconfig.sh > config.diff
```  
1.1.2 如何使用config diff文件
```
  $cp config.diff .config
  $make defconfig
```  
或者
```
  $cat config.diff >> .config
  $make defconfig
```  
1.1.3 make meunconfig
```
  $make menuconfig
```
1.1.3 make kernel_menuconfig
```
$ make kernel_menuconfig
```
1.2 編譯
系統編譯很簡單，直接在系統目錄下運行make命令就可以了，如果想查看輸出資訊，可以在make後面增加V=s/V=99。如果是多核系統，可以在後面再增加j=2或其它數字，這代表同時有多個線程同時運行。這樣可以提高編譯速度。我的系統是單核的，我驗證了一下沒有任何改善。多核系統可以測試一下。
```
 $ make V=99
``` 
1.2.1 linux核心編譯
如果我們僅僅是想對linux核心包進行編譯，可以採用下面的命令來進行。
```
 $ make target/linux/{clean,prepare} V=s QUILT=1
``` 
1.2.2 package編譯（以Madplay為例）
http://jphome.github.io/blog/2014/03/29/openwrt_sdk.html
全新編譯madplay
```
  $ make package/feeds/packages/madplay/{clean,compile,install} V=s
  $ make package/feeds/packages/madplay/{compile,install} V=s
```  
重新編譯madplay
```
$ make package/feeds/packages/madplay/compile V=s
```
1.2.3 package安裝(以Madplay為例)
madplay安裝
複製ipk文件到openwrt系統(採用scp命令)，然後通過opkg進行安裝。
```
  $ scp bin/ramips/packages/packages/madplay-alsa_0.15.2b-4_ramips_24kec.ipk root@192.168.1.168:/tmp
```  
安裝madplay到openwrt
```
  # root@mylinkit:/tmp# opkg install madplay-alsa_0.15.2b-4_ramips_24kec.ipk
    Installing madplay-alsa (0.15.2b-4) to root...
    Configuring madplay-alsa.
```
MadPay源碼修改
$ wget ftp://ftp.mars.org/pub/mpeg/madplay-0.15.2b.tar.gz
得到madplay源碼，修改player.c，採用FIFO控制方式，然後編譯madplay.
```
$ make package/feeds/packages/madplay/{compile,install} V=s
$ scp bin/ramips/packages/packages/madplay-alsa_0.15.2b-4_ramips_24kec.ipk root@192.168.1.168:/tmp
```
```
# opkg install madplay-alsa_0.15.2b-4_ramips_24kec.ipk
# madplay /Media/USB-A1/*.mp3
# echo f > /tmp/.madplayFIFO
```
創建madplayCon.c文件
```
# make package/feeds/packages/gogoo/ethMOH/{clean,compile,install} V=s
  KEY_PAUSE    = 'p', 
  KEY_STOP     = 's',
  KEY_FORWARD  = 'f',
  KEY_BACK     = 'b',
  KEY_TIME     = 't',
  KEY_QUIT     = 'q',
  KEY_INFO     = 'i',
  KEY_GAINDECR = '-',
  KEY_GAININCR = '+',
  KEY_GAINZERO = '_',
  KEY_GAININFO = '='
```  
1.3 dts文件修改
1.3.1 按鈕相關修改
MT7688按鈕一組為32個，所以GPIO0組對應GPIO0-PIO32，GPIO1組對應GPIO32以上的引腳。
參考連接https://wiki.openwrt.org/doc/howto/hardware.button?s[]=button&s[]=hotplug
```
    gpio-keys-polled {
        compatible = "gpio-keys-polled";
        #address-cells = <1>;
        #size-cells = <0>;
        poll-interval = <20>;
        wps {
            label = "wps";
            gpios = <&gpio1 6 1>;     // GPIO38 wifi button
            linux,code = <0x211>;
        };
        key_playpause {
            label = "key_playpause";
            gpios = <&gpio0 15 1>;      // GPIO15-KEY_PLAY/Pause(S5)
            linux,code = <164>;
        };
        key_volumeup {
            label = "key_volumeup";
            gpios = <&gpio0 17 1>;      //GPIO17-KEY_VOL+(S7)
            linux,code = <115>;
        };
        key_volumedown {
            label = "key_volumedown";
            gpios = <&gpio0 18 1>;      //GPIO18-KEY_VOL-(S8)
            linux,code = <114>;
        };
        key_next {
            label = "key_next";
            gpios = <&gpio0 16 1>;      //GPIO16-KEY_NEXT(S6)
            linux,code = <0x197>;
        };
        key_previous {
            label = "key_previous";
            gpios = <&gpio0 14 1>;      //GPIO14-KEY_PRE(S4)
            linux,code = <0x19c>;
        };
    };
```    
尖括號中的內容為標準按鍵代碼，可以在linux/include/uapi/linux/input.h中查詢到。
1.3.2 SD卡檢測引腳電平修改
LinkIt smart7688的SD卡檢測，默認是高電平。但是普通的SD卡是低電平。所以，要對dts進行修改。使用下面命令：
$ vi target/linux/ramips/dts/LINKIT7688.dts
修改前：
```
    sdhci@10130000 {
        status = "okay";
        mediatek,cd-high;
//      mediatek,cd-poll;
    };
```    
修改後：
```
        sdhci@10130000 {
        status = "okay";
        mediatek,cd-low;
//      mediatek,cd-poll;
    };
```    
1.4 package創建
package的Makefile
PKG_NAME - The name of the package, as seen via menuconfig and ipkg
PKG_VERSION - The upstream version number that we』re downloading
PKG_RELEASE - The version of this package Makefile
PKG_LICENSE - The license(s) the package is available under, SPDX form.
PKG_LICENSE_FILE- file containing the license text
PKG_BUILD_DIR - Where to compile the package
PKG_SOURCE - The filename of the original sources
PKG_SOURCE_URL - Where to download the sources from (directory)
PKG_MD5SUM - A checksum to validate the download
PKG_CAT - How to decompress the sources (zcat, bzcat, unzip)
PKG_BUILD_DEPENDS - Packages that need to be built before this package, but are not required at runtime. Uses the same syntax as DEPENDS below.
PKG_INSTALL - Setting it to 「1」 will call the package』s original 「make install」 with prefix set to PKG_INSTALL_DIR
PKG_INSTALL_DIR - Where 「make install」 copies the compiled files
PKG_FIXUP - See below
PKG_SOURCE_PROTO - the protocol to use for fetching the sources (git, svn)
PKG_REV - the svn revision to use, must be specified if proto is 「svn」
PKG_SOURCE_SUBDIR - must be specified if proto is 「svn」 or 「git」, e.g. 「PKG_SOURCE_SUBDIR:=(PKG_NAME)?(PKG_VERSION)」
PKG_SOURCE_VERSION - must be specified if proto is 「git」, the commit hash to check out
PKG_CONFIG_DEPENDS - specifies which config options depend on this package being selected
SECTION - The type of package (currently unused) //包的類型
CATEGORY - Which menu it appears in menuconfig //menuconfig的哪一個功能表顯示
TITLE - A short description of the package //包的簡短描述
DESCRIPTION - (deprecated) A long description of the package //報的一個長描述
URL - Where to find the original software // 那裡找到源軟體
MAINTAINER - (required for new packages) Who to contact concerning the package // 包的聯繫
DEPENDS - (optional) Which packages must be built/installed before this package. See below for the syntax. // 哪些包需要必須先編譯/安裝
PKGARCH - (optional) Set this to 「all」 to produce a package with 「Architecture: all」
USERID - (optional) a username:groupname pair to create at package installation time.
1.5 JFFS2-Journalling Flash File System Version2
JFFS2全名是 Journalling Flash File System Version2，是Redhat公司開發的閃存文件系統[1]，其前身是JFFS, 最早只支援NOR Flash, 自2.6版以後開始支援NAND Flash, 極適合使用於嵌入式系統。https://zh.wikipedia.org/wiki/JFFS2
1.5 如何創建自己的板子支援
增加mt7688支援 
參考CC代碼：(CC-2015/10/19 18:19:18-SHA-1: 3d98b29a3d0aa854fad712a92ace42ad06e92d6b) 
* 修改target\linux\ramips\Makefile文件，增加mt7688支援 
* 修改target\linux\ramips\modules.mk文件，增加TARGET_ramips_mt7688支援 
* 創建target\linux\ramips\mt7688\config-3.18文件 
* 創建target\linux\ramips\mt7688\profiles\00-default.mk文件 
* 創建target\linux\ramips\mt7688\target.mk文件
增加LinkIt Smart7688支援 
參考CC代碼：(CC-2015/10/19 18:19:22-SHA-1: 8829dee8871e45c675a4bd4036c188c6d0f5645b) 
* 在package\boot\uboot-envtools\files\ramips添加linkits7688板名支援 
* 在target\linux\ramips\base-files\etc\board.d\02_network添加linkits7688支援 
* 在target\linux\ramips\base-files\lib\ramips.sh中添加linkits7688支援 
* 在target\linux\ramips\base-files\lib\upgrade\platform.sh中添加linkits7688支援 
* 增加target\linux\ramips\dts\LINKIT7688.dts文件 
* 修改target\linux\ramips\image\Makefile文件 
* 增加target\linux\ramips\mt7688\profiles\01-mediatek.mk文件
參考windora 
* 修改target\linux\ramips\base-files\etc\board.d\02_network 
* 修改target\linux\ramips\base-files\lib\ramips.sh 
* 修改target\linux\ramips\base-files\lib\upgrade\platform.sh 
* 修改target\linux\ramips\image\Makefile 
* 創建一個*.mk文件到target\linux\ramips\mt7688\profiles\目錄下 
* 創建一個example.dts文件到target\linux\ramips\dts\目錄下
root@mylinkit:~# cat /proc/cpuinfo
```
system type             : MediaTek MT7688 ver:1 eco:2
machine                 : MediaTek LinkIt Smart 7688
processor               : 0
cpu model               : MIPS 24KEc V5.5
BogoMIPS                : 385.84
wait instruction        : yes
microsecond timers      : yes
tlb_entries             : 32
extra interrupt vector  : yes
hardware watchpoint     : yes, count: 4, address/irw mask: [0x0ffc, 0x0ffc, 0x0ffb, 0x0ffb]
isa                     : mips1 mips2 mips32r1 mips32r2
ASEs implemented        : mips16 dsp
shadow register sets    : 1
kscratch registers      : 0
package                 : 0
core                    : 0
VCED exceptions         : not available
VCEI exceptions         : not available
```
1.6 rpcd - (OpenWrt ubus RPC backend server)
1.7 patch
http://blog.csdn.net/wwx0715/article/details/25160361
```
$ quilt --help
```
用法：
```
quilt [--trace[=verbose]] [--quiltrc=XX] command [-h] ...
       quilt --version
```       
命令是：
```
        add       fold    new       remove    top
        annotate  fork    next      rename    unapplied
        applied   graph   patches   revert    upgrade
        delete    grep    pop       series
        diff      header  previous  setup
        edit      import  push      shell
        files     mail    refresh   snapshot
```
Global options:
```
--trace
        Runs the command in bash trace mode (-x). For internal debugging.

--quiltrc file
        Use the specified configuration file instead of ~/.quiltrc (or
        /etc/quilt.quiltrc if ~/.quiltrc does not exist).  See the pdf
        documentation for details about its possible contents.  The
        special value "-" causes quilt not to read any configuration
        file.

--version
        Print the version number and exit immediately.
```        
1.7.1 準備quilt配置
```
$ cd ~
cat > ~/.quiltrc <<EOF
QUILT_DIFF_ARGS="--no-timestamps --no-index -p ab --color=auto"
QUILT_REFRESH_ARGS="--no-timestamps --no-index -p ab"
QUILT_PATCH_OPTS="--unified"
QUILT_DIFF_OPTS="-p"
EDITOR="nano"
EOF
**1.7.2
$ cd ~/openwrt/openwrt_ethMOH/build_dir/target-mipsel_24kec+dsp_uClibc-0.9.33.2/linux-ramips_mt7688/linux-3.18.29/
$ quilt series
$ quilt new platform/502-alsa.patch
$ quilt edit sound/soc/codecs/wm8960.c
$ quilt diff
$ quilt refresh
$ cd ../../../../
$ make target/linux/update package/index V=s
修改存在的patch
$ quilt push platform/502-alsa.patch
$ quilt edit sound/soc/codecs/wm8960.c
$ quilt diff
$ quilt refresh
$ cd ../../../../

$ make target/linux/update V=s  //民間更新patch到target/linux/ramips/patches-xxx方法
/$ make target/linux/update package/index V=s //官方更新patch到target/linux/ramips/patches-xxx方法

$ make target/linux/{clean,prepare} V=s QUILT=1
```
1.8 Makefile
$? - 當前目標所依賴的文件列表中比當前目標文件還要新的文件
$@ - 當前目標名字
$< - 當前依賴文件的名字
$* - 不包括後綴名的當前依賴文件的名字
1.9 WM8960聲卡
Linkit的默認的聲卡是WM8960，該聲卡為I2S介面。Linkit默認WM8960使用的為外部晶振提供時鐘頻率。所以如果我們希望採用MT7688的REF_CLK0信號作為WM8960的時鐘信號的話，我們就需要對MTK的配置文件進行一些修改。 
具體的修改可以參考https://github.com/hnhkj/CC15.05.git的代碼。
1.10 USB聲卡CM108
https://wiki.openwrt.org/doc/howto/usb.audio?s[]=sound
1.11 wps 功能 (don't support)
http://labs.mediatek.com/forums/posts/list/4850.page
1.12 init.d/rc.d開機自動運行
參考文檔：https://wiki.openwrt.org/doc/techref/initscripts
啟動方法： 
1，創建腳本到 init.d(具體參考原來文檔)。 
2，開機自動運行./etc/init.d/example enable。 
3, 使能自動運行可以在/etc/rc.d/ 下查找到連接
1.13 eclipse
http://downloads.openwrt.org/docs/eclipse.pdf
2. 系統配置
2.1 MTD
參考連接：https://wiki.openwrt.org/doc/techref/mtd
```
root@mylinkit:~# mtd
Usage: mtd [<options> ...] <command> [<arguments> ...] <device>[:<device>...]

The device is in the format of mtdX (eg: mtd4) or its label.
mtd recognizes these commands:
        unlock                  unlock the device
        refresh                 refresh mtd partition
        erase                   erase all data on device
        verify <imagefile>|-    verify <imagefile> (use - for stdin) to device
        write <imagefile>|-     write <imagefile> (use - for stdin) to device
        jffs2write <file>       append <file> to the jffs2 partition on the device
        fixseama                fix the checksum in a seama header on first boot
Following options are available:
        -q                      quiet mode (once: no [w] on writing,
                                           twice: no status messages)
        -n                      write without first erasing the blocks
        -r                      reboot after successful command
        -f                      force write without trx checks
        -e <device>             erase <device> before executing the command
        -d <name>               directory for jffs2write, defaults to "tmp"
        -j <name>               integrate <file> into jffs2 data when writing an image
        -s <number>             skip the first n bytes when appending data to the jffs2 partiton, defaults to "0"
        -p                      write beginning at partition offset
        -l <length>             the length of data that we want to dump
```
Example: To write linux.trx to mtd4 labeled as linux and reboot afterwards
         mtd -r write linux.trx linux

2.1.1 如何顯示MTD狀態
```
  root@mylinkit:/tmp# cat /proc/mtd
  dev:    size   erasesize  name
  mtd0: 00030000 00010000 "u-boot"
  mtd1: 00010000 00010000 "u-boot-env"
  mtd2: 00010000 00010000 "factory"
  mtd3: 00fb0000 00010000 "firmware"
  mtd4: 0011a791 00010000 "kernel"
  mtd5: 00e9586f 00010000 "rootfs"
  mtd6: 00100000 00010000 "rootfs_data"
```
2.1.2 dd命令：/bin/dd 
讀取mtd2內的數據內容，mac地址
```
  # dd bs=1 skip=3 count=6 if=/dev/mtd2 2>/dev/null | hexdump
```
參考文檔：linkit-smart-7688-feed\mtk-linkit\files\etc\uci-defaults\51_linkit_config - Line30:
MAC=$(dd bs=1 skip=7 count=3 if=/dev/mtd2 2>/dev/null | hexdump -v -n 3 -e '3/1 "%02X"'
2.1.3 入如何寫firmware到flash.
```
   # cd /tmp
   # wget http://www.example.org/original_firmware.bin
   # mtd -r write /tmp/original_firmware.bin firmware
```   
2.1.4 備份MTD2/factory資訊
```
  # dd if=/dev/mtd2 of=/tmp/factory.bin
```  
2.1.5 寫factory.bin到mtd2
```
  # mtd -r write /tmp/factory.bin factory
```  
注意：如果命令返回不能寫入MTD2，可能是由於你的系統設定了禁止寫該區域的權限。我們可以通過修改target/linux/ramips/dts/LINKIT7688.dts，註銷禁止代碼。這樣就可以將數據寫入到MTD2區域了。
I know that we can modify LINKIT7688 file to allow mtd command modify mtd2's data.
```
/target/linux/ramips/dts/LINKIT7688
line82-86:
factory: partition@40000 {
label = "factory";
reg = <0x40000 0x10000>;
read-only;
};
delete read-only.
```
fw_printenv命令：/usr/sbin/fw_printenv
參考文檔：linkit-smart-7688-feed\mtk-linkit\files\etc\init.d\linkit
Line15:
```
SEQ=fw_printenv -n wifi_seq
```
2.2 用SD卡擴展空間(未驗證)
參考: http://labs.mediatek.com/forums/posts/list/4121.page
Yes!you can mount tf card as overlay
1.install block-mount e2fsprogs kmod-fs-ext4
2.mkfs.ext4 /dev/mmcblk0
3.block detect > /etc/config/fstab
4.vi etc/config/fstab
modify option 'target' '/overlay'
modify option 'enable' '1'
5.reboot,use df -h check

2.3 ifconfig 相關參數
狀態：Ethernet0 連接PC，Wifi連接Router (狀態非常好)
```
ifconfig
apcli0    Link encap:Ethernet  HWaddr 9E:65:F9:0B:18:55
          inet addr:192.168.1.104  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::9c65:f9ff:fe0b:1855/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

br-lan    Link encap:Ethernet  HWaddr 9C:65:F9:1B:10:27
          inet addr:192.168.100.1  Bcast:192.168.100.255  Mask:255.255.255.0
          inet6 addr: fe80::9e65:f9ff:fe1b:1027/64 Scope:Link
          inet6 addr: fdef:dd3c:f1e1::1/60 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:478 errors:0 dropped:0 overruns:0 frame:0
          TX packets:340 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:45279 (44.2 KiB)  TX bytes:46562 (45.4 KiB)

eth0      Link encap:Ethernet  HWaddr 9C:65:F9:1B:10:27
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:525 errors:0 dropped:0 overruns:0 frame:0
          TX packets:307 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:70666 (69.0 KiB)  TX bytes:46599 (45.5 KiB)
          Interrupt:5

eth0.1    Link encap:Ethernet  HWaddr 9C:65:F9:1B:10:27
          inet6 addr: fe80::9e65:f9ff:fe1b:1027/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:26 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:5911 (5.7 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:1269 errors:0 dropped:0 overruns:0 frame:0
          TX packets:1269 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:88230 (86.1 KiB)  TX bytes:88230 (86.1 KiB)

ra0       Link encap:Ethernet  HWaddr 9C:65:F9:1B:18:55
          inet6 addr: fe80::9e65:f9ff:fe1b:1855/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:11176 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2457 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2248608 (2.1 MiB)  TX bytes:42335 (41.3 KiB)
          Interrupt:6
```
2.4 network 配置
```
config interface 'loopback'
    option ifname 'lo'
    option proto 'static'
    option ipaddr '127.0.0.1'
    option netmask '255.0.0.0'

config globals 'globals'
    option ula_prefix 'fd01:80d1:1f98::/48'

config interface 'lan'
    option ifname 'eth0'
    option force_link '1'
    option type 'bridge'
    option proto 'static'
    option netmask '255.255.255.0'
    option ip6assign '60'
    option ipaddr '192.168.100.1'
    option macaddr '00:0c:43:e1:76:2a'

config switch
    option name 'switch0'
    option reset '1'
    option enable_vlan '0'

config interface 'wan'
    option proto 'dhcp'
```
2.5 eeprom配置
eepromn內容可以在/lib/firmware/mt7628.eeprom中。
2.1 - Chip ID(0x00h)
2.2 - Layout Revision ID(0x02)
2.3 - WIFI MAC Address (0x04)
2.4 - WIFI MAC Address (0x28)
2.5 - WIFI MAC Address (0x2E)
2.6 - NIC Configuration 0 (0x34)
2.7 - NIC Configuration 1 (0x36)
2.8 - Country Region Code for 2.4G band (0x39)
2.9 - LED Mode (0x3B)
2.10 - NIC COnfiguration 2 (0x42)
2.11 - RSSI Offset for 2.4G band (0x46)
2.12 - 20M/40M BW Power Delta for 2.4G band (0x50)
2.13 - Temp. Sensor Calibation (0x55)
2.14 - 2.4G Tx0 Power Slope/offset (0x56~0x57)
2.15 - 2.4G Tx0 Target Power (0x58)
2.16 - 2.4G Tx0 Power Low/Middle/High Channel (0x59)
2.17 - 2.4G Tx1 Power Slope/Offset (0x5C~0x5D)
2.18 - 2.4G Tx1 Target Power (0x5E)
2.19 - 2.4G Tx1 Power Offset Low/Middle/High Channel (0x5F~0x61)
2.20 - 2.4G Tx rate power configuration (0xA0~0xBF)
2.21 - External LNA (0xC0)
2.22 - 2.4GHz Step Number (0xC6)
2.23 - Frequency offset (0xF4~0xF6)
2.24 - Reserved for Customer (0x140~0x1EF)
2.6 Sysupgrade
https://wiki.openwrt.org/doc/howto/generic.sysupgrade
與opkg, mtd 等相比, sysupgrade 僅僅是個shell腳本: /sbin/sysupgrade 詣在更容易的實現系統更新.
timezone //時區
時區設置保存在/tmp/TZ中。
```
root@mylinkit:/tmp# cat TZ
UTC
```
2.7 uhttpd
https://wiki.openwrt.org/doc/howto/http.uhttpd
2.8 修改Linkit_Smart_7688默認的SSID
在mtk-linkit\files\etc\uci-defaults\51\_linkit\_config文件中，默認是讀取wifi MAC address的後3個位元組，加載到字串LiniIt_Smart_7688_的後面，根據MAC地址的唯一性，形成一個唯一的SSID地址。如果我們想修改該SSID的話，可以在這個文件中進行修改。又或者配置SSID到uboot環境變數中，形成自己的SSID。這部分實現可以參考lks7688.cfg部分。如果系統在uboot中設置了SSID的話，系統將顯示該SSID。如果沒有設置的話，系統將設置該文件配置的SSID。
```
[ -n "${SSID}" ] || { \
  MAC=$(dd bs=1 skip=7 count=3 if=/dev/mtd2 2>/dev/null | hexdump -v -n 3 -e '3/1 "%02X"')
  SSID=LinkIt_Smart_7688_${MAC}
}
```
2.9 修改Linkit_Smart_7688的版本號
Linkit_Smart_7688默認擁有自己的版本號,該版本號定義在mtk-linkit\files\etc\uci-defaults\54_linkit_version文件中。
uci set system.@system[0].firmware_version=v0.9.3
2.10 修改Linkit_Smart_7688的主機名
Linkit_Smart_7688的主機名在mtk-linkit\files\etc\uci-defaults\51_linkit_config文件中定義，你可以通過修改這個文件來修改主機名。
uci set system.@system[-1].hostname="mylinkIt"
2.11 獲得Linkit_Smart_7688的MAC地址
對於如何獲取MAC地址，OpenWrt提供了詳細的程式介面。可以參考\openwrt\package\base-files\files\lib\functions\system.sh文件，該文件包含的mac的操作函數。在很多的sh文檔中都包含的對該文件的引用。
例如：mtk-linkit\files\etc\uci-defaults\51_linkit_config文件中的wan_mac獲取。
wan_mac=$(mtd_get_mac_binary factory 4)
獲取ap_mac地址（源自：mtk-linkit\files\etc\rc.button\wps 
文件）：
```
iwinfo ra0 info | grep Access | awk '{print $3}')
```
2.12 Linkit_Smart_7688默認模組的添加和刪除
Linkit_Smart_7688默認添加了很多的模組，例如：python，node.js等。我們如何對默認的模組進行修改，添加或刪除想要的模組呢。其實很簡單，我們就是需要修改mtk-linkit\Makefile，在該文件中修改想要或不想要的模組。然後feed install它就可以了。當然，你會發現已經安裝過的模組，在文件中刪除後，編譯後仍然會在firmware中，這是怎麼回事呢？這是因為，在編譯默認的Makefile的時候，系統通過feed已經將原來默認的模組添加進了.config。如果要刪除它們，需要同feed來刪除它們。然後，編譯以後就不會出現了。
```
define Package/mtk-linkit
  TITLE:=MTK LinkIt Smart board support package
  HIDDEN:=1
  DEPENDS:=@TARGET_ramips_mt7688_LinkIt7688 \
    +gdbserver +curl +strace +coreutils +coreutils-stty \
    +avahi-nodbus-daemon +mountd +mjpg-streamer \
  +uhttpd +rpcd +rpcd-mod-iwinfo +git +git-http +samba36-server \
  +python +python-pyserial +python-pip +hidapi \
  +libmraa +libupm +node +node-hid +node-cylon-firmata +yunbridge \
  +luci +luci-theme-openwrt +luci-app-mjpg-streamer +luci-app-samba +luci-lib-json \
  +rpcd-mod-rpcsys +cgi-io +avrdude +spi-tools +uboot-envtools \
  +kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core +kmod-i2c-ralink \
  +kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
  +kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
  +kmod-sdhci-mt7620 +kmod-usb-storage \
  +kmod-video-core +kmod-video-uvc \
  +kmod-sound-core +kmod-sound-mtk +madplay-alsa +alsa-utils \
  +mtk-linkit-webui +mtk-sdk-wifi +tcpdump-mini

  CATEGORY:=Base system
  DEFAULT:=y
endef
```
2.13 如果修改Linkit_Smart_7688默認opkg連接地址
```
ubuntu@ubuntu-System-Name:~/openwrt/openwrt_ethMOH$ cat feeds.conf.default
src-git packages https://github.com/openwrt/packages.git;for-15.05
src-git luci https://github.com/openwrt/luci.git;for-15.05
src-git routing https://github.com/openwrt-routing/packages.git;for-15.05
src-git telephony https://github.com/openwrt/telephony.git;for-15.05
src-git management https://github.com/openwrt-management/packages.git;for-15.05
#src-git targets https://github.com/openwrt/targets.git
#src-git oldpackages http://git.openwrt.org/packages.git
#src-svn xwrt http://x-wrt.googlecode.com/svn/trunk/package
#src-svn phone svn://svn.openwrt.org/openwrt/feeds/phone
#src-svn efl svn://svn.openwrt.org/openwrt/feeds/efl
#src-svn xorg svn://svn.openwrt.org/openwrt/feeds/xorg
#src-svn desktop svn://svn.openwrt.org/openwrt/feeds/desktop
#src-svn xfce svn://svn.openwrt.org/openwrt/feeds/xfce
#src-svn lxde svn://svn.openwrt.org/openwrt/feeds/lxde
#src-link custom /usr/src/openwrt/custom-feed
```
該連接地址的修改主要修改一個文件mtk-linkit\files\etc\opkg\linkit.conf。我們可以通過修改這個文件中的文件指向你的opkg連接地址，然後編譯。編譯後出的OS就可以通過opkg install連接你的伺服器了。當然，如果你不想使用Linkit_Smart_7688默認的opkg連接地址的話，你可以在mtk-linkit\files\etc\init.d\linkit文件中刪除對linkit.conf的初始化部分，這樣在OpenWrt啟動的時候就不會講linit.conf添加/etc/opkg/distfeeds.conf。
當然，如果你不想修改系統，只是在OpenWrt中修改opkg連接地址的話，那也很簡單。你只要用vi命令修改/etc/opkg/distfeeds.conf文件就可以了。這也很簡單。
2.14 如果修改Linkit_Smart_7688默認lan ipaddress.
默認的Lan IPAddress在OpenWrt的/etc/config/network文件中設置，如果想修改ip地址。可以在linkit-smart-7688-feed\mtk-linkit\files\etc\uci-defaults\51_linkit_config文件中進行修改。linkit-smart-7688-feed默認的Lan ipaddr 是 192.168.100.1。
2.15 如果修改Linkit_Smart_7688的GPIO11.
Linkit_Smart_7688的GPIO11引腳，默認用來鎖定CL245A晶片的。該晶片是一個鎖存器，用來提升MT7688的引腳輸出功率和保護MT7688的引腳功能。但是，如果你不需要這個功能，希望將GPIO11引腳釋放出來的話。你可以對源代碼進行一些修改或者刪除。MTK在linux中增加了一個驅動，用來驅動GPIO11引腳的。詳細內容可以參考target\linux\ramips\patches-3.18\0200-linkit_bootstrap.patch文件。
2.16 aplay多聲卡的使用
Linkit默認使用WM8960聲卡，現在增加了一個USB聲卡，聲卡檢測發現了該USB聲卡。http://alsa.opensrc.org/MultipleCards
2.16.1 aplay查詢有效聲卡 aplay -l
```
root@mylinkit:/# aplay -l
**** List of PLAYBACK Hardware Devices ****
card 0: I2S [MTK APSoC I2S], device 0: WMserious PCM wm8960-hifi-0 []
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: Set [C-Media USB Headphone Set], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
```
2.16.2 用指定的聲卡播放 aplay -Dhw:x (x=0,x=1)
```
root@mylinkit:/# aplay -Dhw:1 /Media/SD-P1/*.wav
Playing WAVE '/Media/SD-P1/1.wav' : Signed 16 bit Little Endian, Rate 44100 Hz, Stereo
```
2.16.3 aply -h
```
root@mylinkit:/# aplay -h
Usage: aplay [OPTION]... [FILE]...

-h, --help              help
    --version           print current version
-l, --list-devices      list all soundcards and digital audio devices
-L, --list-pcms         list device names
-D, --device=NAME       select PCM by name
-q, --quiet             quiet mode
-t, --file-type TYPE    file type (voc, wav, raw or au)
-c, --channels=#        channels
-f, --format=FORMAT     sample format (case insensitive)
-r, --rate=#            sample rate
-d, --duration=#        interrupt after # seconds
-M, --mmap              mmap stream
-N, --nonblock          nonblocking mode
-F, --period-time=#     distance between interrupts is # microseconds
-B, --buffer-time=#     buffer duration is # microseconds
    --period-size=#     distance between interrupts is # frames
    --buffer-size=#     buffer duration is # frames
-A, --avail-min=#       min available space for wakeup is # microseconds
-R, --start-delay=#     delay for automatic PCM start is # microseconds
                        (relative to buffer size if <= 0)
-T, --stop-delay=#      delay for automatic PCM stop is # microseconds from xrun
-v, --verbose           show PCM structure and setup (accumulative)
-V, --vumeter=TYPE      enable VU meter (TYPE: mono or stereo)
-I, --separate-channels one file for each channel
-i, --interactive       allow interactive operation from stdin
-m, --chmap=ch1,ch2,..  Give the channel map to override or follow
    --disable-resample  disable automatic rate resample
    --disable-channels  disable automatic channel conversions
    --disable-format    disable automatic format conversions
    --disable-softvol   disable software volume control (softvol)
    --test-position     test ring buffer position
    --test-coef=#       test coefficient for ring buffer position (default 8)
                        expression for validation is: coef * (buffer_size / 2)
    --test-nowait       do not wait for ring buffer - eats whole CPU
    --max-file-time=#   start another output file when the old file has recorded
                        for this many seconds
    --process-id-file   write the process ID here
    --use-strftime      apply the strftime facility to the output file name
    --dump-hw-params    dump hw_params of the device
    --fatal-errors      treat all errors as fatal
Recognized sample formats are: S8 U8 S16_LE S16_BE U16_LE U16_BE S24_LE S24_BE U24_LE U24_BE S32_LE S32_BE U32_LE U32_BE FLOAT_LE FLOAT_BE FLOAT64_LE FLOAT64_BE IEC958_SUBFRAME_LE IEC958_SUBFRAME_BE MU_LAW A_LAW IMA_ADPCM MPEG GSM SPECIAL S24_3LE S24_3BE U24_3LE U24_3BE S20_3LE S20_3BE U20_3LE U20_3BE S18_3LE S18_3BE U18_3LE U18_3BE G723_24 G723_24_1B G723_40 G723_40_1B DSD_U8 DSD_U16_LE
Some of these may not be available on selected hardware
The available format shortcuts are:
-f cd (16 bit little endian, 44100, stereo)
-f cdr (16 bit big endian, 44100, stereo)
-f dat (16 bit little endian, 48000, stereo)
```
2.16.4 arecord & aplay test
```
arecord -f cd -t wav -M /Media/USB-A1/my_recording.wav
aplay -M my_recording.wav
```
2.16.5 參考連接：
http://alsa.opensrc.org/
http://www.cnblogs.com/cslunatic/p/3227655.html 
http://blog.chinaunix.net/uid-26588712-id-3054726.html 
https://wiki.archlinux.org/index.php/Advanced_Linux_Sound_Architecture_%28%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%29#.E8.AE.BE.E7.BD.AE.E9.BB.98.E8.AE.A4.E5.A3.B0.E5.8D.A1
2.17 madplay
http://www.crystalradio.cn/thread-466848-1-1.html 
http://blog.csdn.net/fengliang191/article/details/19763579
madplay默認按鍵
```
The keyboard controls are documented in the man page for madplay:
    P  Pause; press any key to resume.
    S  Stop; press any key to replay the  current  file
       from the beginning.
    F  Forward; advance to the next file.
    B  Back;  replay  the  current  file, unless it has
       been playing for less than 4 seconds,  in  which
       case replay the previous file.
    T  Time display; change the time display mode. This
       only works with  -v  (--verbose).   The  display
       mode alternates among overall playing time, cur-
       rent time remaining, and current playing time.
    +  Increase gain; increase the audio output gain by
       0.5 dB.
    -  Decrease gain; decrease the audio output gain by
       0.5 dB.
    Q  Quit; stop decoding and exit.
root@mylinkit:~# madplay -h
Usage: madplay [OPTIONS] FILE [...]
Decode and play MPEG audio FILE(s).

Verbosity:
  -v, --verbose                show status while decoding
  -q, --quiet                  be quiet but show warnings
  -Q, --very-quiet             be quiet and do not show warnings
      --display-time=MODE      use default verbose time display MODE
                                 (remaining, current, overall)

Decoding:
      --downsample             reduce sample rate 2:1
  -i, --ignore-crc             ignore CRC errors
      --ancillary-output=PATH  write ancillary data to PATH

Audio output:
  -o, --output=[TYPE:]PATH     write output to PATH with format TYPE (below)
  -b, --bit-depth=DEPTH        request DEPTH bits per sample
  -R, --sample-rate=HERTZ      request HERTZ samples per second
  -d, --no-dither              do not dither output PCM samples
      --fade-in[=DURATION]     fade-in songs over DURATION (default 0:05)
  -a, --attenuate=DECIBELS     attenuate signal by DECIBELS (-)
  -a, --amplify=DECIBELS       amplify signal by DECIBELS (+)
  -A, --adjust-volume=DECIBELS override per-file volume adjustments
  -G, --replay-gain[=PROFILE]  enable Replay Gain volume adjustments using
                                 PROFILE (radio, audiophile)

Channel selection:
  -1, --left                   output first (left) channel only
  -2, --right                  output second (right) channel only
  -m, --mono                   mix left and right channels for monaural output
  -S, --stereo                 force stereo output

Playback:
  -s, --start=TIME             skip to begin at TIME (HH:MM:SS.DDD)
  -t, --time=DURATION          play only for DURATION (HH:MM:SS.DDD)
  -z, --shuffle                randomize file list
  -r, --repeat[=MAX]           play files MAX times, or indefinitely
      --tty-control            enable keyboard controls
      --no-tty-control         disable keyboard controls

Miscellaneous:
  -T, --show-tags-only         show ID3/encoder tags only (do not decode)
  -V, --version                display version number and exit
      --license                show copyright/license message and exit
  -h, --help                   display this help and exit

Supported output formats:
  cdda    CD audio, 16-bit big-endian 44100 Hz stereo PCM (*.cdr, *.cda)
  aiff    Audio IFF, [16-bit] PCM (*.aif, *.aiff)
  wave    Microsoft RIFF/WAVE, [16-bit] PCM (*.wav)
  snd     Sun/NeXT audio, 8-bit ISDN mu-law (*.au, *.snd)
  raw     binary [16-bit] host-endian linear PCM
  hex     ASCII hexadecimal [24-bit] linear PCM
  null    no output (decode only)
```  
2.17.1 C調用函數
參考文檔：http://blog.csdn.net/zouzuohuo/article/details/7895917
system("madplay north.mp3 &");//利用system函數調用madplay播放器播放*.mp3音樂
system("madplay north.mp3 -r &");//循環播放：參數-r
system("killall -9 madplay");//利用system函數調用killall命令將madplay終止掉 
system("killall -STOP madplay &");//利用system函數調用killall命令將madplay暫停
system("killall -CONT madplay &");//利用system函數調用killall命令恢復madplay的播放

killall -19 madplay"使進程掛起以暫停
killall -18 madplay"使進程恢復運行
killall -9 madplay"終止進程以停止。
2.17.2 madplay 播放網路音頻
參考文檔：https://wiki.openwrt.org/toh/freecom/fsg-3?s[]=madplay
```
cd /tmp
wget http://icy-e-bz-05-cr.sharp-stream.com/magic1054.mp3 -O - | madplay 
wget -O - http://u11aw.di.fm:80/di_goapsy | madplay -
wget -O - http://mp3stream1.apasf.apa.at:8000/ | madplay -
wget -O - http://hirschmilch.de:7000/psytrance.mp3 | madplay -
wget -O - http://64.236.34.97:80/stream/1014 | madplay -
$ wget–q–O– http://my_music.com/mystream | madplay -Q --no-tty-control- $ wget–q–O– http://my_music.com/mystream | madplay -Q --no-tty-control- $ wget–q–O– http://my_music.com/mystream | madplay -Q --no-tty-control- $ wget–q–O– http://my_music.com/mystream | madplay -Q --no-tty-control- 
```
2.17.3 顯示剩餘時間
```
madplay -v --display-time=remaining 001.mp3
madplay -v --display-time=current /tmp/mounts/USB-A1/music/*.mp3
madplay -v /tmp/mounts/USB-A1/music/*.mp3
```
2.17.4 -o 將mp3轉換成一個wav文件
```
$madplay /Media/SD-P1/moh/*.mp3 -o /tmp/tmp.wav
$madplay /Media/SD-P1/moh/*.mp3 -o /tmp/tmp.wav |aplay
| madplay - &
```
2.17.5 根據文件進行音樂播放
```
  http://www.epdoc.cn/qrs/18100.html

  root@mylinkit:/tmp# find /Media/SD-P1/moh/ -name "*.mp3" | sort >mp3.list
  root@mylinkit:/tmp# more mp3.list
  /Media/SD-P1/moh/001.mp3
  /Media/SD-P1/moh/002.mp3
  /Media/SD-P1/moh/003.mp3
  /Media/SD-P1/moh/001.mp3
  /Media/SD-P1/moh/002.mp3
  /Media/SD-P1/moh/003.mp3
  /Media/SD-P1/moh/004.mp3
  /Media/SD-P1/moh/005.mp3
  /Media/SD-P1/moh/006.mp3
  root@mylinkit:/tmp# madplay $(more mp3.list )

  example code:
    echo "sort the mp3 file and generate a mp3 list"
  find ./ -name "*.mp3"|sort>mp3.list
  /bin/echo "mp3.list:"
  more/mp3.list
  /bin/echo
  /bin/echo
  /bin/madplay$(more /mp3.list)
```
2.17.6 madplay管道控制方式 FIFO
參考文檔：https://www.cs.sfu.ca/CourseCentral/433/bfraser/other/2011-student-howtos/MadplayControlViaButtons.pdf
2.17.7 madplay音量控制
獲得喇叭的最大音量/最小音量/當前音量，運算後保存回去。
```
  MIN_VOLUME=$(amixer cget numid=11,iface=MIXER,name='Speaker Playback Volume' | grep '; type' |sed 's/^.*min=//g' | sed 's/,.*$//g')
  MAX_VOLUME=$(amixer cget numid=11,iface=MIXER,name='Speaker Playback Volume' | grep '; type' |sed 's/^.*max=//g' | sed 's/,.*$//g')
  ALSA_VOLUME=$(amixer cget numid=11,iface=MIXER,name='Speaker Playback Volume' | grep ': values' |sed 's/^.*values=//g' | sed 's/,.*$//g')
  let MAX_VOLUME-=8
  if [ "$ALSA_VOLUME" -le "$MAX_VOLUME" ]
  then
    let ALSA_VOLUME+=8
  fi
  #echo $ALSA_VOLUME >/dev/console; echo $MAX_VOLUME >/dev/console
  amixer cset numid=11,iface=MIXER,name='Speaker Playback Volume' $ALSA_VOLUME
```
2.17.8 參考文檔：
講解如何用按鍵控制madplay 
http://wenku.baidu.com/link?url=aSt7QMxrFFHZngf7rN2lZu2R8tldvJdXnRSl93SCf1xldTvVFfQ_77dsWF3-nb9gYa3_LBDmJXTNLQQR09rCuUT-ycWgL-Z7V-BG3EH7fKW
Openwrt下 mplayer的配置詳解 
http://www.crystalradio.cn/thread-466848-1-1.html
mp3播放器控制程式 
http://blog.sina.com.cn/s/blog_95268f5001016gnf.html
http://blog.csdn.net/zouzuohuo/article/details/7895917
2.18 swconfig
列出當前系統的存在的switch
```
root@ipRec:/etc/config# swconfig list
Found: switch0 - rt305x
```
展示當前switch連接埠配置
```
root@ipRec:/etc/config# swconfig dev rt305x show
Global attributes:
        enable_vlan: 0
        alternate_vlan_disable: 0
        bc_storm_protect: 0
        led_frequency: 0
Port 0:
        disable: 0
        doubletag: 1
        untag: 1
        led: 5
        lan: 1
        recv_bad: 0
        recv_good: 2479
        tr_bad: 0
        tr_good: 104
        pvid: 0
        link: port:0 link:up speed:100baseT full-duplex
Port 1:
        disable: 0
        doubletag: 1
        untag: 1
        led: 5
        lan: 1
        recv_bad: 0
        recv_good: 0
        tr_bad: 0
        tr_good: 0
        pvid: 0
        link: port:1 link:down
Port 2:
        disable: 0
        doubletag: 1
        untag: 1
        led: 5
        lan: 1
        recv_bad: 0
        recv_good: 0
        tr_bad: 0
        tr_good: 0
        pvid: 0
        link: port:2 link:down
Port 3:
        disable: 0
        doubletag: 1
        untag: 1
        led: 5
        lan: 1
        recv_bad: 0
        recv_good: 0
        tr_bad: 0
        tr_good: 0
        pvid: 0
        link: port:3 link:down
Port 4:
        disable: 0
        doubletag: 1
        untag: 1
        led: 5
        lan: 1
        recv_bad: 0
        recv_good: 0
        tr_bad: 0
        tr_good: 0
        pvid: 0
        link: port:4 link:down
Port 5:
        disable: 1
        doubletag: 1
        untag: 1
        led: ???
        lan: 1
        recv_bad: 0
        recv_good: 0
        tr_bad: 0
        tr_good: 0
        pvid: 0
        link: port:5 link:down
Port 6:
        disable: 0
        doubletag: 1
        untag: 1
        led: ???
        lan: ???
        recv_bad: ???
        recv_good: ???
        tr_bad: ???
        tr_good: ???
        pvid: 0
        link: port:6 link:up speed:1000baseT full-duplex
VLAN 0:
        ports: 0 1 2 3 4 5 6

root@ipRec:/etc/config# ifconfig
br-lan    Link encap:Ethernet  HWaddr 00:0C:43:E1:76:2A
          inet addr:192.168.100.1  Bcast:192.168.100.255  Mask:255.255.255.0
          inet6 addr: fe80::20c:43ff:fee1:762a/64 Scope:Link
          inet6 addr: fd83:d6c:cf85::1/60 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:903 errors:0 dropped:0 overruns:0 frame:0
          TX packets:306 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:63543 (62.0 KiB)  TX bytes:27616 (26.9 KiB)

eth0      Link encap:Ethernet  HWaddr 00:0C:43:E1:76:29
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1130 errors:0 dropped:0 overruns:0 frame:0
          TX packets:132 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:124403 (121.4 KiB)  TX bytes:11965 (11.6 KiB)
          Interrupt:5

eth0.1    Link encap:Ethernet  HWaddr 00:0C:43:E1:76:29
          inet6 addr: fe80::20c:43ff:fee1:7629/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:9 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:1931 (1.8 KiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:8736 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8736 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:594720 (580.7 KiB)  TX bytes:594720 (580.7 KiB)
```
2.19 網路配置
http://labs.mediatek.com/site/global/developer_tools/mediatek_linkit_smart_7688/training_docs/network/setup_wireless_router/index.gsp
2.20 gpio debug
可以通過#cat /sys/kernel/debug/gpio命令查詢當前按鈕狀態。lo,低電平，hi為高電平。
```
root@mylinkit:/# cat /sys/kernel/debug/gpio
GPIOs 0-31, platform/10000600.gpio, 10000600.gpio:
 gpio-11  (bootstrap           ) out lo
 gpio-14  (BTN_0               ) in  hi
 gpio-15  (BTN_1               ) in  hi
 gpio-16  (BTN_2               ) in  hi
 gpio-17  (BNT_3               ) in  hi
 gpio-18  (BTN_4               ) in  hi
 gpio-19  (S9                  ) in  hi

 GPIOs 32-63, platform/10000600.gpio, 10000600.gpio:
  gpio-38  (reset               ) in  hi

 GPIOs 64-95, platform/10000600.gpio, 10000600.gpio:

 GPIOs 127-127, platform/gpio-wifi, gpio-wifi:
  gpio-127 (mediatek:orange:wifi) out ?
```
2.21 環境變數顯示
環境變數的相關資訊，參考linux鳥歌私房菜上，P304。
2.22 稍描wifi熱點
```
# iwinfo ra0 scan 
# time iwlist wlan0 scan | grep ESSID
 root@mylinkit:/tmp# iwinfo ra0 scan
  Cell 01 - Address: 6C:E8:73:AB:0C:96
            ESSID: "FAST_AB0C96"
            Mode: Master  Channel: 1
            Signal: -256 dBm  Quality: 10/100
            Encryption: WPA2 PSK (AES-OCB)

  Cell 02 - Address: C8:3A:35:29:F5:54
            ESSID: "wanghf"
            Mode: Master  Channel: 1
            Signal: -256 dBm  Quality: 7/100
            Encryption: WPA PSK (AES-OCB)

  Cell 03 - Address: 00:06:25:00:6E:72
            ESSID: "home"
            Mode: Master  Channel: 6
            Signal: -256 dBm  Quality: 81/100
            Encryption: WPA2 PSK (TKIP, AES-OCB)

  Cell 04 - Address: 8C:21:0A:41:D3:64
            ESSID: "wf"
            Mode: Master  Channel: 11
            Signal: -256 dBm  Quality: 0/100
            Encryption: WPA2 PSK (AES-OCB)
```
2.23 du 查詢磁碟空間使用情況
```
du /
```
2.24 PID查詢命令ps, pidof, pgrep
2.25 date
```
http://www.runoob.com/linux/linux-comm-date.html 
http://www.2cto.com/os/201310/248416.html 
http://www.firefoxbug.com/index.php/archives/2799/ 
http://www.cnblogs.com/peida/archive/2012/12/13/2815687.html
date +%Y/%m/%d 
date +%H:%M
+%Y - year年 
+%m - month月 
+%d - day天 
+%H - Hour時 
+%M - Minute分 
+%S - Second秒 
+%s - 從 1970 年 1 月 1 日 00:00:00 UTC 到目前為止的秒數 
%H : 小時(00..23) 
%I : 小時(01..12) 
%k : 小時(0..23) 
%l : 小時(1..12) 
%M : 分鐘(00..59) 
%p : 顯示本地 AM 或 PM 
%r : 直接顯示時間 (12 小時制，格式為 hh:mm:ss [AP]M) 
%s : 從 1970 年 1 月 1 日 00:00:00 UTC 到目前為止的秒數 
%S : 秒(00..61) 
%T : 直接顯示時間 (24 小時制) 
%X : 相當於 %H:%M:%S 
%Z : 顯示時區 %a : 星期幾 (Sun..Sat) 
%A : 星期幾 (Sunday..Saturday) 
%b : 月份 (Jan..Dec) 
%B : 月份 (January..December) 
%c : 直接顯示日期與時間 
%d : 日 (01..31) 
%D : 直接顯示日期 (mm/dd/yy) 
%h : 同 %b 
%j : 一年中的第幾天 (001..366) 
%m : 月份 (01..12) 
%U : 一年中的第幾周 (00..53) (以 Sunday 為一週的第一天的情形) 
%w : 一週中的第幾天 (0..6) 
%W : 一年中的第幾周 (00..53) (以 Monday 為一週的第一天的情形) 
%x : 直接顯示日期 (mm/dd/yy) 
%y : 年份的最後兩位數字 (00.99) 
%Y : 完整年份 (0000..9999)
date指定格式輸出 
$ date +」%Y-%m-%d %H:%M:%S」 
2014-11-21 23:59:37
轉換指定日期為Unix時間戳： 
$ date -d 「2008-01-01 00:00:00」 +%s 
1199116800
$ date -d 2008-01-01 +%s
1199116800
```
```
$ date -d 20080101 +%s
1199116800
```
例外: 有一種場景date格式是連續的(沒找到date命令怎麼轉換成unix)
```
$ echo 20080101010101 | awk '{print substr($0,1,4)"-"substr($0,5,2)"-"substr($0,7,2)" "substr($0,9,2)":"substr($0,11,2)":"substr($0,13,2) }'
2008-01-01 01:01:01

$ date -d "2008-01-01 01:01:01" +%s
1199120461
root@mylinkit:/etc/config# date -help 
date: invalid option – h 
BusyBox v1.23.2 (2016-01-20 23:54:03 CST) multi-call binary.
Usage: date [OPTIONS] [+FMT] [TIME]
Display time (using +FMT), or set time
    [-s,--set] TIME Set time to TIME
    -u,--utc        Work in UTC (don't convert to local time)
    -R,--rfc-2822   Output RFC-2822 compliant date string
    -I[SPEC]        Output ISO-8601 compliant date string
                    SPEC='date' (default) for date only,
                    'hours', 'minutes', or 'seconds' for date and
                    time to the indicated precision
    -r,--reference FILE     Display last modification time of FILE
    -d,--date TIME  Display TIME, not 'now'
    -D FMT          Use FMT for -d TIME conversion
    -k              Set Kernel timezone from localtime and exit
Recognized TIME formats: 
hh:mm[:ss] 
[YYYY.]MM.DD-hh:mm[:ss] 
YYYY-MM-DD hh:mm[:ss] 
[[[[[YY]YY]MM]DD]hh]mm[.ss]
```
2.26 grep,sed,cut
參考moh-scheduler文檔
```
  # SD10022016&ED31012016&DW1111100&TS1015TE1730
  start_day=$(cat $config_file |sed 's/^.*SD//g'|cut -c -8)
  cut切除指定的字元
  cut -c 1-8 //切除第1到第8字元
```  
2.27 wait
https://zh.wikipedia.org/wiki/Wait_(%E5%91%BD%E4%BB%A4)
2.28 ubus
```
  root@mylinkit:~# ubus --help
  ubus: invalid option -- -
  Usage: ubus [<options>] <command> [arguments...]
  Options:
   -s <socket>:           Set the unix domain socket to connect to
   -t <timeout>:          Set the timeout (in seconds) for a command to complete
   -S:                    Use simplified output (for scripts)
   -v:                    More verbose output

  Commands:
   - list [<path>]                        List objects
   - call <path> <method> [<message>]     Call an object method
   - listen [<path>...]                   Listen for events
   - send <type> [<message>]              Send an event
   - wait_for <object> [<object>...]      Wait for multiple objects to appear on ubus


  root@mylinkit:~# ubus list
  dhcp
  iwinfo
  log
  network
  network.device
  network.interface
  network.interface.lan
  network.interface.loopback
  network.interface.wan
  network.wireless
  rpc-sys
  service
  session
  system
  uci

  root@mylinkit:~# ubus list -v
  'dhcp' @d5aa2d81
        "ipv4leases":{}
        "ipv6leases":{}
  'iwinfo' @804494b9
        "devices":{}
        "info":{"device":"String"}
        "scan":{"device":"String"}
        "assoclist":{"device":"String","mac":"String"}
        "freqlist":{"device":"String"}
        "txpowerlist":{"device":"String"}
        "countrylist":{"device":"String"}
        "phyname":{"section":"String"}
  'log' @e7e97da6
        "read":{"lines":"Integer"}
        "write":{"event":"String"}
  'network' @06d3dcba
        "restart":{}
        "reload":{}
        "add_host_route":{"target":"String","v6":"Boolean","interface":"String"}
        "get_proto_handlers":{}
        "add_dynamic":{"name":"String"}
  'network.device' @9b47eb98
        "status":{"name":"String"}
        "set_alias":{"alias":"Array","device":"String"}
        "set_state":{"name":"String","defer":"Boolean"}
  'network.interface' @c806e5d7
        "up":{}
        "down":{}
        "status":{}
        "prepare":{}
        "dump":{}
        "add_device":{"name":"String","link-ext":"Boolean"}
        "remove_device":{"name":"String","link-ext":"Boolean"}
        "notify_proto":{}
        "remove":{}
        "set_data":{}
  'network.interface.lan' @da711a3b
        "up":{}
        "down":{}
        "status":{}
        "prepare":{}
        "dump":{}
        "add_device":{"name":"String","link-ext":"Boolean"}
        "remove_device":{"name":"String","link-ext":"Boolean"}
        "notify_proto":{}
        "remove":{}
        "set_data":{}
  'network.interface.loopback' @eaf974e8
        "up":{}
        "down":{}
        "status":{}
        "prepare":{}
        "dump":{}
        "add_device":{"name":"String","link-ext":"Boolean"}
        "remove_device":{"name":"String","link-ext":"Boolean"}
        "notify_proto":{}
        "remove":{}
        "set_data":{}
  'network.interface.wan' @eff0e141
        "up":{}
        "down":{}
        "status":{}
        "prepare":{}
        "dump":{}
        "add_device":{"name":"String","link-ext":"Boolean"}
        "remove_device":{"name":"String","link-ext":"Boolean"}
        "notify_proto":{}
        "remove":{}
        "set_data":{}
  'network.wireless' @a8161143
        "up":{}
        "down":{}
        "status":{}
        "notify":{}
        "get_validate":{}
  'rpc-sys' @dd844b8f
        "password_set":{"user":"String","password":"String"}
        "upgrade_test":{}
        "upgrade_start":{"keep":"Boolean"}
        "upgrade_clean":{}
        "factory":{}
        "reboot":{}
  'service' @1312b281
        "set":{"name":"String","script":"String","instances":"Table","triggers":"Array","validate":"Array"}
        "add":{"name":"String","script":"String","instances":"Table","triggers":"Array","validate":"Array"}
        "list":{"name":"String","verbose":"Boolean"}
        "delete":{"name":"String","instance":"String"}
        "update_start":{"name":"String"}
        "update_complete":{"name":"String"}
        "event":{"type":"String","data":"Table"}
        "validate":{"package":"String","type":"String","service":"String"}
        "get_data":{"name":"String","instance":"String","type":"String"}
  'session' @4417ac78
        "create":{"timeout":"Integer"}
        "list":{"ubus_rpc_session":"String"}
        "grant":{"ubus_rpc_session":"String","scope":"String","objects":"Array"}
        "revoke":{"ubus_rpc_session":"String","scope":"String","objects":"Array"}
        "access":{"ubus_rpc_session":"String","scope":"String","object":"String","function":"String"}
        "set":{"ubus_rpc_session":"String","values":"Table"}
        "get":{"ubus_rpc_session":"String","keys":"Array"}
        "unset":{"ubus_rpc_session":"String","keys":"Array"}
        "destroy":{"ubus_rpc_session":"String"}
        "login":{"username":"String","password":"String","timeout":"Integer"}
  'system' @5bc7fd25
        "board":{}
        "info":{}
        "upgrade":{}
        "watchdog":{"frequency":"Integer","timeout":"Integer","stop":"Boolean"}
        "signal":{"pid":"Integer","signum":"Integer"}
        "nandupgrade":{"path":"String"}
  'uci' @2fd66254
        "configs":{}
        "get":{"config":"String","section":"String","option":"String","type":"String","match":"Table","ubus_rpc_session":"String"}
        "state":{"config":"String","section":"String","option":"String","type":"String","match":"Table","ubus_rpc_session":"String"}
        "add":{"config":"String","type":"String","name":"String","values":"Table","ubus_rpc_session":"String"}
        "set":{"config":"String","section":"String","type":"String","match":"Table","values":"Table","ubus_rpc_session":"String"}
        "delete":{"config":"String","section":"String","type":"String","match":"Table","option":"String","options":"Array","ubus_rpc_session":"String"}
        "rename":{"config":"String","section":"String","option":"String","name":"String","ubus_rpc_session":"String"}
        "order":{"config":"String","sections":"Array","ubus_rpc_session":"String"}
        "changes":{"config":"String","ubus_rpc_session":"String"}
        "revert":{"config":"String","ubus_rpc_session":"String"}
        "commit":{"config":"String","ubus_rpc_session":"String"}
        "apply":{"rollback":"Boolean","timeout":"Integer","ubus_rpc_session":"String"}
        "confirm":{"ubus_rpc_session":"String"}
        "rollback":{"ubus_rpc_session":"String"}
        "reload_config":{}
```
3. openwrt application
3.1 opkg
3.2 date
```
  root@mylinkit:/etc/config# date -help
  date: invalid option -- h
  BusyBox v1.23.2 (2016-01-20 23:54:03 CST) multi-call binary.

  Usage: date [OPTIONS] [+FMT] [TIME]

  Display time (using +FMT), or set time

        [-s,--set] TIME Set time to TIME
        -u,--utc        Work in UTC (don't convert to local time)
        -R,--rfc-2822   Output RFC-2822 compliant date string
        -I[SPEC]        Output ISO-8601 compliant date string
                        SPEC='date' (default) for date only,
                        'hours', 'minutes', or 'seconds' for date and
                        time to the indicated precision
        -r,--reference FILE     Display last modification time of FILE
        -d,--date TIME  Display TIME, not 'now'
        -D FMT          Use FMT for -d TIME conversion
        -k              Set Kernel timezone from localtime and exit

  Recognized TIME formats:
        hh:mm[:ss]
        [YYYY.]MM.DD-hh:mm[:ss]
        YYYY-MM-DD hh:mm[:ss]
        [[[[[YY]YY]MM]DD]hh]mm[.ss]
```
3.3 稍描wifi熱點
```
  # iwinfo ra0 scan
  # time iwlist wlan0 scan | grep ESSID

  root@mylinkit:/tmp# iwinfo ra0 scan
  Cell 01 - Address: 6C:E8:73:AB:0C:96
            ESSID: "FAST_AB0C96"
            Mode: Master  Channel: 1
            Signal: -256 dBm  Quality: 10/100
            Encryption: WPA2 PSK (AES-OCB)

  Cell 02 - Address: C8:3A:35:29:F5:54
            ESSID: "wanghf"
            Mode: Master  Channel: 1
            Signal: -256 dBm  Quality: 7/100
            Encryption: WPA PSK (AES-OCB)

  Cell 03 - Address: 00:06:25:00:6E:72
            ESSID: "home"
            Mode: Master  Channel: 6
            Signal: -256 dBm  Quality: 81/100
            Encryption: WPA2 PSK (TKIP, AES-OCB)

  Cell 04 - Address: 8C:21:0A:41:D3:64
            ESSID: "wf"
            Mode: Master  Channel: 11
            Signal: -256 dBm  Quality: 0/100
            Encryption: WPA2 PSK (AES-OCB)
```
3.4 alsamixer,amixer 音量調節
alsamixer是文本方式下的圖形命令
amixer是文本方式下的文本命令
```
amixer
Simple mixer control 'Headphone',0
  Capabilities: pvolume
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 127
  Mono:
  Front Left: Playback 121 [95%] [0.00dB]
  Front Right: Playback 121 [95%] [0.00dB]
Simple mixer control 'Headphone Playback ZC',0
  Capabilities: pswitch
  Playback channels: Front Left - Front Right
  Mono:
  Front Left: Playback [on]
  Front Right: Playback [on]
Simple mixer control 'Speaker',0
  Capabilities: pvolume
  Playback channels: Front Left - Front Right
  Limits: Playback 0 - 127
  Mono:
  Front Left: Playback 121 [95%] [0.00dB]
  Front Right: Playback 121 [95%] [0.00dB]
Simple mixer control 'Speaker AC',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 5
  Mono: 4 [80%]
Simple mixer control 'Speaker DC',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 5
  Mono: 5 [100%]
Simple mixer control 'Speaker Playback ZC',0
  Capabilities: pswitch
  Playback channels: Front Left - Front Right
  Mono:
  Front Left: Playback [off]
  Front Right: Playback [off]
Simple mixer control 'PCM Playback -6dB',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'Mono Output Mixer Left',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Mono Output Mixer Right',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Playback',0
  Capabilities: volume
  Playback channels: Front Left - Front Right
  Capture channels: Front Left - Front Right
  Limits: 0 - 255
  Front Left: 243 [95%] [-5.50dB]
  Front Right: 243 [95%] [-5.50dB]
Simple mixer control 'Capture',0
  Capabilities: cvolume cswitch
  Capture channels: Front Left - Front Right
  Limits: Capture 0 - 63
  Front Left: Capture 43 [68%] [-75.50dB] [off]
  Front Right: Capture 43 [68%] [-75.50dB] [off]
Simple mixer control '3D',0
  Capabilities: volume volume-joined pswitch pswitch-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 15
  Mono: 0 [0%] Playback [off]
Simple mixer control '3D Filter Lower Cut-Off',0
  Capabilities: enum
  Items: 'Low' 'High'
  Item0: 'Low'
Simple mixer control '3D Filter Upper Cut-Off',0
  Capabilities: enum
  Items: 'High' 'Low'
  Item0: 'High'
Simple mixer control 'ADC High Pass Filter',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'ADC PCM',0
  Capabilities: cvolume
  Capture channels: Front Left - Front Right
  Limits: Capture 0 - 255
  Front Left: Capture 206 [81%] [6.00dB]
  Front Right: Capture 206 [81%] [6.00dB]
Simple mixer control 'ADC Polarity',0
  Capabilities: enum
  Items: 'No Inversion' 'Left Inverted' 'Right Inverted' 'Stereo Inversion'
  Item0: 'No Inversion'
Simple mixer control 'ALC Attack',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 15
  Mono: 2 [13%]
Simple mixer control 'ALC Decay',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 15
  Mono: 3 [20%]
Simple mixer control 'ALC Function',0
  Capabilities: enum
  Items: 'Off' 'Right' 'Left' 'Stereo'
  Item0: 'Off'
Simple mixer control 'ALC Hold Time',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 15
  Mono: 0 [0%]
Simple mixer control 'ALC Max Gain',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 7 [100%]
Simple mixer control 'ALC Min Gain',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 0 [0%]
Simple mixer control 'ALC Mode',0
  Capabilities: enum
  Items: 'ALC' 'Limiter'
  Item0: 'ALC'
Simple mixer control 'ALC Target',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 15
  Mono: 4 [27%]
Simple mixer control 'DAC Deemphasis',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'DAC Polarity',0
  Capabilities: enum
  Items: 'No Inversion' 'Left Inverted' 'Right Inverted' 'Stereo Inversion'
  Item0: 'No Inversion'
Simple mixer control 'Left Boost Mixer LINPUT1',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Left Boost Mixer LINPUT2',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Left Boost Mixer LINPUT3',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'Left Input Boost Mixer LINPUT2',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 0 [0%] [-99999.99dB]
Simple mixer control 'Left Input Boost Mixer LINPUT3',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 0 [0%] [-99999.99dB]
Simple mixer control 'Left Input Mixer Boost',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Left Output Mixer Boost Bypass',0
  Capabilities: volume volume-joined pswitch pswitch-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 2 [29%] [-15.00dB] Playback [off]
Simple mixer control 'Left Output Mixer LINPUT3',0
  Capabilities: volume volume-joined pswitch pswitch-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 7 [100%] [0.00dB] Playback [off]
Simple mixer control 'Left Output Mixer PCM',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Noise Gate',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'Noise Gate Threshold',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 31
  Mono: 0 [0%]
Simple mixer control 'Right Boost Mixer RINPUT1',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Right Boost Mixer RINPUT2',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Right Boost Mixer RINPUT3',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [off]
Simple mixer control 'Right Input Boost Mixer RINPUT2',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 0 [0%] [-99999.99dB]
Simple mixer control 'Right Input Boost Mixer RINPUT3',0
  Capabilities: volume volume-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 0 [0%] [-99999.99dB]
Simple mixer control 'Right Input Mixer Boost',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Right Output Mixer Boost Bypass',0
  Capabilities: volume volume-joined pswitch pswitch-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 2 [29%] [-15.00dB] Playback [off]
Simple mixer control 'Right Output Mixer PCM',0
  Capabilities: pswitch pswitch-joined
  Playback channels: Mono
  Mono: Playback [on]
Simple mixer control 'Right Output Mixer RINPUT3',0
  Capabilities: volume volume-joined pswitch pswitch-joined
  Playback channels: Mono
  Capture channels: Mono
  Limits: 0 - 7
  Mono: 7 [100%] [0.00dB] Playback [off]
amixer controls
numid=10,iface=MIXER,name='Headphone Playback ZC Switch'
numid=9,iface=MIXER,name='Headphone Playback Volume'
numid=15,iface=MIXER,name='PCM Playback -6dB Switch'
numid=39,iface=MIXER,name='Mono Output Mixer Left Switch'
numid=40,iface=MIXER,name='Mono Output Mixer Right Switch'
numid=17,iface=MIXER,name='ADC High Pass Filter Switch'
numid=34,iface=MIXER,name='ADC PCM Capture Volume'
numid=16,iface=MIXER,name='ADC Polarity'
numid=2,iface=MIXER,name='Capture Volume ZC Switch'
numid=3,iface=MIXER,name='Capture Switch'
numid=1,iface=MIXER,name='Capture Volume'
numid=8,iface=MIXER,name='Playback Volume'
numid=21,iface=MIXER,name='3D Filter Lower Cut-Off'
numid=20,iface=MIXER,name='3D Filter Upper Cut-Off'
numid=23,iface=MIXER,name='3D Switch'
numid=22,iface=MIXER,name='3D Volume'
numid=31,iface=MIXER,name='ALC Attack'
numid=30,iface=MIXER,name='ALC Decay'
numid=24,iface=MIXER,name='ALC Function'
numid=28,iface=MIXER,name='ALC Hold Time'
numid=25,iface=MIXER,name='ALC Max Gain'
numid=27,iface=MIXER,name='ALC Min Gain'
numid=29,iface=MIXER,name='ALC Mode'
numid=26,iface=MIXER,name='ALC Target'
numid=19,iface=MIXER,name='DAC Deemphasis Switch'
numid=18,iface=MIXER,name='DAC Polarity'
numid=54,iface=MIXER,name='Left Boost Mixer LINPUT1 Switch'
numid=52,iface=MIXER,name='Left Boost Mixer LINPUT2 Switch'
numid=53,iface=MIXER,name='Left Boost Mixer LINPUT3 Switch'
numid=7,iface=MIXER,name='Left Input Boost Mixer LINPUT2 Volume'
numid=6,iface=MIXER,name='Left Input Boost Mixer LINPUT3 Volume'
numid=48,iface=MIXER,name='Left Input Mixer Boost Switch'
numid=46,iface=MIXER,name='Left Output Mixer Boost Bypass Switch'
numid=35,iface=MIXER,name='Left Output Mixer Boost Bypass Volume'
numid=45,iface=MIXER,name='Left Output Mixer LINPUT3 Switch'
numid=36,iface=MIXER,name='Left Output Mixer LINPUT3 Volume'
numid=44,iface=MIXER,name='Left Output Mixer PCM Playback Switch'
numid=33,iface=MIXER,name='Noise Gate Switch'
numid=32,iface=MIXER,name='Noise Gate Threshold'
numid=51,iface=MIXER,name='Right Boost Mixer RINPUT1 Switch'
numid=49,iface=MIXER,name='Right Boost Mixer RINPUT2 Switch'
numid=50,iface=MIXER,name='Right Boost Mixer RINPUT3 Switch'
numid=5,iface=MIXER,name='Right Input Boost Mixer RINPUT2 Volume'
numid=4,iface=MIXER,name='Right Input Boost Mixer RINPUT3 Volume'
numid=47,iface=MIXER,name='Right Input Mixer Boost Switch'
numid=43,iface=MIXER,name='Right Output Mixer Boost Bypass Switch'
numid=37,iface=MIXER,name='Right Output Mixer Boost Bypass Volume'
numid=41,iface=MIXER,name='Right Output Mixer PCM Playback Switch'
numid=42,iface=MIXER,name='Right Output Mixer RINPUT3 Switch'
numid=38,iface=MIXER,name='Right Output Mixer RINPUT3 Volume'
numid=14,iface=MIXER,name='Speaker AC Volume'
numid=13,iface=MIXER,name='Speaker DC Volume'
numid=11,iface=MIXER,name='Speaker Playback Volume'
numid=12,iface=MIXER,name='Speaker Playback ZC Switch'

numid=8,iface=MIXER,name='Playback Volume'
numid=9,iface=MIXER,name='Headphone Playback Volume'
numid=11,iface=MIXER,name='Speaker Playback Volume'
sed參考文檔：Linux鳥歌的私房菜 P359
獲得當前喇叭音量值
# amixer cget numid=11,iface=MIXER,name='Speaker Playback Volume' | grep ': values' |sed 's/^.*values=//g' | sed 's/,.*$//g'
獲得耳機音量值
# amixer cget numid=9,iface=MIXER,name='Headphone Playback Volume' | grep ': values' |sed 's/^.*values=//g' | sed 's/,.*$//g'
獲得播放音量值
# amixer cget numid=8,iface=MIXER,name='Playback Volume' | grep ': values' |sed 's/^.*values=//g' | sed 's/,.*$//g'
```
3.5 top
3.6 ps
```
Mem: 41608K used, 84840K free, 320K shrd, 4332K buff, 11960K cached
CPU:   0% usr   0% sys   0% nic  99% idle   0% io   0% irq   0% sirq
Load average: 0.00 0.01 0.05 2/43 1864
  PID  PPID USER     STAT   VSZ %VSZ %CPU COMMAND
 1581  1191 root     S     1240   1%   0% /usr/sbin/dropbear -F -P /var/run/dro
 1331     1 root     S     1016   1%   0% /sbin/mountd -f
 1299     1 root     S     3188   3%   0% /usr/sbin/nmbd -F
 1298     1 root     S     3096   2%   0% /usr/sbin/smbd -F
 1088     1 root     S     1824   1%   0% /sbin/rpcd
 1306     1 nobody   S     1768   1%   0% avahi-daemon: running [mylinkit.local
 1267     1 root     S     1640   1%   0% /usr/sbin/uhttpd -f -h /www -r mylink
 1122     1 root     S     1600   1%   0% /sbin/netifd
 1582  1581 root     S     1496   1%   0% -ash
 1401     1 root     S     1488   1%   0% /usr/sbin/ntpd -n -S /usr/sbin/ntpd-h
 1602  1601 root     S     1488   1%   0% -ash
 1864  1582 root     R     1488   1%   0% top
 1504  1122 root     S     1484   1%   0% udhcpc -p /var/run/udhcpc-apcli0.pid
    1     0 root     S     1436   1%   0% /sbin/procd
 1601  1191 root     S     1240   1%   0% /usr/sbin/dropbear -F -P /var/run/dro
 1160     1 root     S     1192   1%   0% /usr/sbin/odhcpd
 1191     1 root     S     1148   1%   0% /usr/sbin/dropbear -F -P /var/run/dro
 1079     1 root     S     1056   1%   0% /sbin/logd -S 16
 1572     1 nobody   S      992   1%   0% /usr/sbin/dnsmasq -C /var/etc/dnsmasq
  430     1 root     S      904   1%   0% /sbin/ubusd
```
3.7 iwpriv
```
root@mylinkit:/tmp# iwpriv -help
Usage: iwpriv interface [private-command [private-arguments]]
root@mylinkit:/tmp# iwpriv
eth0.1    no private ioctls.
lo        no private ioctls.
ra0       Available private ioctls :
          set              (8BE2) : set 1536 char  & get   0
          show             (8BF1) : set 1024 char  & get   0
          get_site_survey  (8BED) : set   0       & get 1024 char
          set_wsc_oob      (8BF9) : set 1024 char  & get 1024 char
          get_mac_table    (8BEF) : set 1024 char  & get 1024 char
          e2p              (8BE7) : set 1024 char  & get 1024 char
          bbp              (8BE3) : set 1024 char  & get 1024 char
          mac              (8BE5) : set 1024 char  & get 1024 char
          rf               (8BF3) : set 1024 char  & get 1024 char
          get_wsc_profile  (8BF2) : set 1024 char  & get 1024 char
          get_ba_table     (8BF6) : set 1024 char  & get 1024 char
          stat             (8BE9) : set 1024 char  & get 1024 char

apcli1    Available private ioctls :
          set              (8BE2) : set 1536 char  & get   0
          show             (8BF1) : set 1024 char  & get   0
          get_site_survey  (8BED) : set   0       & get 1024 char
          set_wsc_oob      (8BF9) : set 1024 char  & get 1024 char
          get_mac_table    (8BEF) : set 1024 char  & get 1024 char
          e2p              (8BE7) : set 1024 char  & get 1024 char
          bbp              (8BE3) : set 1024 char  & get 1024 char
          mac              (8BE5) : set 1024 char  & get 1024 char
          rf               (8BF3) : set 1024 char  & get 1024 char
          get_wsc_profile  (8BF2) : set 1024 char  & get 1024 char
          get_ba_table     (8BF6) : set 1024 char  & get 1024 char
          stat             (8BE9) : set 1024 char  & get 1024 char

eth0      no private ioctls.

apcli0    Available private ioctls :
          set              (8BE2) : set 1536 char  & get   0
          show             (8BF1) : set 1024 char  & get   0
          get_site_survey  (8BED) : set   0       & get 1024 char
          set_wsc_oob      (8BF9) : set 1024 char  & get 1024 char
          get_mac_table    (8BEF) : set 1024 char  & get 1024 char
          e2p              (8BE7) : set 1024 char  & get 1024 char
          bbp              (8BE3) : set 1024 char  & get 1024 char
          mac              (8BE5) : set 1024 char  & get 1024 char
          rf               (8BF3) : set 1024 char  & get 1024 char
          get_wsc_profile  (8BF2) : set 1024 char  & get 1024 char
          get_ba_table     (8BF6) : set 1024 char  & get 1024 char
          stat             (8BE9) : set 1024 char  & get 1024 char
br-lan    no private ioctls.

/lib/netifd/wireless/ralink.sh 
* iwpriv ra0 
* set 
* Channel 
* NoForwarding 
* NoForwardingBTNBSSID 
* NoForwardingMBCast 
* HideSSID 
* RADIUS_Server 
* RADIUS_Port 
* RADIUS_Key 
* own_ip_addr 
* EAPifname 
* PreAuthIfname 
* AuthMode 
* EncrypType 
* IEEE8021X 
* 「SSID=ssid」?「WPAPSK={key} 
* DefaultKeyID=2 
* AuthMode=WEPAUTO 
* EncrypType=WEP 
* IEEE8021X=0 
* DefaultKeyID=key?WscConfMode=wsc_mode 
* WscConfStatus=2 
* WscMode=2 
* ACLClearAll=1 
* ACLAddEntry=」$m」 
* AccessPolicy=0,1,2
# iwpriv ra0 set Channel=6
1
```
3.8 miniDLNA
https://wiki.openwrt.org/doc/uci/minidlna 
https://github.com/xiongyihui/LinkIt_Smart_7688
Openwrt下安裝miniDLNA
```
root@OpenWrt:~# opkg update
root@OpenWrt:~# opkg install minidlna
root@mylinkit:~# opkg install minidlna
Installing minidlna (1.1.4-2) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/minidlna_1.1.4-2_ramips_24kec.ipk.
Installing libexif (0.6.21-1) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/libexif_0.6.21-1_ramips_24kec.ipk.
Installing libffmpeg-mini (2.6.2-1) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/libffmpeg-mini_2.6.2-1_ramips_24kec.ipk.
Installing libflac (1.3.1-1) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/libflac_1.3.1-1_ramips_24kec.ipk.
Installing libvorbis (1.3.5-1) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/libvorbis_1.3.5-1_ramips_24kec.ipk.
Installing libogg (1.3.2-2) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/packages/libogg_1.3.2-2_ramips_24kec.ipk.
Installing libuuid (2.25.2-4) to root...
Downloading http://downloads.openwrt.org/chaos_calmer/15.05.1/ramips/mt7688/packages/base/libuuid_2.25.2-4_ramips_24kec.ipk.
Configuring libogg.
Configuring libexif.
Configuring libflac.
Configuring libvorbis.
Configuring libuuid.
Configuring libffmpeg-mini.
Configuring minidlna.
```
Ubuntu下安裝miniDLNAhttp://blog.csdn.net/wanruirui/article/details/14222283
1，安裝
```
$ sudo apt-get install minidlna
```
2，修改配置
```
$ sudo vi /etc/minidlna.conf
```
3、你可以選擇讓minidlna隨機啟動
```
$ sudo update-rc.d minidlna defaults
```
4、啟動minidlna服務
```
$ sudo service minidlna start
```
5、當你修改配置文件及媒體資源更新時，需要強制刷新，以便minidlna將最新的媒體文件進行索引
```
sudo service minidlna force-reload
```
6、查看資源個數
http://192.168.1.106:8200/
7、取消minidlna的開機自動啟動
```
sudo update-rc.d -f minidlna remove
```
8、停止minidlna服務
```
sudo service minidlna stop
```
9、停止minidlna所有進程
```
sudo killall minidlna
```
10、卸載minidlna
```
sudo apt-get remove --purge minidlna
```
3.9 which/find
which用來查找可執行文件，find用來查找文件。另外，還有whereis,locate，不過在OpenWrt中默認沒有這兩個命令。
```
root@mylinkit:/# which which
/usr/bin/which
```
3.10 網路工具 //net-tools, iproute2, vlan, bridge-utils, wireless-tools
3.11 huawei 4g
```
kmod-usb-serial
kmod-usb-serial-option
kmod-usb-serial-wwan

usb-modeswitch
kmod-mii
kmod-usb-net
kmod-usb-wdm
kmod-usb-net-qmi-wwan
usb-modeswitch-data
uqmi

kmod-usb-net-huawei-cdc-ncm
```
uart
開兩個shell,一端:cat /dev/ttyS0,另一端: echo 1111 >/dev/ttyS0

4. linux application
在ubuntu環境下，需要安裝下面的安裝包用來編譯openwrt。
```
sudo apt-get install git g++ make libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip wget python xz-utils
```
4.1 openssh-service
SSH服務是一個非常好的服務，採用加密方式進行文件傳輸。該服務可以替代telnet的明文連接，並且可以實現文件加密傳輸(scp)。
4.2 vnc server
在ubuntu12系統環境下
vnc server安裝
```
$ sudo apt-get install vnc4server
```
設置vnc Password
啟動VNC Server
```
$ vncserver
```
關閉一個VNC窗口
```
$ vncserver -kill :1
```
安裝gnome
```
apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
4.3 git
https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E6%92%A4%E6%B6%88%E6%93%8D%E4%BD%9C
```
git command**
git clone
git reset HEAD^
git reset HEAD^^
git reset HEAD~3/1
git reset -hard origin/master // 回退到遠端最新版本
git remote add github https://github.com/xxxx/openwrt.git
git remote -v
git checkout -b huang
git branch
git pull github huang:master // 從遠端github拉出huang分支到本地的master
git push github huang:master // 上傳本地的huang分支到github遠端的master
git merge
```
基礎命令：撤銷沒有提交修改
```
$ git checkout -- config-3.18
分支操作：合併master到分支
  git pull origon master    // 從遠端伺服器更新master分支
  git checkout IR077H       // 切換到IR077H分支
  git merge Master          // 合併Master分支到當前分支
```
庫：創建本地 git 庫 example.git
```
$ cd /opt/git
$ mkdir example.git
$ cd example.git
$ git --bare init
```
庫：clone本地git庫
```
$ git clone /opt/git/example.git
```
庫：clone ssh遠端庫
```
$ git clone git@192.168.1.1:/opt/git/example.git
```
庫；clone github庫
```
# git clone https://github.com/MediaTek-Labs/linkit-smart-7688-feed.git
```
4.3.7 從伺服器更新本地文檔
```
$ git pull origin master:master
$ git pull origin IR077H:IR077H
```
分支管理
創建分支並切換到分支
```
$ git checkout -b moh
```
分支切換
```
$ git checkout moh
```
分支合併 //合併master到moh分支
```
$ git checkout moh  
$ git merge master  
```

圖形界面GitK
```
$ gitk
```
gitk是linux下git自帶的一個圖形顯示工具。可以使用這個工具在圖形模式下察看詳細的log文件等資訊。
4.4 串口通訊
screen
ubuntu系統中使用如何使用RS232通訊，在系統中，可以採用screen命令。
```
$ ls /dev/ttyUSB*
$ sudo apt-get install screen
$ sudo screen /dev/ttyUSB0 57600
```
4.5 tftp server
在openwrt系統更新環節中，有多種方法可以實現firmware更新。tftp方式就是一個方法。我們可以在ubuntu中創建一個tftp server，這樣uboot就可以通過網線直接更新firmware了。這是一個非常簡單的方式。
```
sudo apt-get install tftpd-hpa
config /etc/default/tftpd-hpa
start server /etc/init.d/tftpd-hpa start or start tftp-hpa
stop server /etc/init.d/tftpd-hpa stop or stop tftp-hpa
```
4.5.1 安裝下面的安裝包
```
$ sudo apt-get install xinetd tftpd tftp
```
4.5.2 創建/etc/xinetd.d/tftp並且put this entry
```
service tftp
{
protocol        = udp
port            = 69
socket_type     = dgram
wait            = yes
user            = nobody
server          = /usr/sbin/in.tftpd
server_args     = /tftpboot
disable         = no
}
```
4.6 scp(secure copy)安全文件傳輸
Secure copy or SCP is a means of securely transferring computer files between a local host and a remote host or between two remote hosts. It is based on the Secure Shell (SSH) protocol.[1]
```
 scp ~/.ssh/id_dsa.pub root@192.168.1.1:/tmp
```
4.7 重定向 0，1，2 >&1,>&2
0 是 < 的預設值，因此 < 與 0<是一樣的;同理，> 與 1> 是一樣的
標準輸入(stdin):代碼為0，使用<或<<；
標準輸入(stdout):代碼為1，使用>或>>；
標準錯誤輸出(stderr)：代碼為2，使用2>或2>>。 
```
0:Standard Input(STDIN) 
1:Standard Output(STDOUT) 
2:Standard Error Output(STDERR) 
http://blog.csdn.net/thirstyblue/article/details/7974300 
http://www.cnblogs.com/Centaurus/archive/2013/05/25/3098256.html
 $ls /dev 1>filename         //把命令的標準輸出重新定向到一個文件filename  
 $ls /dev >>filename         //把輸出追加到filename文件的末尾  
 $ls -qw  /dev  2>filename   //把標準錯誤重新定向到文件  
 $ls /dev &>filename         //把標準輸出和錯誤都定向到文件  
```
4.8垃圾黑洞 /dev/null
```
$find /home -name .basehrc 2> /dev/null
```
4.8 yes 命令
4.9 du 查詢磁碟空間使用情況
```
# du /
```
4.10 PID查詢命令ps, pidof, pgrep
4.11 串口通訊 uart
得到串口數據
```
# cat /dev/ttyUSB0
$screen /dev/cu.usbserial-XXXXXXXX 57600
```
4.12 screen 串口命令
```
ubuntu@ubuntu-System-Name:~$ sudo screen /dev/ttyUSB1 57600
ubuntu@ubuntu-System-Name:~$ screen
-D -RR        Do whatever is needed to get a screen session.
-e xy         Change command characters.
-f            Flow control on, -fn = off, -fa = auto.
-h lines      Set the size of the scrollback history buffer.
-i            Interrupt output sooner when flow control is on.
-l            Login mode on (update /var/run/utmp), -ln = off.
-list         or -ls. Do nothing, just list our SockDir.
-L            Turn on output logging.
-m            ignore $STY variable, do create a new screen session.
-O            Choose optimal output rather than exact vt100 emulation.
-p window     Preselect the named window if it exists.
-q            Quiet startup. Exits with non-zero return code if unsuccessful.
-r            Reattach to a detached screen process.
-R            Reattach if possible, otherwise start a new session.
-s shell      Shell to execute rather than $SHELL.
-S sockname   Name this session <pid>.sockname instead of <pid>.<tty>.<host>.
-t title      Set title. (window's name).
-T term       Use term as $TERM for windows, rather than "screen".
-U            Tell screen to use UTF-8 encoding.
-v            Print "Screen version 4.00.03jw4 (FAU) 2-May-06".
-wipe         Do nothing, just clean up SockDir.
-x            Attach to a not detached screen. (Multi display mode).
-X            Execute <cmd> as a screen command in the specified session.
```
4.13 後台運行命令
在linux中，讓程式在後台運行的話，其實很簡單。只要在運行程式的時候，在後面增加&符號就可以了。
5. Uboot
5.1 編譯Uboot
```
  $git clone https://github.com/MediaTek-Labs/linkit-smart-7688-uboot.git
  $cd linkit-smart-7688-uboot
  $sudo tar jxf buildroot-gcc342.tar.bz2 -C /opt/
  $make
```
5.2 修改uboot串口號
修改文件linkit-smart-7688-uboot\board\rt2880\serial.h
line21: #define CFG_RT2880_CONSOLE RT2880_UART3
5.3 uboot環境變數列印/修改(printenv,setenv,saveenv)
```
MT7628 # printenv
bootcmd=tftp
bootdelay=1
baudrate=57600
ethaddr="00:AA:BB:CC:DD:10" //
ipaddr=10.10.10.123   // 設備IP
serverip=10.10.10.3   // 伺服器IP
stdin=serial
stdout=serial
stderr=serial

Environment size: 149/4092 bytes

  MT7628 # setenv ipaddr 192.168.1.120
  MT7628 # setenv serverip 192.168.1.116
  MT7628 # saveenv
```  
5.4 linkit u-boot特有燒錄功能
5.4.1 uboot更新uboot-env環境變數
a. 在U盤中創建lks7688.cfg文件
```
  $cat lks7688.cfg
  wifi_ssid=moh_app
  wifi_key=12345678
```  
b. 插入u盤到開發板usb連接埠，按下wifi按鈕，復位板子。等待wifi指示燈亮後，鬆開wifi按鈕。uboot燒錄配置到uboot-env
5.4.2 uboot更新固件
a.燒錄lks7688.img到U盤
b.插入u盤，按下wifi按鈕，復位板子，等待大約5秒（wifi指示燈亮然後滅掉），鬆開wifi按鈕，uboot開始燒錄firmware
5.4.3 uboot更新uboot
a. 複製lks7688.ldr到U盤
b. u盤，按下wifi按鈕，復位板子，等待大約20秒，鬆開wifi按鈕，uboot更新uboot。
5.5 Uboot源代碼分析
5.5.1 lib_mips/board.c
linkit-smart-7688-uboot的主要代碼內容在這個文件當中，如果想對該uboot進行一些功能修改的話，可以在這個文件中進行進行。
6 shell command
6.1 pidof madplay

==================================================================
## WiFiHiFi – How to run Music Player Daemon on an OpenWRT wifi router ##
ref : https://silkemeyer.net/wifihifi-how-to-run-music-player-daemon-on-an-openwrt-wifi-router

Remember those old jukeboxes where pub guests could choose a song that was added to the playlist? Well, imagine a party at your house where all guests could do so via wifi using their own mobile devices! In this article I will show you how. They easiest setup is, of course, to run Music Player Daemon on the computer where the music is stored. You install a Music Player Client on your mobile device and connect it to this computer via wifi.
The setup I describe is interesting if you want to play music from a file server that is not connected to the wifi but is somewhere in the LAN. Once the setup works, you can listen to the music without your laptop being turned on all the time. The aim is to run Music Player Daemon directly on the wifi router so that different devices in the wifi network can create a common playlist. (Music Player Daemon is quite an old free software project. Read more about it in the project’s wiki [1] or on Wikipedia [2].)

What you need:
1. A wifi router running the free operating system OpenWRT. We used the TP-LINK model TL-WR1043ND – the one that comes with a USB port.
2. A supported USB sound card (e.g. the C-Media USB Headphone Set (3D SOUND)) and a cable connecting this sound card to your stereo.
3. Storage: You can either plug a USB hub into the wifi router and then connect the sound card and a USB flash disk to it. Or you get your music storage from somewhere else in the local network. This is what I did, so here I’ll talk about a fileserver in the LAN.
4. A notebook or PC to configure everything and to test your setup.
5. An internet connection for the wifi router during setup.
Diagram of the described setup

The setup (click to enlarge)
Step 1: Install OpenWRT on the wifi router
We need to modify the wifi router first to be able to install additional software on it. When you buy the TP-Link router mentioned above, you don’t get it with OpenWRT preinstalled. So here is how you install it (some of it depends on the exact hardware you choose):
To download the appropriate image for the hardware enter your device’s name on the wiki http://wiki.openwrt.org [3] and search. (It might not be the most user-friendly website you have ever seen.) For the TP-Link TL-WR1043ND I downloaded this image to my computer: http://downloads.openwrt.org/backfire/10.03.1/ar71xx/openwrt-ar71xx-tl-wr1043nd-v1-squashfs-factory.bin.
Configure your computer’s LAN interface in a way that it has a fixed IP address: The router probably has got the 192.168.1.1, give your computer the 192.168.1.2/24.
Open your browser, go to 192.168.1.1. Find the menu item that allows you to update the device’s firmware. Upload the OpenWRT image via the web interface. It will take a little moment, then the router will be back with a completely different web interface called „LuCI“. That’s OpenWRT.
Change the password and configure it as a wifi router for your network. (As I don’t know your router’s hostname, in the commands below, I will call it „router“. So make sure to replace „router“ with the hostname. Similarly, I called the user that accesses the file server via ssh „router“. „server-ip“ and „fileserver“ have to be replaced by your fileserver’s IP address.)
Keep your cable connection to the router and connect a second network cable to it, so that it can access the internet.

Step 2: Install some extra software on the router
Connect to the router via ssh, then run:
```
root@router:~# opkg update
root@router:~# opkg install kmod-usb-audio kmod-sound-core
# If you want to keep your music on a fileserver:
root@router:~# opkg install sshfs rsync
```
Step 3: Set up the ssh connection between router and file server
The router will have to access some directories on your file server permanently via ssh. Let’s create the key and config for this. First, create a user on your file server, e.g. „router“.
root@fileserver:~# useradd -m -d /home/router -s /bin/bash router
Check the file permissions of the music directory. If necessary, add the router user to an additional group. On OpenWRT you use dropbear for ssh. The procedure is very similar to openssh. This is how you create a key on your router:
```
root@router:~# dropbearkey -t rsa -f ~/.ssh/router
root@router:~# dropbearkey -y -f ~/.ssh/router | grep "^ssh-rsa " > ~/.ssh/router.pub
root@router:~# scp ~/.ssh/router.pub root@fileserver:/home/router/
```
on the file server:
```
root@fileserver:~# mkdir /home/router/.ssh && mv /home/router/router.pub /home/router/.ssh/authorized_keys
root@fileserver:~# chown -R router:router /home/router && chmod 750 /home/router/.ssh && chmod 600 /home/router/.ssh/authorized_keys
```
Create a new file called „config“ on your router, in the directory /root/.ssh:
```
IdentitiesOnly yes
Host = HOSTNAME OF FILE SERVER
HostName = server-ip
User = router
Port = 22
IdentityFile /root/.ssh/router
```
Step 3: Mount some extra disk space
On the router there is not enough free space to install everything we need. We will therefore use some storage the file server offers us. (Replace the parts in capital letters with your own values.)
```
root@router:~# mkdir /tmp/mnt
root@router:~# /usr/bin/sshfs -o ssh_command="ssh -i /root/.ssh/router" -o follow_symlinks router@server-ip:/home/router/usr /tmp/mnt
root@router:~# /usr/bin/rsync -rLptgoD /usr/ /tmp/mnt
root@router:~# umount /tmp/mnt
root@router:~# /usr/bin/sshfs -o ssh_command="ssh -i /root/.ssh/router" -o nonempty -o follow_symlinks router@server-ip:/home/router/usr /usr
## Control if this step worked:
root@router:~# mount
router@server-ip:/home/router/usr on /usr type fuse.sshfs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,max_read=65536)
```
Step 4: Mount the remote music storage and configure the sound stuff
Now we will install mpd, mount the file server’s music directory to the router via the encrypted sshfs connection and configure mpd. (mpc is only needed when you want to make the router update the music database itself. See below.)
```
root@router:~# opkg install mpd mpc alsa-utils
root@router:~# mkdir /mnt/mpd
root@router:~# /usr/bin/sshfs -o ssh_command="ssh -i /root/.ssh/router" -o follow_symlinks router@server-ip:/home/router/mpd /mnt/mpd
```
Check if it worked. In addition to the line, you just saw, there should now be a new one similar to this one:
```
root@router:~# mount
router@server-ip:/home/router/mpd on /mnt/mpd type fuse.sshfs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,max_read=65536)
Edit the configuration file of Music Player Daemon /etc/mpd.conf:
# /etc/mpd.conf for C-Media USB Headphone Set
# files
music_directory "/mnt/mpd/music"
playlist_directory "/mnt/mpd/playlists"
db_file "/mnt/mpd/database"
log_file "/mnt/mpd/log"
pid_file "/var/run/mpd.pid"
state_file "/mnt/mpd/state"
sticker_file "/mnt/mpd/sticker.sql"
# IP address of your router:
bind_to_address "XXX.YYY.ZZZ.XYZ"
# metadata
metadata_to_use "artist,album,title,track,name,genre,date,composer,performer,disc"
# follow symlinks
follow_outside_symlinks "yes"
follow_inside_symlinks "yes"
# permissions
password "YOURPASSWORD@read,add,control,admin"
default_permissions ""
# mixer type
mixer_type "software"
# max connections
max_connections "30"
# input
input {
plugin "curl"
}
# output
audio_output {
type "alsa"
name "Generic USB Audio Device" # you can check this with alsamixer
device "hw:0,0" # optional
}
#EOF
Edit the file /etc/init.d/mpd and replace the line amixer set PCM 40 with this line: amixer set Speaker 150.
```
Step 5: Make the router check if everyting is fine and update the music database every night
You might want to restore your setup automatically, in case you reboot the router. Write a small script that checks if the remote directories are mounted and if Music Player Daemon is running. the file should be placed in /bin/music.sh. Run chmod u+x to make in executable.
```
#!/bin/sh
  if [ "$( mount | grep sshfs | grep /usr )" == "" ]; then
  /bin/sleep 2
  /usr/bin/sshfs -o ssh_command="ssh -i /root/.ssh/router" -o nonempty -o follow_symlinks router@fileserver:/home/router/usr /usr
fi

if [ "$( mount | grep sshfs | grep /mnt/mpd )" == "" ]; then
  /bin/sleep 2
  /usr/bin/sshfs -o ssh_command="ssh -i /root/.ssh/router" -o follow_symlinks router@fileserver:/home/router/mpd /mnt/mpd
fi

if [ "$( ps | grep $( cat /var/run/mpd.pid ) | grep mpd )" == "" ]; then
  /bin/sleep 10
  /usr/bin/test -x /usr/bin/mpd && /etc/init.d/mpd start
fi
#EOF
```
Enter the command crontab -e. Add the following two lines to update mpd’s database every night automatically:
```
05 05 * * * /usr/bin/test -x /usr/bin/mpc && /usr/bin/mpc -h server-ip -P YOUR_PASSWORD update
*/2 *  * * * /usr/bin/test -x /bin/music.sh && /bin/music.sh
When you save and quit the file, the new cron job will be installed.
```
Step 6: Connect client devices
You are ready to test your setup! Choose a device that has access to your wifi and install a Music Player client. On Linux, this could be gmpc, on Android I recommend MPDroid. There is a long list of client software for different operating systems in the MPD wiki [4]. (Even iphone users will have access. 🙂 )

Step 7: Connect your friends and party
To make your next party’s guests choose music and add them directly to the playlist, you just give them the following information:

They have to install a client app.
Give them access to your wifi network,
the IP address of the router and
the password if you set one in /etc/mpd.conf.
Now turn your laptop off and enjoy! The wifi router and your guests will do the work! 😉

Links
[1]: http://mpd.wikia.com/wiki/Music_Player_Daemon_Wiki
[2]: Music Player Daemon on the English language Wikipedia: https://en.wikipedia.org/wiki/Music_Player_Daemon
[3]: http://wiki.openwrt.org
[4]: http://mpd.wikia.com/wiki/Clients

## make menuconfig error 解決方法 ##
```
root@jazzhipster-VirtualBox:/media/sf_LinuxDisk_JS/Mtk7688/openwrt# make menuconfig
Checking 'working-make'... ok.
Checking 'case-sensitive-fs'... failed.
Checking 'gcc'... ok.
Checking 'working-gcc'... ok.
Checking 'g++'... ok.
Checking 'working-g++'... ok.
Checking 'ncurses'... ok.
Checking 'zlib'... ok.
Checking 'libssl'... ok.
Checking 'tar'... ok.
Checking 'find'... ok.
Checking 'bash'... ok.
Checking 'patch'... ok.
Checking 'diff'... ok.
Checking 'cp'... ok.
Checking 'seq'... ok.
Checking 'awk'... ok.
Checking 'grep'... ok.
Checking 'getopt'... ok.
Checking 'stat'... ok.
Checking 'md5sum'... ok.
Checking 'unzip'... ok.
Checking 'bzip2'... ok.
Checking 'wget'... ok.
Checking 'perl'... ok.
Checking 'python'... ok.
Checking 'svn'... ok.
Checking 'git'... ok.
Checking 'file'... ok.
Checking 'openssl'... ok.
Checking 'ldconfig-stub'... ok.

Build dependency: OpenWrt can only be built on a case-sensitive filesystem
Prerequisite check failed. Use FORCE=1 to override.
make: *** [staging_dir/host/.prereq-build] Error 1
root@jazzhipster-VirtualBox:/media/sf_LinuxDisk_JS/Mtk7688/openwrt# ^C
root@jazzhipster-VirtualBox:/media/sf_LinuxDisk_JS/Mtk7688/openwrt# ^C
```
I know it has been year but even now you are stuck here is answer
You might be using Windows as host and NTFS as file system
so NTFS is non case sensitive FS
according to wiki
In Unix filesystems, filenames are usually case-sensitive. Old Windows filesystems (VFAT, FAT32) are not case-sensitive (there cannot be a readme.txt and a Readme.txt in the same directory) but are case-preserving, i.e. remembering the case of the letters. The original FAT12 filesystem was case-insensitive.[7] Current Windows file systems, like NTFS, are case-sensitive; that is a readme.txt and a Readme.txt can exist in the same directory.
so there is chance that you have shared your folder with virtual box.
and compiling same source.
so copy source on EXT4 partition and compile.
safest way is get fresh source directly on EXT4 partition and let me know.
I think this should solve your problem.

## Linkit 7688 Duo USB firmware update-記錄(解磚-救磚-更新) ##
開發板的第一篇分享文章，就是把開發板玩壞後的復原……
先看一下磚掉的7688是什麼情況，老實說我也不確定是否磚掉了
但wifi燈長亮也連不上7688，我就當他是磚掉了
接下來的說明，參考資料來自 https://www.youtube.com/watch?v=YZ1Zkg7vBqQ
簡單的說，解磚的方法 = 透過USB更新 firmware
1. 首先要準備一支USB隨身碟，必需要是FAT32的格式
2. 至官網下載最新的 firmware 
https://labs.mediatek.com/site/global/developer_tools/mediatek_linkit_smart_7688/sdt_intro/index.gsp
3. 解開壓縮檔，拷貝lks7688.img至隨身碟根目錄
一定要放在USB的根目錄，而且檔名為 lks7688.img
4. 隨身碟接至7688的USB HOST
靠綠燈的是USB Host
5. 按下wifi reset 不放，再按一下MPU reset並放開(wifi reset還不能放喔)，等五秒後再放開wifi reset
6. 請等約五分鐘…wifi 燈號一開始會快閃，然後穩定的閃亮，更新完成時7688會重啟(耐心！耐心！)
https://labs.mediatek.com/fileMedia/download/87c801b5-d1e6-4227-9a29-b5421f2955ac#page=47
7. done.   
wifi 回復正常了
如果是要更新firmware，照本篇做是沒問題的
希望你也救回你的了7688

============================================================
## WiFi STA setup ##

- Step-by-step
Step 1 — Apply UCI commands to assign SSID, key, and encryption information for the Station mode
Assume the wireless router to be connected is with the following properties:
```
SSID: SampleAP
Password: 12345678
Encryption: WPA2 Personal
In the system console of LinkIt Smart 7688, type the following commands if you're with the firmware version v0.9.4 or above: 
Commands for v0.9.4 or above
# uci set wireless.sta.ssid=SampleAP
# uci set wireless.sta.key=12345678
# uci set wireless.sta.encryption=psk2
# uci commit
If you're using the firmware v0.9.3 or below, please use this set of commands:
Commands for v0.9.3 and v0.9.2
# uci set wireless.sta.ssid=SampleAP  
# uci set wireless.sta.key=12345678  
# uci set wireless.sta.encryption=psk2  
# uci set wireless.sta.disabled=0  
# uci commit
```
Step 2 — Restart the Wi-Fi driver to activate the configuration
Type the command in the system console:
Command for v0.9.4 or above
```
# wifi_mode sta
For firmware v0.9.3 or below, please use this command:
Commands for v0.9.3 and v0.9.2
# wifi  
```
If you use SSH to connect to the system console of the LinkIt Smart 7688 development board, you'll lose the connection once the wifi command is set. This command will restart the Wi-Fi driver and then connect your PC to the same wireless router as the board did. Then you can connect to the LinkIt Smart 7688 development board with mylinkit.local by SSH again.
You can also refer to the LED behavior to check the states of the connection in Station mode.
Step 3 — Check for internet connection
Now check if you’ve established internet connection by typing the following command in the system console:
```
# ping –c 5 www.mediatek.com
```
If you see messages like below, then congratulations. You’ve connected to the wireless router with internet access.
```
root@mylinkit:/# ping -c 5 www.mediatek.com  
PING www.mediatek.com (210.61.82.38): 56 data bytes  
64 bytes from 210.61.82.38: seq=0 ttl=244 time=388.372 ms  
64 bytes from 210.61.82.38: seq=1 ttl=244 time=368.003 ms  
64 bytes from 210.61.82.38: seq=2 ttl=244 time=397.851 ms  
64 bytes from 210.61.82.38: seq=3 ttl=244 time=417.423 ms  
64 bytes from 210.61.82.38: seq=4 ttl=244 time=357.303 ms   
--- www.mediatek.com ping statistics ---  5 packets transmitted, 
5 packets received, 0% packet loss  
round-trip min/avg/max = 357.303/385.790/417.423 ms
```

==================================================================
## END
