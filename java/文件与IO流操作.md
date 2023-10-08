## 文件 File

#### 构造函数

```java
public File(String pathname)
public File(String parent, String child)
public File(File parents, String chile)

//  只有一个参数时，默认是文件的完整路径
//  有两个参数时，会将两个路径拼接起来（父路径，子路径）
File file = new File("D:\\aaa.txt");
```



#### 常见成员方法

```java
file.exists();  //  判断路径是否存在
file.isDirectory();  //  判断是否为文件夹
file.isFile();  //  判断是否为文件
file.length();  //  返回文件的大小（字节数量）
file.getAbsolutePath();  //  返回文件的绝对路径
file.getPath();  //  返回定义文件时使用的路径
file.getName();  //  获取文件名，带后缀
file.lastModified();  //  获取最后修改时间（时间毫秒值）

file.createNewFile();  //  创建文件file，创建成功返回true
file.mkdirs();  //  创建一个或多级文件夹，创建成功返回true
file.delete();  //  删除文件或空文件夹
    
File[] files = file.listFiles();  //  获取文件夹中的所有文件
```





### IO流

- 字节流
  - 能打开所有文件
- 字符流
  - 只能打开“记事本”能打开的且能读懂的文件，如txt、md文件



#### 字节流

##### 字节输入流

```java
//  创建文件输入流，file可以是File文件，也可以是String字符串
//  文件不存在则报错
//  字节流底层没有缓冲区
FileInputStream fis = new FileInputStream(file);

fis.close();
```



数据读取方法

```java
//  空参一次只读取一个字符，返回这个字符的ASCII码值
int b = fis.read();  

//  可以传递一个byte数组，一次读取这个byte数组大小的数据，返回本次读取的长度
byte[] bytes = new byte[1024 * 1024]  //  1M
int n = fis.read(bytes);

//  读取到文件末尾时返回-1

/*  ---------------------------  */

//  read()读取字符后，会自动将指针向后移动一位
//  读取一个文件中所有的字符，并打印在控制台上：
FileInputStream fis = new FileInputStream(file);
int b;
while((b = fis.read()) != -1){
    System.out.print(b);
}
fis.close();
```







##### 字节输出流

创建对象

```java
//  创建文件输入流，file可以是File文件，也可以是String字符串
//  如果文件不存在，会创建一个新的文件（需要保证父级路径存在）
//  如果文件存在，会先清空文件
FileOutputStream fos = new FileOutputStream(file);

//  如果不希望文件倍清空，需要添加第二个参数true
FileOutputStream fos = new FileOutputStream(file, true);

fos.close();
```



数据输出方法

```java
fos.write(int b);  //  一次写一个字节的数据
fos.write(byte[] b);  //  一次写一个字节数组的数据
fos.write(byte[] b, int off, int len);  //  一次写一个字节数组的数据的一部分，指定起始位置和长度
```





#### 字符流

##### 字符输入流

```java
//  创建字符输入流，file可以是File文件，也可以是String字符串
//  文件不存在则报错
FileReader fr = new FileReader(file);

//  FileReader可以指定字符编码读取：
FileReader fr = new FileReader(file, Charset.forName("UTF-8"));

//  字符输入流中自带一个8192字节的缓冲区，每次读取8192个字符，之后从缓冲区中读取

fr.close();
```



字符读取方法

```java
//  空参一次只读取一个字符，解码并转成十进制数字
int b = fr.read();  

//  可以传递一个byte数组，一次读取这个byte数组大小的数据，返回本次读取的长度
//  读取到文件末尾时返回-1
byte[] bytes = new byte[1024 * 1024]  //  1M
int n = fr.read(bytes);

/*  ---------------------------  */

//  read()读取字符后，会自动将指针向后移动一位
//  读取一个文件中所有的字符，并打印在控制台上：
FileReader fr = new FileReader(file);
int ch;
while((ch = fr.read()) != -1){
    System.out.print(ch);
}

fis.close();
```



##### 字符输出流

```java
//  file可以是File文件，也可以是String
//  如果文件不存在，会创建一个新的文件（需要保证父级路径存在）
//  如果文件存在，会先清空文件
//  如果不希望文件倍清空，需要添加第二个参数true
FileWriter fw = new FileWriter(file);

//  也可以指定输出的字符编码格式，续写参数调整为第三个位置
FileWriter fw = new FileWriter(file, Charset.forName("UTF-8"), true);


//  字符输出流中自带一个8192字节的缓冲区，写出数据时会先写出到缓冲区。
//  如果想将缓冲区中的数据立即输出到文件中，且不关闭连接，需要使用:
fw.flush();

fw.close();
```



字符输出方法

```java
fw.write()
```





#### 缓冲流

​	对字节流进行进一步包装，在字节流的基础上新增了一个长度为8192字节的缓冲区，以提高性能。

```java
//  构造函数
public BufferedInputStream(InputStream is, int size)
public BufferedOutputStream(OutputStream os, int size)
    
//  size省略时默认创建长度为8192字节的缓冲区，也可以自行指定缓冲区大小
//  关流时只需要关缓冲流，不需要关基本流
```



​	对字符流也进行了包装，新增了几个方法

```java
//  构造函数
public BufferedReader(Reader r, int size)
public BufferedWriter(Writer w, int size)
    
//  size省略时默认创建长度为8192字节的缓冲区，也可以自行指定缓冲区大小
//  关流时只需要关缓冲流，不需要关基本流
    
//  新增方法：
    //  输入流
    br.readLine()  //  一次读取一行，不包含最后的换行符
    
    //  输出流
    bw.newLine()  //  跨平台换行
```

