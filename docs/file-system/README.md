# 文件系统

文件系统为用户提供了在计算机系统中对数据信息进行长期、大量存储和访问对功能。

## 文件

### 文件命名

所有操作系统都允许用1-8个字母组成的字符串作为文件名。
多数操作系统都支持文件名用圆点隔开氛围两部分，圆点后面的部分分为文件扩展名。

### 文件结构

1. 无结构字节序列

无结构字节序列也称为流式文件. 操作系统不知道也不关心文件内容是什么，操作系统所见到的就是字节。

2. 固定长度记录序列

构成文件的基本单位是具有固定长度的记录，每个记录都有其内部结构。把文件作为记录序列的中心思想是：读操作返回一个记录，而写操作重新或者追加一个记录。


3. 树形结构

文件由一棵记录树构成，记录长度不定，在记录的固定位置包含一个关键字域.记录树按关键字域排序。

### 文件类型

文件的类型有正规文件、目录文件、字符设备文件和块设备文件等。

正规文件包含用户信息，一般分为ASCII文件和二进制文件。

目录文件用于管理文件的系统文件。

字符设备文件和输入输出有关，用于串行I/O类设备。

1. ASCII （Amercian Standard Code for Information Interchange）文件

ASCII文件由多行正文组成, 在某些系统中每行用回车符结束， 某些则用换行符结束，而有些系统还同时采用回车符和换行符。
ASCII文件的明显优势是可以显示和打印，也可以用通常的文本编辑器进行编辑。

2. 二进制文件

具有一定的内部结构，如可执行的.exe 文件。 必须用专门的二进制文件编辑器，不同的操作系统可以识别不同的二进制文件。

### 文件存取

用户通过对文件对存取来完成对文件对各种操作，文件对存取方式是由文件对性质和用户使用文件对情况确定的。常用的文件存取方式由两种，顺序存取和随机存取。

1. 顺序存取

早起的操作系统只有顺序存取这一种文件存取方式。进程可以从文件开始处读取文件中的所有字节或记录，但不能跳过某些内容，也不能不按顺序存取。

2. 随机存取

随机存取又称直接存取，即可以以任意顺序读取文件中但字节或者记录。现代操作系统的文件一旦被创建，所有文件自动成为随机存取文件。定长记录的文件能很好地支持随机存取，而变长记录虽然可以随机存取，但实现起来复杂而且存取速度慢。


### 文件属性

为方便管理，除了文件名和文件数据外，文件系统还会保存其他与文件相关的信息，如文件的创建日期，文件大小和修改时间等，这些附加信息成为文件属性。

文件属性在不同操作系统中差别很大。

### 文件操作

使用文件等目的是存储信息并方便以后检索。 不同的系统提供了不同的操作来存储和检索信息。

1. CREATE 

该操作完成创建文件的功能，并设置文件的一些属性。

2. DELETE

当不再需要某个文件时，删除该文件并释放磁盘空间。

3. OPEN

在使用文件之前，必须先打开文件。 OPEN 调用的目的是将文件属性和文件的地址信息装入主存，便于在对文件的后续访问中能快速存取文件信息。

4. CLOSE

当存取结束后，不再需要文件属性和地址信息，这时应该关闭文件以释放内部表空间。很多系统限制进程打开文件的个数，以鼓励用户关闭不再使用的文件。

5. READ

从文件中读取数据。 一般地，用户可以指定从哪个文件的第几个字节开始读取多少个字节的内容。

6. WRITE

从文件中写数据，写操作一般从写函数的参数指定的文件位置开始。如果当前位置是文件末尾，文件长度增加。如果当前位置在文件中间，则现有数据被覆盖，并且永远丢失。

7. APPEND

该操作是WRITE调用的限制形式，它只能在文件末尾添加数据。

8. SEEK

对于随机存取文件，要指定从何处开始取数据。 通常的做法是用 SEEK 系统调用把当前位置指针指向文件中特定的位置。SEEK调用结束后，就可以从该位置读写数据了。

9. GETATTRIBUTES

该操作用于获取文件属性。

10. SETATTRIBUTES

某些属性是可由用户设置的，文件创建以后，用户还可以通过系统调用SETATTRIBUTES 来修改它们。

11. RENAME

该操作用于修改已有文件的文件名。


## 目录

文件系统通常提供目录或文件夹用于记录文件，很多系统中目录本身也是文件，目录是文件系统中实现按名访问文件的重要数据结构。

### 层次目录系统

1. 目录文件的结构

目录文件由两种常见的结构：属性放在目录项中和放在i结点中。
文件目录包含许多目录项，每个目录项用于描述一个文件。

在第一种结构中，每个目录项长度相同，每个文件对应一个目录项。 其中包含文件名、文件属性和文件的地址。

在第二种结构中，目录项中有一个文件名和i结点号。 i结点是一种数据结构，文件属性和文件的地址信息存放在i结点中。


2. 目录结构

文件目录的组织和管理是文件管理的一个重要方面，包括单层目录，两级目录和树形目录。

(1) 单层目录

这种目录也被称为根目录。在整个系统中设置一张线性目录表，表中包括了所有文件的描述信息。

