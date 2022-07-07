README.md

КАК НАПИСАТЬ ОС. ПОШАГОВАЯ ИНСТРУКЦИЯ ОТ АЛЕКСЕЯ

ПОДГОТОВКА

Скачайте и установите vm ware

Далее скачайте образ kali linux(можно любой другой другой linux,но для него команда может выбрать вариант) и установите на vm ware (графическую версию)

Запускаем наш линукс, переносим в нем командную строку(далее - терминал) и там вводим команду в терминал, возвращаем в точки. (команды выделенны)

Если у вас не установлены определенные программы, их можно установить командами:

apt update       

apt upgrade          

apt install git            

apt install nasm               

apt install gcc            

apt install binutils             

ЗАГРУЗКА ФАЙЛОВ

git clone https://github.com/arjun024/mkernel.git

cd mkernel

КОМАНДЫ СБОРКИ

Необязательно:

Код нашей ОС написан на си, его можно отредактировать. Он находится в файле kernel.c Чтобы отредактировать код, введите

nano kernel.c

Обязательно(команды сборки):

nasm -f elf32 kernel.asm -o kasm.o

gcc -m32 -c kernel.c -o kc.o

ld -m elf_i386 -T link.ld -o kernel kasm.o kc.o

Если выдает ошибку,то есть готовый файл в папке binary_x86 :

cd binary_x86

ТЕСТ НА ЭМУЛЯТОРЕ(необязательно)

Установка :

apt install qemu

Тест:

qemu-system-i386 -kernel kernel

ПРИСТУПАЙТЕ К ЗАГРУЗКЕ

GRUB требует, чтобы исполняемый файл ядра использовал шаблону.kernel-версия

Итак, переименуйте ядро:

mv kernel kernel-701

Скопируйте в загрузочный раздел (при условии, что вы суперпользователь):

cp kernel-701 /boot/kernel-701

УСТАНОВКА ЗАПУСК И НАСТРОЙКА

apt install grub

grub-install /dev/hda

grub

ввести в терминале grub, он выглядит так: grub>

title ALEXsystem

root (hd0,0)

kernel /boot/kernel-701 ro

Далее перезагрузитесь и загрузите вашу ос. Все. Слава России. Вы написали ос по гениальному гайду от Алексея. that can read the characters `a-z` and `0-9` from the keyboard and print them on screen.

See the repo [mkernel](http://github.com/arjun024/mkernel) which is a minimal kernel that prints a string on the screen. mkeykernel just extends this to include keyboard support. 


#### Blog post ####

[Kernel 201 - Let’s write a Kernel with keyboard and screen support](http://arjunsreedharan.org/post/99370248137/kernel-201-lets-write-a-kernel-with-keyboard-and)

#### Build commands ####
```
nasm -f elf32 kernel.asm -o kasm.o
```
```
gcc -m32 -c kernel.c -o kc.o
```
```
ld -m elf_i386 -T link.ld -o kernel kasm.o kc.o
```

If you get the following error message:
```
kc.o: In function `idt_init':
kernel.c:(.text+0x129): undefined reference to `__stack_chk_fail'
```

compile with the `-fno-stack-protector` option:
```
gcc -fno-stack-protector -m32 -c kernel.c -o bin/kc.o
```

#### Test on emulator ####
```
qemu-system-i386 -kernel kernel
```

#### Get to boot ####
GRUB requires your kernel executable to be of the pattern `kernel-<version>`.

So, rename the kernel:

```
mv kernel kernel-701
```

Copy it to your boot partition (assuming you are superuser):

```
cp kernel-701 /boot/kernel-701
```

Configure your grub/grub2 similar to what is given in `_grub_grub2_config` folder of [mkernel repo](http://github.com/arjun024/mkernel).

Reboot.

Voila!

![kernel screenshot](http://31.media.tumblr.com/1afd75b433b13df613fa0c2301977893/tumblr_inline_ncy1p0kSGj1rivrqc.png "Screenshot")
