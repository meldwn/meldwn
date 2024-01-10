```asm
section .data
    message db 72, 105, 32, 58, 51

section .text
    global _start

_start:
    mov eax, 4
    mov ebx, 1
    mov ecx, message
    mov edx, 5

    xor esi, esi

    encode_loop:
        cmp esi, edx
        jge done

        mov al, byte [ecx + esi]
        add al, 5

        push eax
        pop eax
        dec al

        mov dl, al
        sub dl, 2
        push edx

        pop edx
        sub dl, 1
        mov al, dl

        int 0x80

        inc esi
        jmp encode_loop

    done:
    mov eax, 1
    xor ebx, ebx
    int 0x80
```
