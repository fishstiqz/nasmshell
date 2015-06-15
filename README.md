# nasmshell

## commands

1. **as, assemble** - set to assembly mode
2. **disas** - set to disassembly mode
3. **bits** - set bits (32 or 64)
4. **exit, quit** - exit shell

## examples

### assembling

```
$ nasmshell
nasm> push eax
50                       push eax
nasm> push eax ; retn 4
50                       push eax
C20400                   ret 0x4
nasm> push eax ; call [eax+1ch]
50                       push eax
FF501C                   call dword [eax+0x1c]
nasm> inc ecx; loop: push eax; push ebx; jmp loop
41                       inc ecx
50                       push eax
53                       push ebx
EBFC                     jmp short 0x1
nasm> times 3 movsb
A4                       movsb
A4                       movsb
A4                       movsb
```

### disassembling

```
nasm> disas
disas mode
ndisasm> 50ff501c
50                       push eax
FF501C                   call dword [eax+0x1c]
ndisasm> 4141414141414141
41                       inc ecx
41                       inc ecx
41                       inc ecx
41                       inc ecx
41                       inc ecx
41                       inc ecx
41                       inc ecx
41                       inc ecx

```

### x86-64

```
ndisasm> bits 64
ndisasm> as
assemble mode
nasm> push rax
50                       push rax
nasm> push rax ; push rbx
50                       push rax
53                       push rbx
nasm> jmp pastsym; sym: db 0x11,0x01,0x11,0xff; pastsym: lea rax, [rel sym]
EB04                     jmp short 0x6
1101                     adc [rcx],eax
11FF                     adc edi,edi
488D05F5FFFFFF           lea rax,[rel 0x2]
```

