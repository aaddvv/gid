# КАК НАПИСАТЬ ОС. ПОШАГОВАЯ ИНСТРУКЦИЯ ОТ АЛЕКСЕЯ

# ПОДГОТОВКА



Скачайте и установите vm ware

Далее скачайте образ kali linux(можно любой другой linux,но для него команды могут отличаться) и установите на vm ware (графическую версию) 

Запустите наш линукс, откройте в нем командную строку(далее - терминал) и там вводите команды в терминал, указанные в пунктах. (команды выделенны)

Если у вас не установленны необходимые программы,их можно установить командами:

    apt update       

    apt upgrade          

    apt install git            

    apt install nasm               

    apt install gcc            

    apt install ld             



# ЗАГРУЗКА ФАЙЛОВ



    git clone https://github.com/arjun024/mkernel.git

    cd mkernel



# КОМАНДЫ СБОРКИ



Необязательно:

Код нашей ОС написан на си, его можно отредактировать. Он находится в файле kernel.c 
Чтобы отредактировать код, введите 

    nano kernel.c

Обязательно(команды сборки):

    nasm -f elf32 kernel.asm -o kasm.o

    gcc -m32 -c kernel.c -o kc.o

    ld -m elf_i386 -T link.ld -o kernel kasm.o kc.o




Если выдает ошибку,то есть готовый файл в папке binary_x86 :

    cd binary_x86



# ТЕСТ НА ЭМУЛЯТОРЕ(необязательно)



Только если установлен эмулятор qemu

    qemu-system-i386 -kernel kernel



# ПРИСТУПАЙТЕ К ЗАГРУЗКЕ



GRUB требует, чтобы исполняемый файл ядра соответствовал шаблону.kernel-версия

Итак, переименуйте ядро:

    mv kernel kernel-701

Скопируйте его в загрузочный раздел (при условии, что вы суперпользователь):

    cp kernel-701 /boot/kernel-701



# УСТАНОВКА ЗАПУСК И НАСТРОЙКА



    apt install grub

    grub-install /dev/hda



    grub

ввести в терминале grub, он выглядит так:     grub>

    title ALEXsystem
	
	root (hd0,0)
	
	kernel /boot/kernel-701 ro
далее перезагрузитесь и загрузите вашу ос. 
все. Слава россие. Вы написали ос по гениальному гайду от Алексея.