使用单层目录时，要查找一个文件必须对单层目录表中的所有文件信息项进行搜索，因而搜索效率也较低。

(2) 两级目录

为了避免文件名冲突，一种改进的方法是为每个用户提供一个私有目录。这样，一个用户选择文件名时就不会影响到其他用户。

使用两级目录的优点是解决来文件的重名问题和文件共享问题，查找时间降低。缺点是增加了系统的存储开销。

(3) 树形目录

把两级目录的层次关系加以推广，就形成了多级目录，又称树形目录。

树形目录的优点是便于文件的分类，层次结构清晰，便于管理和保护，解决了重名问题问题，查找速度加快。

缺点是查找一个文件按路径名逐层检查，由于每个文件都放在外存中，多次访问磁盘会影响速度，结构相对复杂。


### 路径名

用目录树组织文件系统时，需要有某种方法指明文件名。常用的方法有两种：绝对路径名和相对路径名。

1. 绝对路径名

绝对路径名由从根目录到文件的路径组成。

2. 相对路径名

当访问一个文件系统的目录包含很多级时，如果访问每个文件都要从根目录开始，直到叶子的文件名为止，包含所有经过的各级分目录在内的全路径名是相当麻烦的。

在设计文件系统时，可以允许用户指定一个目录作为当前的工作目录，所有的不从根目录开始的路径名都是相对于工作目录的。

### 目录操作

1. CREATE

根据给定的目录文件名，创建目录。 除了目录项 " . " 和 " .. " 外，目录内容为空。 

2. DELETE

删除目录，根据指定的目录名删除一个目录文件。

3. OPENDIR

目录内容可以被读取

4. CLOSEDIR

读目录结束后，应关闭目录以释放内存表空间。

5. READDIR

以标准格式返回打开目录的下一步目录项。

6. RENAME

更换目录名

## 文件系统的实现

### 实现文件

1. 连续分配

顾名思义，连续分配就是把每个文件作为一连串连续数据块存储在磁盘上。

连续分配方式有两大优点： 首先，实现简单，记录每个文件用到的簇仅需存储两个数字即可：第一块的磁盘空间和文件的块数。给定第一块的簇号，就可以找到任何其他块的簇号。其次，读操作性能好，在单个操作中就能从磁盘上读取整个文件。只需要寻找一次第一个块，之后不再需要寻道和旋转延迟，所以数据以磁盘全带宽的速率输入。

2. 使用磁盘链接表的分配

该方法为每个文件构造簇的链接表，每个簇开始的几个字节用于存放下一个簇的簇号，簇的其他部分存放数据，每个文件可以存放在不连续的簇中，在目录项中只需存放第一个数据块的磁盘地址，文件的其他块可以根据这个地址来查找。

3. 使用内存的链接表分配

该方法是将文件所在的磁盘的簇号存放在内存的表中。访问文件时，只需从内存文件分配表中顺着某种链接关系查找簇号，不管文件有多大，在目录项中只需记录文件的第一块数据所在簇的簇号，根据它查找到文件的所有块。

4. i结点

该方法为每个文件赋予一个被称为i结点的数据结构。

### 实现目录

系统在读文件前，必须先打开文件。打开文件时，操作系统利用用户给出的路径名找到相应的目录项，目录项中提供来查找文件簇所需要的信息。

1. CP/M 中的目录

CP/M是一个微机操作系统，它只有一层目录，因此只有一个目录文件。 要查找文件名，就是在这个唯一的目录文件中找到文件对应的目录项，从目录项中获得文件存放的磁盘地址。

2. MS-DOS 中的目录

MS-DOS 文件系统曾经是IBM PC系列所采用的文件系统，目前它已经不再是新的PC文件系统的标准来，但它和它的扩展（FAT32）一直被许多嵌入式系统所广泛使用。大部分的数码相机，MP3使用了它，

3. UNIX 中的目录

每个目录项只包含一个文件名及其i结点号。 有关文件类型、长度、时间、所有者和簇号等信息都放在i结点中。
当打开某个文件时，文件系统必须要获得文件名并且定位文件所在的第一个簇。


### 磁盘空间管理

磁盘空间管理是文件系统的重要功能，包括记录空闲磁盘信息、设计文件的存放方式，以及规定文件系统的簇大小等内容。

1. 簇大小

文件系统为文件分配磁盘空间是以簇为单位的，一旦用固定大小的簇来存储文件，就会出现一个问题：簇的大小应该是多少？

拥有大的簇尺寸意味着每个文件，甚至一个字节的文件，都要占用很大的空间，也就是说小的文件浪费了大量的磁盘空间。另一方面，小的尺寸意味着大多数文件会跨越多个簇，因此需要多次寻道与旋转延迟才能读出它们，从而降低来时间性能。因此，簇太大，容易造成空间的浪费；簇太小，则会使访问文件的时间延长。

2. 记录空闲块

(1)空闲簇链接表

用一些空间簇存放空闲簇的簇号。一个簇存放尽可能多的空闲簇的簇号，并专门留出最后几个字节存放指向下一个存放空闲簇的指针，

(2)

用n位图对应磁盘的n个簇，在位图中，空闲簇用1表示，已分配簇用0表示（或者反过来）
