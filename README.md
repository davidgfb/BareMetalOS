# BareMetalOS
main.img es el resultado de escribir en la terminal de ubuntu

printf '\364%509s\125\252' > main.img <br>
sudo apt-get install qemu-system-x86 <br>
qemu-system-x86_64 -hda main.img

Las comprobaciones de que hlt corresponde con f4 en hexadecimal o \364 en octal se pueden realizar mediante los siguientes comandos

echo hlt > a.S <br>
as -o a.o a.S <br>
objdump -S a.o <br>

Binutils incluye los siguientes comandos: as - ensamblador 

El comando 

hd main.img

da como salida el archivo 2.txt donde se aprecian los primeros 512 bytes que cargara el firmware de la BIOS

El argumento %509s escribe 509 espacios o 20 en ASCII para llegar hasta el byte 510 
\125\252 en octal es 55 y AA en hexadecimal que son los dos bytes magicos 511 y 512 que la BIOS interpretara como unidad arrancable
El firmware de la bios tan solo recoge estos primeros 512 bytes que forman parte del primer sector MBR y los carga en la RAM apuntando al primer byte

El desensamblado de main.o dara lugar a 3.txt, sin necesidad de linker.ld tan solo con el comando make y el codigo de https://stackoverflow.com/questions/22054578/how-to-run-a-program-without-an-operating-system/32483545, repitiendo el comando objdump asi como el del nuevo main.img dara lugar a 4.txt con el anterior comando hd

Mas codigo usado en main.S

    .code16: tells GAS to output 16-bit code

    cli: disable software interrupts. Those could make the processor start running again after the hlt

    int $0x10: does a BIOS call. This is what prints the characters one by one.

The important link flags are:

    --oformat binary: output raw binary assembly code, don't wrap it inside an ELF file as is the case for regular userland executables.
   
En C
5.txt es el resultado de hacer hd a main.img construido desde main.c 
6.txt es el resultado de hacer objdump a main.o desde main.c

