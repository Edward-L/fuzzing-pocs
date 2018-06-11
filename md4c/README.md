#md4c commit cb7ecd713593acef78f2698f6c5a5a59a2745b6f

NULL_pointer_dereferenc_in_md4c_c_5824.poc
```
(gdb) set args --github crash1 
(gdb) r
Starting program: /opt/lxf/md4c/md2html/md2html --github crash1 

Program received signal SIGSEGV, Segmentation fault.
md_process_line (line=0x7fffffffde80, p_pivot_line=<synthetic pointer>, ctx=0x7fffffffdf30)
    at /opt/lxf/md4c/md4c/md4c.c:5824
5824	        ctx->current_block->type = MD_BLOCK_TABLE;
(gdb) bt
#0  md_process_line (line=0x7fffffffde80, p_pivot_line=<synthetic pointer>, ctx=0x7fffffffdf30)
    at /opt/lxf/md4c/md4c/md4c.c:5824
#1  md_process_doc (ctx=0x7fffffffdf30) at /opt/lxf/md4c/md4c/md4c.c:5865
#2  md_parse (text=text@entry=0x627250 "", size=size@entry=8632, renderer=renderer@entry=0x7fffffffe1c0, 
    userdata=userdata@entry=0x7fffffffe1a0) at /opt/lxf/md4c/md4c/md4c.c:5935
#3  0x0000000000403aa2 in md_render_html (input=input@entry=0x627250 "", input_size=input_size@entry=8632, 
    process_output=process_output@entry=0x402280 <process_output>, userdata=userdata@entry=0x7fffffffe210, 
    parser_flags=<optimized out>, renderer_flags=<optimized out>) at /opt/lxf/md4c/md2html/render_html.c:488
#4  0x0000000000401263 in process_file (out=0x7ffff7dd4400 <_IO_2_1_stdout_>, in=0x627010)
    at /opt/lxf/md4c/md2html/md2html.c:139
#5  main (argc=<optimized out>, argv=<optimized out>) at /opt/lxf/md4c/md2html/md2html.c:343
(gdb) p ctx->current_block 
$1 = (MD_BLOCK *) 0x0
```

heap_overflow_in_md_build_attribute_md4c_c_1462.poc
```
Program received signal SIGSEGV, Segmentation fault.
0x0000000000404f4b in md_build_attribute (ctx=ctx@entry=0x7fffffffdf30, 
    raw_text=0x62756b "http://meta.math.stackexchan\214\345\246\202\351\234\200\346\222\260\345\206\231\346\226\260\347\250\277\344\273\266\357\274\214\347\202\271\345\207\273\351\241\266\351\203\250\345\267\245\345\205\267\346\240\217\345\217\263\344\276\377\a\232\204 <i class=\"icon-file\"></i> **\346\226\260\346\226\207\347\250\277** \346\210\226\350\200\205\344\275\277\347\224\250\345\277\253\346\215\267\351\224\256 `Ctrl+Alt+N`\343\200\202\r\n\r\n------\r\n\r\n## \344\273\200\344\271\210\346\230\257 Markdown\r\n\r\n"..., 
    raw_size=raw_size@entry=4294966501, flags=<optimized out>, attr=attr@entry=0x7fffffffdd40, 
    build=build@entry=0x7fffffffdce0) at /opt/lxf/md4c/md4c/md4c.c:1462
1462	            if(raw_text[raw_off] == _T('\0')) {
(gdb) bt
#0  0x0000000000404f4b in md_build_attribute (ctx=ctx@entry=0x7fffffffdf30, 
    raw_text=0x62756b "http://meta.math.stackexchan\214\345\246\202\351\234\200\346\222\260\345\206\231\346\226\260\347\250\277\344\273\266\357\274\214\347\202\271\345\207\273\351\241\266\351\203\250\345\267\245\345\205\267\346\240\217\345\217\263\344\276\377\a\232\204 <i class=\"icon-file\"></i> **\346\226\260\346\226\207\347\250\277** \346\210\226\350\200\205\344\275\277\347\224\250\345\277\253\346\215\267\351\224\256 `Ctrl+Alt+N`\343\200\202\r\n\r\n------\r\n\r\n## \344\273\200\344\271\210\346\230\257 Markdown\r\n\r\n"..., 
    raw_size=raw_size@entry=4294966501, flags=<optimized out>, attr=attr@entry=0x7fffffffdd40, 
    build=build@entry=0x7fffffffdce0) at /opt/lxf/md4c/md4c/md4c.c:1462
#1  0x0000000000405446 in md_enter_leave_span_a (ctx=ctx@entry=0x7fffffffdf30, enter=4, 
    type=type@entry=MD_SPAN_A, dest=<optimized out>, dest_size=dest_size@entry=4294966501, 
    prohibit_escapes_in_dest=prohibit_escapes_in_dest@entry=1, title=0x0, title_size=0)
    at /opt/lxf/md4c/md4c/md4c.c:3846
#2  0x000000000040580c in md_process_inlines (ctx=ctx@entry=0x7fffffffdf30, lines=lines@entry=0x6333a8, 
    n_lines=n_lines@entry=1) at /opt/lxf/md4c/md4c/md4c.c:4003
#3  0x0000000000411ce3 in md_process_normal_block_contents (n_lines=1, lines=0x6333a8, ctx=0x7fffffffdf30)
    at /opt/lxf/md4c/md4c/md4c.c:4302
#4  md_process_leaf_block (block=0x6333a0, ctx=0x7fffffffdf30) at /opt/lxf/md4c/md4c/md4c.c:4472
#5  md_process_all_blocks (ctx=0x7fffffffdf30) at /opt/lxf/md4c/md4c/md4c.c:4547
#6  md_process_doc (ctx=0x7fffffffdf30) at /opt/lxf/md4c/md4c/md4c.c:5874
#7  md_parse (
    text=text@entry=0x627250 "# \346\254\242\350\277\216\344\275", '&' <repeats 17 times>, " \347\274\226\350\276\221\351\230\305\350\257\273\345\231\250\r\n\r\n------\r\n\r\n\346\310\221\344\273\254\347\220\206\350\247\r\n", size=size@entry=10251, renderer=renderer@entry=0x7fffffffe1c0, 
    userdata=userdata@entry=0x7fffffffe1a0) at /opt/lxf/md4c/md4c/md4c.c:5935
#8  0x0000000000403aa2 in md_render_html (
    input=input@entry=0x627250 "# \346\254\242\350\277\216\344\275", '&' <repeats 17 times>, " \347\274\226\350\276\221\351\230\305\350\257\273\345\231\250\r\n\r\n------\r\n\r\n\346\310\221\344\273\254\347\220\206\350\247\r\n", input_size=input_size@entry=10251, process_output=process_output@entry=0x402280 <process_output>, 
    userdata=userdata@entry=0x7fffffffe210, parser_flags=<optimized out>, renderer_flags=<optimized out>)
    at /opt/lxf/md4c/md2html/render_html.c:488
#9  0x0000000000401263 in process_file (out=0x7ffff7dd4400 <_IO_2_1_stdout_>, in=0x627010)
    at /opt/lxf/md4c/md2html/md2html.c:139
#10 main (argc=<optimized out>, argv=<optimized out>) at /opt/lxf/md4c/md2html/md2html.c:343
(gdb) p raw_off 
$1 = 187029
(gdb) p raw_text[raw_off]
Cannot access memory at address 0x655000
(gdb) p raw_text[raw_off-1]
$2 = 0 '\000'
(gdb) p raw_size 
$3 = 4294966501
```
