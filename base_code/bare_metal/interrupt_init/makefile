#定义变量，用于保存编译选项和头文件保存路径
header_file := -fno-builtin -I$(shell pwd)/include
export header_file


all : start.o main.o device/device.o 
	arm-none-eabi-ld -Tbase.lds $^ -o base.elf 
	arm-none-eabi-objcopy -O binary -S -g base.elf base.bin


%.o : %.S
	arm-none-eabi-gcc -g -c $^ 
%.o : %.c
	arm-none-eabi-gcc $(header_file) -c $^ 	

#调用其他文件的makefile
device/device.o :
	make -C device all


.PHONY: copy
copy:
	cp ./base.bin  /home/pan/download/embedfire

#定义清理伪目标
.PHONY: clean
clean:
	make -C device clean
	-rm -f *.o *.elf *.bin 


	
