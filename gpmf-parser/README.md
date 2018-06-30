# gpmf-parser commit 5610f2d

## cve-2018-13007 & cve-2018-13008 & cve-2018-13009 
heap_overflow_GPMF_parser_c_line_260.poc
three heap overflow in GPMF_parser.c line 260 ,line 266, line 277 in function GPMF_Next

fix it like this
```
while ( ms->nest_size[ms->nest_level] > 0 && ms->buffer[ms->pos] == GPMF_KEY_END)
```

asan report

```
=================================================================
==9074==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x62100001ded8 at pc 0x403fe1 bp 0x7ffd9e198990 sp 0x7ffd9e198988
READ of size 4 at 0x62100001ded8 thread T0
    #0 0x403fe0 in GPMF_Next ../GPMF_parser.c:260
    #1 0x404f77 in GPMF_FindNext ../GPMF_parser.c:327
    #2 0x4018c2 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:109
    #3 0x7fe0aa9c2f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #4 0x401108 (/opt/lxf/gpmf-parser-master/demo/gpmfdemo+0x401108)

0x62100001ded8 is located 0 bytes to the right of 4568-byte region [0x62100001cd00,0x62100001ded8)
allocated by thread T0 here:
    #0 0x7fe0aadbeb0a in __interceptor_realloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54b0a)
    #1 0x429352 in GetGPMFPayload /opt/lxf/gpmf-parser-master/demo/GPMF_mp4reader.c:86
    #2 0x4014e5 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:94
    #3 0x7fe0aa9c2f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)

SUMMARY: AddressSanitizer: heap-buffer-overflow ../GPMF_parser.c:260 GPMF_Next
Shadow bytes around the buggy address:
  0x0c427fffbb80: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c427fffbb90: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c427fffbba0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c427fffbbb0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c427fffbbc0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c427fffbbd0: 00 00 00 00 00 00 00 00 00 00 00[fa]fa fa fa fa
  0x0c427fffbbe0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c427fffbbf0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c427fffbc00: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c427fffbc10: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c427fffbc20: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==9074==ABORTING
```

[poc](https://github.com/gopro/gpmf-parser/blob/master/samples/karma.mp4)


## heap-buffer-overflow-GPMF_parser-c-61-GPMF_Validate.poc
a heap buffer overflow in GPMF_parser.c line 61 in function GPMF_Validate

asan report

```
=================================================================
==60040==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000efb4 at pc 0x40260d bp 0x7ffeeb6e1a40 sp 0x7ffeeb6e1a38
READ of size 4 at 0x60200000efb4 thread T0
    #0 0x40260c in GPMF_Validate ../GPMF_parser.c:61
    #1 0x401425 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:71
    #2 0x7f6c28e1bf44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #3 0x401108 (/opt/lxf/gpmf-parser-master/demo/gpmfdemo_asan+0x401108)

0x60200000efb4 is located 0 bytes to the right of 4-byte region [0x60200000efb0,0x60200000efb4)
allocated by thread T0 here:
    #0 0x7f6c29217b0a in __interceptor_realloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54b0a)
    #1 0x429352 in GetGPMFPayload /opt/lxf/gpmf-parser-master/demo/GPMF_mp4reader.c:86
    #2 0x4013c8 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:62
    #3 0x7f6c28e1bf44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)

SUMMARY: AddressSanitizer: heap-buffer-overflow ../GPMF_parser.c:61 GPMF_Validate
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa fa fa fa fa[04]fa fa fa 00 00 fa fa 00 fa
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
==60040==ABORTING
```


## CVE-2018-13011 
heap-buffer-overflow-GPMF_parser-c-129-GPMF_Validate.poc
a heap-buffer-overflow in GPMF_parser.c line 129 in functions GPMF_Validate

asan report
```
=================================================================
==126379==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x62300000f900 at pc 0x402d7c bp 0x7ffedf84d6e0 sp 0x7ffedf84d6d8
READ of size 4 at 0x62300000f900 thread T0
    #0 0x402d7b in GPMF_Validate ../GPMF_parser.c:129
    #1 0x401425 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:71
    #2 0x7f3595eb8f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #3 0x401108 (/opt/lxf/gpmf-parser-master/demo/gpmfdemo_asan+0x401108)

0x62300000f900 is located 0 bytes to the right of 6144-byte region [0x62300000e100,0x62300000f900)
allocated by thread T0 here:
    #0 0x7f35962b4b0a in __interceptor_realloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54b0a)
    #1 0x429352 in GetGPMFPayload /opt/lxf/gpmf-parser-master/demo/GPMF_mp4reader.c:86
    #2 0x4013c8 in main /opt/lxf/gpmf-parser-master/demo/GPMF_demo.c:62
    #3 0x7f3595eb8f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)

SUMMARY: AddressSanitizer: heap-buffer-overflow ../GPMF_parser.c:129 GPMF_Validate
Shadow bytes around the buggy address:
  0x0c467fff9ed0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c467fff9ee0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c467fff9ef0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c467fff9f00: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  0x0c467fff9f10: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
=>0x0c467fff9f20:[fa]fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c467fff9f30: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c467fff9f40: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c467fff9f50: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c467fff9f60: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c467fff9f70: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
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
==126379==ABORTING
```


## heap-buffer-overflow-in-GPMF_parser.c-528-GPMF_Type.poc
a heap-buffer-overflow in GPMF_parser.c:528 function GPMF_Type

```
=================================================================
==131748==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000efb4 at pc 0x4068ee bp 0x7ffe5153d9e0 sp 0x7ffe5153d9d8
READ of size 4 at 0x60200000efb4 thread T0
    #0 0x4068ed in GPMF_Type ../GPMF_parser.c:528
    #1 0x431a30 in PrintGPMF /opt/lxf/gpmf-parser/gpmf-parser-master/demo/GPMF_print.c:394
    #2 0x401461 in main /opt/lxf/gpmf-parser/gpmf-parser-master/demo/GPMF_demo.c:81
    #3 0x7fa688a75f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)
    #4 0x401108 (/opt/lxf/gpmf-parser/gpmf-parser-master/demo/gpmfdemo-asan+0x401108)

0x60200000efb4 is located 0 bytes to the right of 4-byte region [0x60200000efb0,0x60200000efb4)
allocated by thread T0 here:
    #0 0x7fa688e71b0a in __interceptor_realloc (/usr/lib/x86_64-linux-gnu/libasan.so.1+0x54b0a)
    #1 0x429520 in GetGPMFPayload /opt/lxf/gpmf-parser/gpmf-parser-master/demo/GPMF_mp4reader.c:86
    #2 0x4013c8 in main /opt/lxf/gpmf-parser/gpmf-parser-master/demo/GPMF_demo.c:62
    #3 0x7fa688a75f44 in __libc_start_main (/lib/x86_64-linux-gnu/libc.so.6+0x21f44)

SUMMARY: AddressSanitizer: heap-buffer-overflow ../GPMF_parser.c:528 GPMF_Type
Shadow bytes around the buggy address:
  0x0c047fff9da0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9db0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dc0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9dd0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
  0x0c047fff9de0: fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa fa
=>0x0c047fff9df0: fa fa fa fa fa fa[04]fa fa fa 00 00 fa fa 00 fa
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
==131748==ABORTING
```

