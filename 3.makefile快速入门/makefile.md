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
首先，创建一个Makefile文件，在文件中写下如下命令   
```
g++ helloworld.cpp -o helloworld
```
此时我们可以试一下通过makefile编译C++   
在Makefile文件所在位置输入命令   
make   
会显示   
`Makefile:1: *** 缺失分隔符。 停止。`
这是因为Makefile不认识这一串命令   
也就是说，它不符合makefile的语法   
这节课我们不教大家makefile语法，大家只需要简单的知道makefile能干嘛用就可以   
回到Makefile文件   
我们把这个命令改成Makefile认识的格式   
```
anyname:
	g++ helloworld.cpp -o helloworld
```
这样他就认识了。此时我们保存，再运行make命令，就会发现   
终端显示了我们的g++命令   
文件夹里也出现了helloworld文件   
此时我们可以运行一下这个文件，会发现，完全没有异常   
   
用makefile的一个好处就是可以同时编译多个文件   
比如我们有一个打印helloworld的cpp文件   
还有一个打印Lizzy的cpp文件   
我们如果用之前的方法，用g++，要输入两串很长的命令   
如果我们用makefile,只需要输入make就可以把他们全部编译出来   
现在我们创建一个Lizzy.cpp，让他能够打印字符串   
然后我们来编辑Makefile文件   
```
helloworld:
	g++ helloworld.cpp -o helloworld
Lizzy:
	g++ Lizzy.cpp -o Lizzy
```
把刚刚创建好的helloworld文件删除掉   
这个时候，我们可以输入make命令   
发现，只生成了helloworld   
我们把helloworld文件删了，运行如下命令   
make Lizzy   
发现没有，生成的就只有Lizzy文件了   
现在我们把Lizzy文件删了，之后运行   
make helloworld   
他生成的就只有helloworld文件了   
所以我们可以通过make命令   
在make后加上makefile中的name,就可以运行那个name对应的命令   
当然，如果只有make,make后面没有name,那么执行的就是Makefile文件中第一个name   
现在我有一个方法，可以直接一个make,不用输入后面的name,也能将两个name同时编译   
就是写上第一个name,   
然后在 ： 后面写上我们希望执行的命令对应的name   
比如，我给第一个name命名为helloworldandlizzy,表示我要运行helloworld和lizzy对应的命令   
```
helloworldandlizzy:helloworld Lizzy
	

helloworld:
	g++ helloworld.cpp -o helloworld
Lizzy:
	g++ Lizzy.cpp -o Lizzy
```
现在我们直接输入make,就可以直接生成两个可执行文件   
不过一般我们不命名为helloworldandlizzy   
我们把它命名为all   
这样是更符合命名规范的   
```
all:helloworld Lizzy


helloworld:
	g++ helloworld.cpp -o helloworld
Lizzy:
	g++ Lizzy.cpp -o Lizzy
```

如果想快速删除生成的文件，也没问题   
我们首先学一下linux怎么用命令删除文件   
在终端进入某个文件夹后，我们可以ls一下，看看这个文件夹里有什么文件   
比如这里我们ls,发现有helloworld文件，有lizzy文件，和其他的文件   
我们想通过命令删除lizzy文件，就在当前文件夹下输入下面的命令   
rm Lizzy   
这样这个文件就删掉了   
我们顺手把helloworld文件也删掉   
   
接下来，我们重新make,来生成这两个文件   
然后我们进入Makefile文件，写一个name,让这个name对应的命令来实现文件的删除   
```
qingchu:
	rm Lizzy
	rm helloworld
```
这样，我们就可以通过make qingchu命令来删除前面生成的文件   
但是，我们一般给它命名为clean.这样是符合命名规范的   
也就是   
```
clean:
	rm Lizzy
	rm helloworld
```
这个时候，我们只需要输入   
make clean   
就可以清除我们在Makefile文件里制定的文件   

