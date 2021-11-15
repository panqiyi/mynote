### docker创建tomcat容器，无法访问首页

进入tomcat容器

```
docker exec -it 容器名/id名 /bin/bash
```

查看tomcat根目录，进入webapps文件夹，发现里面没有内容，也没有默认文件，自然无法在浏览器页面进行访问，在根目录发现另外一个webapps.dist文件夹，进入后发现文件都在这里里面，遂删除原来空的webapps

```
rm -r webapps
```

重命名webapps.dist为webapps

```
mv webapps.dist webapps
```

(tomcat7版本没事，9版本就需要这样改了)