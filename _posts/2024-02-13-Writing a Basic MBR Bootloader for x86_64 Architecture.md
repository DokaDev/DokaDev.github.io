---
title: Writing a Basic MBR Bootloader for x86_64 Architecture
date: 2024-02-13 01:10 +0900
categories: [Computer Science, System Programming]
tags: [nasm, x86_64, bootloader]     #TAG names should always be lowercase
---
When you turn on your computer, it doesn't immediately jump into the operating system.
Did you know that?
A crucial player is the `bootloader`.
In this post, we're going to craft a bootloader for the x86_64 architecture from scratch.
Before we dive into coding, let's first understand what MBR is.

## What is MBR(Master Boot Record)?
MBR is a 512-byte area at the beginning of the disk, containing the code necessary for booting along with partition information.
This area is structured as follows:

## How the Bootloader Works
When the computer is powered on, the BIOS or UEFI finds and loads the MBR into memory and executes it.
The code in the MBR then loads the next stage bootloader or directly starts the operating system.

## Setting Up the Development Environment
To develop a bootloader, we need to install NASM and QEMU. NASM will translate our assembly code into machine code, and QEMU will allow us to test our bootloader in a virtual environment.

### Installing NASM
Linux users can install it through their package manager:
```bash
sudo apt-get install nasm
```

### Installing QEMU
```bash
sudo apt-get install qemu
```

## Writing Your First MBR Bootloader Code
Let's start with a simple example.
This code will display the message "Hello, MBR!" on the screen.

```assembly
[org 0x7c00]  ; The MBR is loaded at address 0x7c00.

mov ah, 0x0e  ; BIOS interrupt for printing characters in text mode
mov bh, 0x00  ; Page number
mov bl, 0x07  ; Character color (light gray)

; Printing the "Hello, MBR!" message
mov si, msg
print_char:
    lodsb      ; Load the character from SI register and increment SI
    or al, al  ; Check if the character is 0 (end of the string)
    jz hang    ; If 0, jump to infinite loop
    int 0x10   ; Call BIOS video service to print the character on the screen
    jmp print_char

; Infinite loop
hang:
    jmp hang

msg db 'Hello, MBR!', 0

times 510-($-$$) db 0  ; Fill the boot sector to 512 bytes
dw 0xaa55               ; Signature at the end of the boot sector
```

### Compiling and Running the Code
Save this code as `hello_mbr.asm`, then use NASM to compile it into a binary:

```bash
nasm -f bin hello_mbr.asm -o hello_mbr.bin
```
And test it with QEMU:
```bash
qemu-system-x86_64 -fda hello_mbr.bin
```

In this post, we've looked at the basics of MBR bootloader structure and walked through a simple example of writing bootloader code in assembly language.
Of course, this is just the beginning, and bootloaders can perform more complex functions.
Topic like loading the actual operating system or switching to protected mode(32bit) require further exploration.

With these basics in hand, you can experiment further, such as using your bootloader to load your own operating system.
Understanding the boot process is a crucial foundation in system programming, and this knowledge will be a valuable asset as you design and implement more complex systems.