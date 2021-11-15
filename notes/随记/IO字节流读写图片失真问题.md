### IO字节流读写图片失真问题

![image-20210602071938593](https://gitee.com/panqiyi/pqimg/raw/master/20210602071938.png)

如上图，图片读取不完整，下方均发黑或者发绿。

**原因：**仔细观察代码后，发现没有关闭资源。添加关闭流后读取图片完整。

```java
//将上传到服务器的图片写入本地项目中
String localFile = "D:\\PRoject\\maven_web\\src\\main\\webapp\\image\\" + newFileName;
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(localFile));
BufferedInputStream bis = new BufferedInputStream(new FileInputStream(image));
byte[] bys = new byte[1024*4];
int len;
while ((len = bis.read(bys))!=-1) {
    bos.write(bys, 0, len);
}
//关闭流
bos.close();
bis.close();
```

![image-20210602072228822](https://gitee.com/panqiyi/pqimg/raw/master/20210602072228.png)