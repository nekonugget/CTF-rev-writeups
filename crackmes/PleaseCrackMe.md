This can be solved using GDB.

First, 
`gdb-pwndbg PleaseCrackMe`

## Getting an overview of the program:
info functions
run - See that it prompts us for a username, number, and password.
Now that we know our likely goal, we `disass main`.
We can see a flow which one can figure out is very similar to what we just ran,
with the strcmp on call +288 likely comparing the password:
```
   0x0000555555555309 <+288>:   call   0x5555555550e0 <strcmp@plt>
   0x000055555555530e <+293>:   test   eax,eax
   0x0000555555555310 <+295>:   jne    0x555555555320 <main+311>
   0x0000555555555312 <+297>:   lea    rdi,[rip+0xd87]        # 0x5555555560a0
   0x0000555555555319 <+304>:   call   0x5555555550a0 <puts@plt>
   0x000055555555531e <+309>:   jmp    0x55555555532c <main+323>
   0x0000555555555320 <+311>:   lea    rdi,[rip+0xd98]        # 0x5555555560bf
   0x0000555555555327 <+318>:   call   0x5555555550a0 <puts@plt>
```

So we set a breakpoint on this address.
`bp main+288`
And `run` the program again.
Giving a random username and number will produce different passwords.
Give it a user and number which you remember, then take the generated
password once hitting the breakpoint:

```
 ► 0x555555555309 <main+288>    call   strcmp@plt                <strcmp@plt>
        s1: 0x7fffffffdd50 ◂— 0x656565 /* 'eee' */
        s2: 0x7fffffffdd70 ◂— 0x6b6469 /* 'idk' */
```

My password is 'idk'. s1 is therefor likely the password.
Indeed, removing the breakpoint with `delete`, giving same username and number, with 'eee' as pass,
shows we successfully solved the challenge.