```java
//  一次读取一行
FileReader fr = new FileReader(filename);
BufferedReader br = new BufferedReader(fr);
String line;
while((line = br.readLine()) != null){
    System.out.println(line);
}
br.close();
```







#### 转换流

| 将字节流 转换 为字符流     | InputStreamReader      |
| -------------------------- | ---------------------- |
| **将字符流 转换 为字节流** | **OutputStreamWriter** |

```mermaid
graph LR
数据源 --> 字节流1 --InputStreamReader--> 内存 --OutputStreamWriter--> 字节流2 --> 目的地
```

主要作用：**字节流使用字符流的方法**

- 使字节流使用字符流的方法

```java
//  创建字节流(input)
FileInputStream fis = new FileInputStream(filename);
//  将字节流转换为字符流，这里需要指定字符编码
InputStreamReader isr = new InputStreamReader(fis, "UTF-8");

//  转换流可以直接调用字符流的方法
int ch;
while((ch = isr.read()) != -1){
    System.out.print(ch);
}

isr.close();
fis.close();
```

- 利用转换流按照指定字符编码写出

```java
//  创建字节流(output)
FileOutputStream fos = new FileOutputStream(filename);
//  将字节流转换为字符流，这里需要指定字符编码
OutputStreamReader osw = new OutputStreamReader(fos, "UTF-8");

//  以指定字符编码写出
osw.write("中文汉字");

osw.close();
fos.close();
```



#### 序列化流、反序列化流

序列化流  将对象以序列化输出到文件

```java
//  需要被输出的对象的JavaBean类实现Serializable接口
public class Student implements Serializable {
    public String name;
    public int age;
}


Student stu = new Student();

//  
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(filename));
oos.writeObject(stu);
oos.close();
```



反序列化流  将序列化到本地文件的对象

```java
ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filename));
Object o = ois.readObject();
ois.close();
```



注意问题

```java
//  若将对象序列化到本地文件后，修改了JavaBean类，反序列化时会报错。
//  序列化时，会自动根据JavaBean内的成员变量计算出UID（long类型，相当于版本号）
//  若反序列化时得到的UID，与JavaBean的UID不同，则报错
//  解决方法，可以自定义版本号

private static final long serivalVersionUID = 1L;
```

```java
//  若不希望某个属性被序列化到本地文件，可以添加关键字transient

private transient String address;
```





#### 打印流

​		打印流不能操作数据源，只能操作目的地

字节打印流

```java
PrintStream ps = new PrintStream(new FileInputStream(filename));

//  打印97  自动换行
ps.println(97);
//  使用%s占位符  打印97 + 98 
ps.println(97 %s 98, "+")
```



字符打印流

```java
//  true: 自动刷新
PrintWriter pw = new PrintWriter(new FileInputStream(filename), true)
```





#### 压缩流、解压缩流

```java
//  压缩  压缩单个文件
File src = new File("test\\MyProject\\my file\\a.txt");
File dest = new File("test\\MyProject\\my file");

toZip(filename, dest);

public static void toZip(File src, File dest) throws IOException {
        //  创建压缩流，关联压缩包
        ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(new File(dest,src.getName + ".zip")));
        //  创建ZipEntry对象，表示压缩包里的每一个文件路径
    	//  可以在压缩包中创建文件夹
        ZipEntry entry = new ZipEntry(src.getName());
    	//  把ZipEntry对象放到压缩包中
        zos.putNextEntry(entry);
    	//  将数据写入到压缩包中
        FileInputStream fis = new FileInputStream(src);
        int b;
        while ((b = fis.read()) != -1){
            zos.write(b);
        }
        zos.closeEntry();
        zos.close();
}
```

```java
//  压缩  压缩文件夹
File src = new File("test\\MyProject\\my file\\a");
File dest = new File("test\\MyProject\\my file");

toZip2(src, dest);

public static void toZip2(File src, File dest) throws IOException {
    String name = src.getName();
    //  创建压缩流，文件夹下的所有文件将共用同一个压缩流
    //  所以需要提前创建压缩流，避免递归时出现错误
    ZipOutputStream zos = new ZipOutputStream(new FileOutputStream(new File(dest, name + ".zip")));
    //  name依次记录当前文件夹的父路径
    _toZip2(src, zos, name);
    zos.close();
}

public static void _toZip2(File src, ZipOutputStream zos, String name) throws IOException {
    File[] files = src.listFiles();
    for(File file : files){
        if(file.isDirectory()){
            _toZip2(file, zos, name + "\\" + file.getName());
        }else{
            ZipEntry entry = new ZipEntry(name + "\\" + file.getName());
            zos.putNextEntry(entry);
            FileInputStream fis = new FileInputStream(file);
            int b;
            while((b = fis.read()) != -1){
                zos.write(b);
            }
            fis.close();
            zos.closeEntry();
        }
    }
}

```

```java
//  解压缩
File src = new File("test\\MyProject\\my file\\a.zip");
File dest = new File("test\\MyProject\\my file");

unZip(src, dest);

public static void unZip(File src, File dest) throws IOException {
    //  创建解压缩流
    ZipInputStream zip = new ZipInputStream(new FileInputStream(src));

    //  表示当前在压缩包获取到的文件和文件夹
    ZipEntry entry;
    while ((entry = zip.getNextEntry()) != null) {
        if (entry.isDirectory()){
            File file = new File(dest, entry.toString());
            file.mkdirs();
        }else{
            FileOutputStream fos = new FileOutputStream(new File(dest, entry.toString()));
            int b;
            while ((b = zip.read()) != -1){
                fos.write(b);
            }
            fos.close();
            //  压缩包内的一个文件已处理完毕
            zip.closeEntry();
        }
    }
    zip.close();
}
```













