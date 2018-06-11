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
