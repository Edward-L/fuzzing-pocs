# tcpreplay commit 230d7aa

## heap-buffer-overflow-in-get.c-174-get_l2len.poc
heap-buffer-overflow in /src/common/get.c:174 function get_l2len

command:
```
/tcpprep --auto=bridge --pcap=poc --cachefile=/dev/null
```

asan report:
```
 AddressSanitizer: heap-buffer-overflow in /src/common/get.c:174 get_l2len
=================================================================
==68006==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000effc at pc 0x4174d8 bp 0x7ffffffede30 sp 0x7ffffffede28
READ of size 2 at 0x60200000effc thread T0
    #0 0x4174d7 in get_l2len /opt/lxf/tcpreplay/tcpreplay-master/src/common/get.c:174
    #1 0x4176b4 in get_ipv4 /opt/lxf/tcpreplay/tcpreplay-master/src/common/get.c:229
    #2 0x405fe5 in process_raw_packets /opt/lxf/tcpreplay/tcpreplay-master/src/tcpprep.c:368
    #3 0x405152 in main /opt/lxf/tcpreplay/tcpreplay-master/src/tcpprep.c:146
    #4 0x7ffff66faf44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #5 0x4026c8 (/opt/lxf/tcpreplay/tcpreplay-master/src/tcpprep_asan+0x4026c8)

0x60200000effc is located 8 bytes to the right of 4-byte region [0x60200000eff0,0x60200000eff4)
allocated by thread T0 here:
    #0 0x7ffff6f59862 in __interceptor_malloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54862)
    #1 0x7ffff6ce270c in pcap_check_header sf-pcap.c:401

SUMMARY: AddressSanitizer: heap-buffer-overflow /opt/lxf/tcpreplay/tcpreplay-master/src/common/get.c:174 get_l2len
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa 04[fa]
  0x0c047fff9e00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Heap right redzone:      fb
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack partial redzone:   f4
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Contiguous container OOB:fc
  ASan internal:           fe
==68006==ABORTING
```
