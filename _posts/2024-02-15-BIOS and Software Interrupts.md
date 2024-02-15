---
title: BIOS and Software Interrupts
date: 2024-02-15 23:04:00 +0900
image: 
    path: /assets/post/cs/1.png
    alt: The cover image is created by DALL-E
categories: [Computer Science, System Programming]
tags: [bios, software interrupts]     # TAG names should always be lowercase
---

Despite advancements in computer technology, there are a few core elements at the foundation of every computer system: BIOS and software interrupts. These elements provide a basic understanding of how computers boot up and how the operating system communicates with the hardware. In this article, we will explore their roles, importance, and practical applications through assembly language.

## In-depth Analysis of BIOS Services

BIOS stands for Basic Input/Output System and is the software that activates first when a computer is turned on. Its main roles include hardware initialization and system configuration. The BIOS ensures that all hardware is correctly set up and functioning before the CPU loads the operating system into memory.

* **Configure Interface**: Provides an interface for users to adjust settings such as the system clock, boot order, etc. This can directly impact the stability and performance of the system.
* **Hardware Compatibility Check**: Performs a self-check (Post Power-On Self Test) to ensure all peripherals and hardware components are correctly connected and functioning.
* **Operating System Loading**: Manages the process of finding and loading the operating system from a hard drive, SSD, or network.



## The importance of Software Interrupts

Software interrupts are signals or messages used when a program needs to perform a special task during execution. They are primarily used to access core functions of the operating system.

* **System Calls**: Program trigger software interrupts to use various functions of the operating system. This allows for file system access, network request handling, process management, etc.
* **Hardware Request Processing**: Software interrupts are also used to respond to events such as user input or changes in hardware status.



## Practical Use in Real Mode

Real mode refers to the processor operating in an 8086 compatible mode. In this mode, only 1MB of memory is accessible. BIOS services and software interrupts can be utilized in the following ways in real mode.

### IVT(Interrupt Vector Table)

IVT plays a crucial role in real mode, storing the addresses of interrupt service routines(ISR) corresponding to various system interrupts, set up to respond to different events. Below is a table summarizing a few key interrupts and their purposes.

| Interrupt Number(HEX) | Purpose                     | Description                                                  |
| --------------------- | --------------------------- | ------------------------------------------------------------ |
| 0x00                  | Zero Division Error         | Used for division operation errors like dividing by zero     |
| 0x02                  | NMI(Non-Maskable Interrupt) | Called in urgent situations like system crashes or hardware errors |
| 0x08                  | System Timer                | Interrupt triggered by the computer's system timer           |
| 0x09                  | Keyboard Interrupt          | Called when there is a key input from the keyboard           |
| 0x0E                  | Hard Disk Controller        | Handles interrupts from communication with the hard drive    |
| 0x13                  | Disk Services               | Used for disk operations like reading/writing                |
| 0x1C                  | System Timer Tick           | Interrupt triggered by the system timer at regular intervals |
| 0x21                  | DOS Functional Call         | Interrupt used to access DOS services                        |

This table briefly summarizes a few key interrupts defined in the IVT and their purposes. The IVT contains many other interrupts, and each hardware device or system service can communicate with the CPU through these interrupts.

IVT is used only in real mode, with alternative technologies or methods used in `protected mode` or more recent operating systems.



### Register Usage

Registers, each serving a specific function, allow the BIOS to provide the correct services.

- **AH**: Used to specify the service number, deciding which BIOS function to call.
- **AL**: Used within a function to select specific options or provide additional data. For example, AL is used to specify the video mode number when setting the video mode.
- **BH, BL**: Used to provide additional options in certain BIOS services. For example, in video services, BH can determine the page number, and BL can determine the color of the text.
- **CH, CL**: In disk services, CH and CL are used to specify the cylinder number and sector number, respectively.
- **DH, DL**: DH is used for the head number in disk services, and DL is used to specify the drive number (0 = A drive, 0x80 = first hard drive).



### NASM Assembly Language Examples and Applications

Assembly language is a low-level programming language that allows for close control of hardware and efficient programming. Using NASM examples, let's see how BIOS services can be called with actual assembly language code.

#### Setting Video Mode and Printing Characters

This is a basic method to visually display information to the user. Set the screen mode and print desired characters to the screen.

##### Setting Video Mode

```
mov ah, 0x00  ; Video mode set service
mov al, 0x03  ; Select 80x25 text mode
int 0x10      ; Call video interrupt
```

##### Printing Characters

```
mov ah, 0x0E  ; Character print service
mov al, 'A'   ; Character to print
mov bh, 0x00  ; Page number
mov bl, 0x07  ; Character color (e.g., bright gray)
int 0x10      ; Call video interrupt
```



#### Disk Services

Data storage and retrieval are core functions of all computer systems. Learn how to read and write data to disks using NASM code.

##### Reading a Sector from Disk

```
mov ah, 0x02       ; Sector read service
mov al, 1          ; Number of sectors to read
mov ch, 0          ; Cylinder number
mov cl, 1          ; Sector number
mov dh, 0          ; Head number
mov dl, 0          ; Drive number (0 = A drive, 0x80 = first hard drive)
mov bx, buffer     ; Memory address to store data
int 0x13           ; Call disk interrupt

buffer:            ; Buffer to read data into
    resb 512       ; Reserve buffer space for sector size
```

---

Personally, exploring and understanding BIOS and software interrupts is a journey that extend fundamental perceptions of computer science. These technologies provide deep insights into how our daily-used computers and digital devices "think" and "act", aiding in the process of finding creative solutions to technical problems.

Especially learning to communicate directly with the system through low-level languages like assembly language broadens a programmer's perspective and enhances the ability to solve complex problems. This knowledge not only advances technical skills but also deepens our fundamental understanding of how we interact with the digital world, potentially laying the groundwork for new technological innovations.