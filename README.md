# BareMetalOS
main.img es el resultado de escribir en la terminal de ubuntu

printf '\364%509s\125\252' > main.img <br>
sudo apt-get install qemu-system-x86 <br>
qemu-system-x86_64 -hda main.img

Las comprobaciones de que hlt corresponde con f4 en hexadecimal o \364 en octal se pueden realizar mediante los siguientes comandos

echo hlt > a.S <br>
as -o a.o a.S <br>
objdump -S a.o <br>

