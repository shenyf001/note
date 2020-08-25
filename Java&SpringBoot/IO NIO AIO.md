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

### okhttp下载文件

``` java
    OkHttpClient okHttpClient = new OkHttpClient(); // 创建OkHttpClient对象
    /**
     * 下载文件
     *
     * @param url 文件地址
     * @return 文件
     */
    public File DownloadFile(String url) throws IOException {
        Request request = new Request.Builder().url(url).build(); // 创建一个请求
        Response response = okHttpClient.newCall(request).execute(); // 返回实体
        String destFileDir = "downloads";
        InputStream is = null;
        byte[] buf = new byte[2048];
        int len = 0;
        FileOutputStream fos = null;
        //储存下载文件的目录
        File dir = new File(destFileDir);
        if (!dir.exists()) {
            dir.mkdirs();
        }
        File file = new File(dir, getHeaderFileName(response));
        try {
            is = response.body().byteStream();
            fos = new FileOutputStream(file);
            while ((len = is.read(buf)) != -1) {
                fos.write(buf, 0, len);
            }
            fos.flush();
        } catch (Exception e) {
            log.error("文件下载失败", e);
        } finally {
            try {
                if (is != null) is.close();
                if (fos != null) fos.close();
            } catch (IOException e) {
                log.error("下载关闭失败", e);
            }
        }
        return file;
    }

    private String getHeaderFileName(Response response) throws UnsupportedEncodingException {
        String dispositionHeader = response.header("Content-Disposition");
        if (!TextUtils.isEmpty(dispositionHeader)) {
            dispositionHeader.replace("attachment;filename=", "");
            dispositionHeader.replace("filename*=utf-8", "");
            String[] strings = dispositionHeader.split("; ");
            if (strings.length > 1) {
                dispositionHeader = strings[1].replace("filename=", "");
                dispositionHeader = dispositionHeader.replace("\"", "");
                dispositionHeader = URLDecoder.decode(dispositionHeader, "utf-8");
                return dispositionHeader;
            }
            return "";
        }
        return "";
    }
```
