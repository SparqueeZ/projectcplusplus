September 2023 release of PcapPlusPlus (v23.09)
===============================================

PcapPlusPlus web-site:  https://pcapplusplus.github.io/

GitHub page:            https://github.com/seladb/PcapPlusPlus


This package contains:
----------------------

 - PcapPlusPlus compiled libraries for MinGW-w64 (under `lib\`)
    - Common++.lib
    - Packet++.lib
    - Pcap++.lib
 - PcapPlusPlus header files (under `include\pcapplusplus`)
 - Compiled examples (under `bin\`)
 - Code example with a simple CMake file showing how to build applications with PcapPlusPlus (under `example-app\`)
 - CMake files required to build your application with PcapPlusPlus (under `lib\cmake\pcapplusplus`)


Using PcapPlusPlus in your project:
-----------------------------------

 - Make sure you have MinGW-w64 installed with a gcc/g++ version matching the compiled binaries. The best place to download MinGW-w64 is
   through MSYS2 or directly from here: https://www.mingw-w64.org/downloads/#mingw-builds
 - You may have to put MinGW-w64 directory in your `PATH` environment variable
 - Make sure you have WinPcap, Npcap or Wireshark installed
 - Make sure you have WinPcap or Npcap Developer's pack installed (WinPcap Dev Pack can be downloaded from https://www.winpcap.org/devel.htm, Npcap SDK can be downloaded from https://nmap.org/npcap/#download)
 - If your application uses CMake, you can add `PcapPlusPlus_ROOT=<PACKAGE_DIR>`, `PCAP_ROOT=<WinPcap_OR_Npcap_DIR>` and `Packet_ROOT=<WinPcap_OR_Npcap_DIR>``
   when running CMake, for example:
   `cmake -S . -B build -DPcapPlusPlus_ROOT=<PACKAGE_DIR> -DPCAP_ROOT=<WinPcap_OR_Npcap_DIR> -DPacket_ROOT=<WinPcap_OR_Npcap_DIR>`
 - If your application uses Makefiles, you can create variables in your Makefile to point to the header and lib directories
   in the package. Here is an example:
   ```
   PCAP_ROOT := <WinPcap_OR_Npcap_DIR>
   PCAPPLUSPLUS_ROOT := <PACKAGE_DIR>
   PCAPPLUSPLUS_INCLUDES := $(PCAPPLUSPLUS_ROOT)/include/pcapplusplus
   PCAPPLUSPLUS_LIBS_DIR := $(PCAPPLUSPLUS_ROOT)/lib
   PCAPPLUSPLUS_LIBS := -lPcap++ -lPacket++ -lCommon++ -lwpcap -lPacket -lws2_32 -liphlpapi

   # All Target
   all:
      g++.exe -I$(PCAPPLUSPLUS_INCLUDES) -c -o main.o main.cpp
      g++.exe -L$(PCAPPLUSPLUS_LIBS_DIR) -L$(PCAP_ROOT) -static-libgcc -static-libstdc++ -o PcapPlusPlusTestApp.exe main.o $(PCAPPLUSPLUS_LIBS)
   ```


Running the examples:
---------------------

 - Make sure you have WinPcap, Npcap or Wireshark installed

Release notes (changes from v22.11)
-----------------------------------

 - PcapPlusPlus moved from a custom build system to CMake! (thanks @clementperon !)
 - Added IP/IPv4/IPv6 network classes to better support netmask and subnets
 - Add support for opening NFLOG live device (thanks @MrPeck !)
 - MAC address OUI Lookup (thanks @egecetin !)
 - Intel oneAPI compiler support (icpx) (thanks @egecetin !)
 - DPDK improvements:
   - Properly support no RSS mode in `DpdkDevice`
   - Make DPDK app name configurable (thanks @szokovacs !)
   - More generic search of DPDK KNI kernel module in `setup_dpdk.py`
 - New protocols:
   - NFLOG (Linux Netfilter NFLOG) (thanks @jafar75 !)
   - SLL2 (Linux cooked capture v2) (thanks @jiangjiongyu !)
   - TPKT (thanks @wivien19 !)
   - COTP (thanks @wivien19 !)
   - VRRP (thanks @wangchong2023 !)
 - Existing protocols improvements:
   - HTTP - refactor and improve `HttpResponseStatusCode` (thanks @tigercosmos !)
   - SSL/TLS - better detection of possible encrypted handshake messages (thanks @axmahr !)
   - DNS - support parsing of resources with larger data (thanks @aengusjiang !)
   - STP - add editing/crafting support (thanks @egecetin !)
   - ARP - add `isRequest` and `isReply` methods (thanks @tigercosmos !)
   - FTP-DATA support (thanks @egecetin !)
   - NTP - support Kiss of Death (thanks @egecetin !)
   - SIP - refactor status codes + add a few missing ones
 - Modernize the codebase to use `nullptr` instead of `NULL` (thanks @clementperon !)
 - Remove usage of unsupported `pcap_compile_nopcap()` (thanks @yushijinhun !)
 - Internal tools:
   - Codecov integration for coverage reports (thanks @egecetin !)
   - Enable Clang-Tidy (thanks @clementperon !)
   - Enable `cppcheck` (thanks @egecetin !)
   - Improve the test framework
   - Increase test coverage
 - Remove deprecated methods (due to typos):
   - `DhcpLayer::getMesageType()` -> replaced by `DhcpLayer::getMessageType()`
   - `DhcpLayer::setMesageType()` -> replaced by `DhcpLayer::setMesasgeType()`
   - `SSLHandshakeMessage::createHandhakeMessage()` -> replaced by `SSLHandshakeMessage::createHandshakeMessage()`
   - `SSLClientHelloMessage::getExtensionsLenth()` -> replaced by `SSLClientHelloMessage::getExtensionsLength()`
   - `SSLServerHelloMessage::getExtensionsLenth()` -> replaced by `SSLServerHelloMessage::getExtensionsLength()`
 - Tons of bug fixes, security fixes, major and minor improvements (thanks @egecetin, @clementperon, @sashashura, @tigercosmos, @kolbex, @traversebitree, @JasMetzger, @tbhaxor, @yishai1999, @aengusjiang, @Heysunk, @jpcofr !)


Collaborators
-------------

 - @clementperon
 - @egecetin


Contributors
------------

 - @sashashura
 - @tigercosmos
 - @wivien19
 - @jafar75
 - @MrPeck
 - @szokovacs
 - @axmahr
 - @yishai1999
 - @traversebitree
 - @jiangjiongyu
 - @wangchong2023
 - @kolbex
 - @JasMetzger
 - @yushijinhun
 - @aengusjiang
 - @tbhaxor
 - @Heysunk
 - @jpcofr

**Full Changelog**: https://github.com/seladb/PcapPlusPlus/compare/v22.11...v23.09
