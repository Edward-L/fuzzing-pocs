# ngiflib commit 93d864a

## *CVE-2018-11575*
stack-buffer-overflow-ngiflib-c-543.poc
```
=================================================================
==226949==ERROR: AddressSanitizer: stack-buffer-overflow on address 0x7fff5e0ae0ff at pc 0x404e89 bp 0x7fff5e0aaed0 sp 0x7fff5e0aaec8
WRITE of size 1 at 0x7fff5e0ae0ff thread T0
    #0 0x404e88 in DecodeGifImg /opt/lxf/ngiflib-master/ngiflib.c:543
    #1 0x406515 in LoadGif /opt/lxf/ngiflib-master/ngiflib.c:789
    #2 0x40184e in main /opt/lxf/ngiflib-master/gif2tga.c:95
    #3 0x7f11dbd4bf44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #4 0x4011a8 (/opt/lxf/ngiflib-master/gif2tga_asan+0x4011a8)

Address 0x7fff5e0ae0ff is located in stack of thread T0 at offset 12703 in frame
    #0 0x40378d in DecodeGifImg /opt/lxf/ngiflib-master/ngiflib.c:387

  This frame has 4 object(s):
    [32, 8224) 'ab_prfx'
    [8256, 8544) 'context'
    [8576, 12672) 'ab_suffx'
    [12704, 16800) 'ab_stack' <== Memory access at offset 12703 underflows this variable
HINT: this may be a false positive if your program uses some custom stack unwind mechanism or swapcontext
      (longjmp and C++ exceptions *are* supported)
SUMMARY: AddressSanitizer: stack-buffer-overflow /opt/lxf/ngiflib-master/ngiflib.c:543 DecodeGifImg
Shadow bytes around the buggy address:
  0x10006bc0dbc0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dbd0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dbe0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dbf0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dc00: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x10006bc0dc10: 00 00 00 00 00 00 00 00 00 00 00 00 f2 f2 f2[f2]
  0x10006bc0dc20: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dc30: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dc40: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dc50: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x10006bc0dc60: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
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
==226949==ABORTING
```

## *CVE-2018-11578*
SEGV-ngiflib-c-808.poc
```
ASAN:SIGSEGV
=================================================================
==209972==ERROR: AddressSanitizer: SEGV on unknown address 0x000000000086 (pc 0x000000402b71 sp 0x7fff92bb3570 bp 0x7fff92bb7840 T0)
    #0 0x402b70 in GifIndexToTrueColor /opt/lxf/ngiflib-master/ngiflib.c:808
    #1 0x402e61 in WritePixels /opt/lxf/ngiflib-master/ngiflib.c:214
    #2 0x404f27 in DecodeGifImg /opt/lxf/ngiflib-master/ngiflib.c:550
    #3 0x406515 in LoadGif /opt/lxf/ngiflib-master/ngiflib.c:789
    #4 0x40184e in main /opt/lxf/ngiflib-master/gif2tga.c:95
    #5 0x7fac605b0f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #6 0x4011a8 (/opt/lxf/ngiflib-master/gif2tga_asan+0x4011a8)

AddressSanitizer can not provide additional info.
SUMMARY: AddressSanitizer: SEGV /opt/lxf/ngiflib-master/ngiflib.c:808 GifIndexToTrueColor
==209972==ABORTING
```

## *CVE-2018-11576*
heap-buffer-overflow-ngiflib-c-808.poc
```
=================================================================
==18451==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60300000f00f at pc 0x402b71 bp 0x7ffd69d08800 sp 0x7ffd69d087f8
READ of size 1 at 0x60300000f00f thread T0
    #0 0x402b70 in GifIndexToTrueColor /opt/lxf/ngiflib-master/ngiflib.c:808
    #1 0x4049d5 in WritePixel /opt/lxf/ngiflib-master/ngiflib.c:124
    #2 0x4049d5 in DecodeGifImg /opt/lxf/ngiflib-master/ngiflib.c:531
    #3 0x406515 in LoadGif /opt/lxf/ngiflib-master/ngiflib.c:789
    #4 0x40184e in main /opt/lxf/ngiflib-master/gif2tga.c:95
    #5 0x7f4bbfbbef44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #6 0x4011a8 (/opt/lxf/ngiflib-master/gif2tga_asan+0x4011a8)

0x60300000f00f is located 23 bytes to the right of 24-byte region [0x60300000efe0,0x60300000eff8)
allocated by thread T0 here:
    #0 0x7f4bbffba862 in __interceptor_malloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54862)
    #1 0x405614 in LoadGif /opt/lxf/ngiflib-master/ngiflib.c:634

SUMMARY: AddressSanitizer: heap-buffer-overflow /opt/lxf/ngiflib-master/ngiflib.c:808 GifIndexToTrueColor
Shadow bytes around the buggy address:
  0x0c067fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9df0: fa fa fa fa fa fa fa fa fa fa fa fa 00 00 00 fa
=>0x0c067fff9e00: fa[fa]fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c067fff9e50: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==18451==ABORTING
```


## *CVE-2018-11657*
dos-an-infinite-loop-ngiflib-c-669.poc

 in LoadGif ngiflig.c:669 has an infinite loop
