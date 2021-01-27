On se connecte sur le level0, ou se trouve un **binaire** <code>level0</code>.

On cherche a savoir ce que fait ce binaire:
```gdb
> gdb level0 -q
Reading symbols from /home/user/level0/level0...(no debugging symbols found)...done.
(gdb) > disas main
Dump of assembler code for function main:
   0x08048ec0 <+0>:     push   %ebp
   0x08048ec1 <+1>:     mov    %esp,%ebp
   0x08048ec3 <+3>:     and    $0xfffffff0,%esp
   0x08048ec6 <+6>:     sub    $0x20,%esp
   0x08048ec9 <+9>:     mov    0xc(%ebp),%eax
   0x08048ecc <+12>:    add    $0x4,%eax
   0x08048ecf <+15>:    mov    (%eax),%eax
   0x08048ed1 <+17>:    mov    %eax,(%esp)
   0x08048ed4 <+20>:    call   0x8049710 <atoi>
   0x08048ed9 <+25>:    cmp    $0x1a7,%eax
   0x08048ede <+30>:    jne    0x8048f58 <main+152>
   0x08048ee0 <+32>:    movl   $0x80c5348,(%esp)
   0x08048ee7 <+39>:    call   0x8050bf0 <strdup>
   0x08048eec <+44>:    mov    %eax,0x10(%esp)
   0x08048ef0 <+48>:    movl   $0x0,0x14(%esp)
   0x08048ef8 <+56>:    call   0x8054680 <getegid>
   0x08048efd <+61>:    mov    %eax,0x1c(%esp)
   0x08048f01 <+65>:    call   0x8054670 <geteuid>
   0x08048f06 <+70>:    mov    %eax,0x18(%esp)
   0x08048f0a <+74>:    mov    0x1c(%esp),%eax
   0x08048f0e <+78>:    mov    %eax,0x8(%esp)
   0x08048f12 <+82>:    mov    0x1c(%esp),%eax
   0x08048f16 <+86>:    mov    %eax,0x4(%esp)
   0x08048f1a <+90>:    mov    0x1c(%esp),%eax
   0x08048f1e <+94>:    mov    %eax,(%esp)
   0x08048f21 <+97>:    call   0x8054700 <setresgid>
   0x08048f26 <+102>:   mov    0x18(%esp),%eax
   0x08048f2a <+106>:   mov    %eax,0x8(%esp)
   0x08048f2e <+110>:   mov    0x18(%esp),%eax
   0x08048f32 <+114>:   mov    %eax,0x4(%esp)
   0x08048f36 <+118>:   mov    0x18(%esp),%eax
   0x08048f3a <+122>:   mov    %eax,(%esp)
   0x08048f3d <+125>:   call   0x8054690 <setresuid>
   0x08048f42 <+130>:   lea    0x10(%esp),%eax
   0x08048f46 <+134>:   mov    %eax,0x4(%esp)
   0x08048f4a <+138>:   movl   $0x80c5348,(%esp)
   0x08048f51 <+145>:   call   0x8054640 <execv>
   0x08048f56 <+150>:   jmp    0x8048f80 <main+192>
   0x08048f58 <+152>:   mov    0x80ee170,%eax
   0x08048f5d <+157>:   mov    %eax,%edx
   0x08048f5f <+159>:   mov    $0x80c5350,%eax
   0x08048f64 <+164>:   mov    %edx,0xc(%esp)
   0x08048f68 <+168>:   movl   $0x5,0x8(%esp)
   0x08048f70 <+176>:   movl   $0x1,0x4(%esp)
   0x08048f78 <+184>:   mov    %eax,(%esp)
   0x08048f7b <+187>:   call   0x804a230 <fwrite>
   0x08048f80 <+192>:   mov    $0x0,%eax
   0x08048f85 <+197>:   leave
   0x08048f86 <+198>:   ret
End of assembler dump.
```

On observe la comparaison <code>$0x1a7,%eax</code> qui nous permet d'eviter le jump et ainsi continuer le programme qui va effectuer un **execv**
> 0x1a7 = 423 en hexadécimal

On lance donc le binaire avec **423** et on recupere le flag:
<pre><code>> ./level0 423
> cd ../level1 && cat .pass
1fe8a524fa4bec01ca4ea2a869af2a02260d4a7d5fe7e7c24d8617e6dca12d3a
</code></pre>

For download :
<pre><code>scp -P4242 level0@192.168.1.78:level0 .</code></pre>
> Password : level0