# IO NIO AIO

## 1. IO

### "\\" 和 “/” 选哪个

``` java
String path="D:\\新建文件夹\\2.png";

File file=new File(path);

System.out.println(file.exists());

String path1="D:/新建文件夹/2.png";

File file1=new File(path);

System.out.println(file1.getAbsolutePath());

System.out.println(file1.getCanonicalPath());

输出：
false
D:\新建文件夹\2.png
D:\新建文件夹\2.png
```

具体使用中都可以达到访问路径的效果，只不过有一点小区别  
正斜杠的话，一般在配置文件路径时，指向下一个路径只要使用一个  
例如："c:/a/1. txt";  
而反斜杠的话，在配置文件路径时，由于它本身在java中有特殊意义，作为转义符而存在，所以具体意义上的反斜杠要两个  
例如："c\\a\\1. txt"; 这里的第一个反斜杠是作为转义符存在的，第二个才是真正意义上的反斜杠  
一般可以认为是"/"的作用等同于"\\"  
在java中路径一般用"/"  
windows中的路径一般用"\"  
linux、unix中的路径一般用"/"  
最好用“/”  因为java是跨平台的。“\”（在java代码里应该是\\）是windows环境下的路径分隔符，Linux和Unix下都是用“/”。而在windows下也能识别“/”。所以最好用“/”  

### 在运行程序根目录下创建文件

``` java
String destFileDir = "downloads";

// 储存下载文件的目录，当url中只包含downloads时，会在项目的根目录下创建downloads文件夹
File dir = new File(destFileDir);
if (!dir.exists()) {
    dir.mkdirs();
}
```









