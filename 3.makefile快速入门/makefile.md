第一节课，我们在编译c++文件的时候，会用到下面这很长一串命令
g++ helloworld.cpp -o helloworld
我们觉得他太长了，想用一个短的命令来完成编译
这就是我们这节课学习的makefile
用了makefile之后，我们只需要输入
make
命令
就可以完成编译
原理就是我们把
g++ helloworld.cpp -o helloworld
这一长串命令写进一个文件里，然后我们通过这个文件提供的信息来实现编译命令
这个文件就是Makefile文件，，然后用到make命令来识别makefile文件里的信息
我们先尝试手动完成一个helloworld.cpp的编译