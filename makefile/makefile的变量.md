objects = main.o input.o calcu.o
main: $(objects)
	gcc -o main $(objects)
其中objects就是一个变量，有点像是python中的写法。
