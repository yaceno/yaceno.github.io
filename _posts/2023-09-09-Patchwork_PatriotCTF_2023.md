---
title: Coffee Shop - PatriotCTF 2023
date: 2023-09-09 +0200
tags: [Reverse engineering]
categories: [Write-ups]
---

## Challenge

Here's a write-up for a reverse challenge.  
The challenge description :  

![i2](../../assets/patriotctf2023/patchwork_chall.png)

## Exploitation

We open the file with gdb and then disassemble the main function which is often the most interesting function in reverse challenges.

`gdb ./patchwork`

```
(gdb) disas main
Dump of assembler code for function main:
   0x0000000000001139 <+0>:     push   %rbp
   0x000000000000113a <+1>:     mov    %rsp,%rbp
   0x000000000000113d <+4>:     sub    $0x10,%rsp
   0x0000000000001141 <+8>:     movl   $0x0,-0x4(%rbp)
   0x0000000000001148 <+15>:    lea    0xeb9(%rip),%rax        # 0x2008
   0x000000000000114f <+22>:    mov    %rax,%rdi
   0x0000000000001152 <+25>:    call   0x1030 <puts@plt>
   0x0000000000001157 <+30>:    lea    0xeda(%rip),%rax        # 0x2038
   0x000000000000115e <+37>:    mov    %rax,%rdi
   0x0000000000001161 <+40>:    call   0x1030 <puts@plt>
   0x0000000000001166 <+45>:    cmpl   $0x0,-0x4(%rbp)
   0x000000000000116a <+49>:    je     0x1176 <main+61>
   0x000000000000116c <+51>:    mov    $0x0,%eax
   0x0000000000001171 <+56>:    call   0x117d <give_flag>
   0x0000000000001176 <+61>:    mov    $0x0,%eax
   0x000000000000117b <+66>:    leave
   0x000000000000117c <+67>:    ret
End of assembler dump.
```

We clearly see that the goal here is to bypass the jump following the comparison.  

So we use the break command to stop the execution of the program at the jump instruction : `(gdb) break *0x000055555555516a`.  
And then we replace je by jne so that our comparison will be correct (jne means jump if not equal):  
`set {unsigned char}0x000055555555516a = 0x75`  
What we have typed set the opcode of jne which is 0x75 instead of the one of je instruction.  
  
And we finish the execution !

```
(gdb) next
Single stepping until exit from function main,
which has no line number information.
PCTF{JuMp_uP_4nd_g3t_d0Wn}
```

Flagged !
