the inspection of a file path is very limited, and it only covers Nul character check.
limited 有限的

# 传统IO

File 类是文件和目录路径名的抽象表示形式，与平台无关
File 能新建、删除、重命名文件和目录，但 File 不能访问文件内容本身。如果需要访问文件内容本身，则需要使用输入/输出流。
File对象可以作为参数传递给流的构造函数


FileInputStream FileOutputStream   read和write方法的使用


FileReader extends InputStreamReader ---> FileInputStream 
FileWriter  

缓冲流
BufferedInputStream BufferedOutputStream
BufferedReader BufferedWriter

转换流
InputStreamReader   OutputStreamWriter

标准流
System.in   System.out

输出到文件PrintStream
System.setOut(PrintStream ps)
可能是直接把ps赋值给了out
怎么再恢复到输出到控制台

ObjectInputStream   ObjectOutputStream
要实现序列化的类： 
 * 1.要求此类是可序列化的：实现Serializable接口
 * 2.要求类的属性同样的要实现Serializable接口
 * 3.提供一个版本号：private static final long serialVersionUID
 * 4.使用static或transient修饰的属性，不可实现序列化

RandomAccessFile
读取，写入操作 seek()方法定位指针



# Java直接内存与堆内存

NIO的Buffer提供了一个可以不经过JVM内存直接访问系统物理内存的类——DirectBuffer。 DirectBuffer类继承自ByteBuffer，但和普通的ByteBuffer不同，普通的ByteBuffer仍在JVM堆上分配内存，其最大内存受到最大堆内存的限制；而DirectBuffer直接分配在物理内存中，并不占用堆空间，其可申请的最大内存受操作系统限制。

直接内存的读写操作比普通Buffer快，但它的创建、销毁比普通Buffer慢。

因此直接内存使用于需要大内存空间且频繁访问的场合，不适用于频繁申请释放内存的场合。

（Note：DirectBuffer并没有真正向OS申请分配内存，其最终还是通过调用Unsafe的allocateMemory()来进行内存分配。不过JVM对Direct Memory可申请的大小也有限制，可用-XX:MaxDirectMemorySize=1M设置，这部分内存不受JVM垃圾回收管理。）

[Java直接内存与堆内存](https://www.cnblogs.com/z-sm/p/6235157.html)
