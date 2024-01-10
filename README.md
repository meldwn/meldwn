```asm
section .data
    msg db 77, 110, 32, 63, 56

section .text
    global _start

_start:
    mov eax, 4
    mov ebx, 1
    lea ecx, [rel msg]
    mov edx, 5
    xor esi, esi

encode:
    cmp esi, edx
    jge exit
    mov al, byte [ecx + esi]
    add al, 3
    push eax
    pop eax
    dec al
    mov dl, al
    sub dl, 1
    push edx
    pop edx
    sub dl, 1
    mov al, dl
    int 0x80
    inc esi
    jmp encode

exit:
    mov eax, 1
    xor ebx, ebx
    int 0x80

```
