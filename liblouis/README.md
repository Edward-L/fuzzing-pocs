#liblouis commit 53b839f

*CVE-2018-11577*
SEGV-logging-c-148.poc
```
ASAN:SIGSEGV
=================================================================
==59249==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000000 (pc 0x7f862930f3dc sp 0x7ffc3e653ca0 bp 0x000000000001 T0)
    #0 0x7f862930f3db in __vfprintf_chk (/lib/x86_64-linux-gnu/libc.so.6+0x10d3db)
    #1 0x40d5d7 in vfprintf /usr/include/x86_64-linux-gnu/bits/stdio2.h:127
    #2 0x40d5d7 in lou_logPrint /opt/lxf/liblouis-master/liblouis/logging.c:148
    #3 0x40d32f in _lou_logMessage /opt/lxf/liblouis-master/liblouis/logging.c:114
    #4 0x401afd in compileError /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:272
    #5 0x402420 in parseDots /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:1271
    #6 0x4024a7 in passGetDots /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:1584
    #7 0x405ce9 in compilePassOpcode /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:2561
    #8 0x40896a in compileRule /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:3974
    #9 0x40af72 in compileFile /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:4498
    #10 0x40b265 in compileTranslationTable /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:4603
    #11 0x40b265 in lou_getTable /opt/lxf/liblouis-master/liblouis/compileTranslationTable.c:4688
    #12 0x40162a in main /opt/lxf/liblouis-master/tools/lou_checktable.c:112
    #13 0x7f8629223f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #14 0x401854 (/opt/lxf/liblouis-master/tools/.libs/lou_checktable_static_asan+0x401854)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV ??:0 __vfprintf_chk
==59249==ABORTING
```
