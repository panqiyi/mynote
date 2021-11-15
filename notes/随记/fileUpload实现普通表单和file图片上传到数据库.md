## fileUpload实现普通表单和file图片上传到数据库

首先需要去apache 官网 下载commons-fileupload和 commons-io 下载这两个jar包

下载步骤：fileUpload的commons-fileupload和 commons-io 下载

### 效果图：

表单提交：

<img src="https://gitee.com/panqiyi/pqimg/raw/master/20210516114645.png" alt="image-20210516114645464" style="zoom:67%;" />

数据库：

![image-20210516115011292](https://gitee.com/panqiyi/pqimg/raw/master/20210516115011.png)

### 实现

#### jsp:页面

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
    <link rel="stylesheet" href="publish.css">
    <script src="js/jquery-3.2.1.min.js"></script>
    <script>
            $(function () { //加载页面完成后
                $("#file_upload").change(function () { // 选择图片后即时在页面显示
                    var $file = $(this);
                    var fileObj = $file[0];
                    var windowURL = window.URL || window.webkitURL;
                    var dataURL;
                    var $img = $("#img_show");

                    if (fileObj && fileObj.files && fileObj.files[0]) {
                        dataURL = windowURL.createObjectURL(fileObj.files[0]);
                        $img.attr('src', dataURL);
                    } else {
                        dataURL = $file.val();
                        var imgObj = document.getElementById("img_show");

                        imgObj.style.filter = "progid:DXImageTransform.Microsoft.AlphaImageLoader(sizingMethod=scale)";
                        imgObj.filters.item("DXImageTransform.Microsoft.AlphaImageLoader").src = dataURL;

                    }
                });
            });

            function open_file() { //点击 + 字体图标，触发文件点击事件
                document.getElementById("file_upload").click();
            }

    </script>
</head>
<body class="body_img">
<img src="img/logom2.png" class="img_logo_pub">
<div class="pb_box">
    <div class="pb_box_z">
        <form action="${pageContext.request.contextPath}/publishServlet" method="post" autocomplete="off" enctype="multipart/form-data">

            <table <%--border="1"--%> class="table_pb">
                <tr>
                    <td class="two_right"><label for="product_name">商品名称：</label></td>
                    <td>
                        <input type="text" name="name" id="product_name" class="name">
                        <%--隐藏的uid表单，上传发布用户的id--%>
                        <input type="text" name="uid" value="2" style="display:none">
                    </td>
                </tr>

                <tr>
                    <td class="two_right"><label for=""></label>
                        成色：</td>
                    <td> <select class="select grade" name="level">
                        <option value="5成新">5成新</option>
                        <option value="6成新">6成新</option>
                        <option value="7成新">7成新</option>
                        <option selected value="8成新">8成新</option>
                        <option value="9成新">9成新</option>
                        <option value="全新">全新</option>
                    </select></td>
                </tr>

                <tr>
                    <td class="two_right"><label for=""></label>
                        单价：</td>
                    <td> <input type="text" name="pricenow" id="" class="price price_now">￥</td>

                </tr>

                <tr>
                    <td class="two_right"><label for="">  原价：</label></td>
                    <td><input type="text" name="priceold" id="" class="price price_old">￥</td>
                </tr>

                <tr>
                    <td class="two_right"><label for=""></label>
                        数量：</td>
                    <td> <input type="text" name="count" id="" class="sum"></td>
                </tr>

                <tr>
                    <td class="text_td two_right"><label for=""></label>
                        商品详情：</td>
                    <td> <textarea class="textarea" name="remark"></textarea></td>
                </tr>

                <tr>
                    <td class="two_right">
                        分类：</td>
                    <td> <select class="select " name="sort">
                        <option value="数码">数码</option>
                        <option value="图书影音">图书影音</option>
                        <option value="内衣">内衣</option>
                        <option selected value="户外运动">户外运动</option>
                        <option value="茶酒">茶酒</option>
                        <option value="美食">美食</option>
                    </select></td>
                </tr>

                <tr>
                    <td class="img_td two_right"><label for=""></label>
                        图片：</td>
                    <td>
                        <%--隐藏文件表单--%>
                        <input type="file" name="file_img" id="file_upload" style="display:none">
                        <a href="#" onclick="open_file();" class="font_a"><span class="iconfont font_img">&#xe6da;</span></a>

                        <%--用于图片回显--%>
                    <img src="${pageContext.request.contextPath}/${imgUrl}" id="img_show"  height="180px">
                        <div> <input type="submit" name="submit" class="submit_pb" value="提交"></div>
                    </td>

                </tr>

            </table>
        </form>
    </div>
</div>
</body>
</html>
```

#### servelt:控制器

```java
package cn.pqy.web.servlet;

import cn.pqy.domain.CommodityBean;
import cn.pqy.service.CommodityService;
import cn.pqy.service.impl.CommodityServiceImpl;
import org.apache.commons.fileupload.FileItem;
import org.apache.commons.fileupload.FileUploadException;
import org.apache.commons.fileupload.disk.DiskFileItemFactory;
import org.apache.commons.fileupload.servlet.ServletFileUpload;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.File;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.util.Date;
import java.util.List;

/**
 * @author panqiyi
 * @date 2021/5/15 - 21:33
 */
@WebServlet("/publishServlet")
public class PublishServlet extends HttpServlet {
    CommodityBean commodityBean=new CommodityBean();
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Object file_img = request.getParameter("file_img");
        String imgUrl = null;  //存储到数据库的图像路径
        String imgFileName="image";  //web中存储图片的文件夹

        //判断上传表单是否为multipart/form-data类型
        if (ServletFileUpload.isMultipartContent(request)){
            //1、创建DiskFileItemFactory对象，作用是 设置缓存大小以及临时文件保存位置.
            DiskFileItemFactory factory = new DiskFileItemFactory();
            //2、创建一个上传工具，指定使用缓存区与临时文件存储位置. 并设置上传文件大小限制
            ServletFileUpload sfu = new ServletFileUpload(factory);
            sfu.setSizeMax(10*1024*1024); // 1024byte=1kb 1024kb=1M; 设置不能超过10M
            //3、解决上传文件中文名称乱码
            sfu.setHeaderEncoding("utf-8");
            //4、ServletFileUpload.parseRequest()方法解析request对象，
            // 得到所有上传项对象的list.每一个FileItem就相当于一个上传项
            try {
                List<FileItem> fileItems = sfu.parseRequest(request);
                //遍历list，每迭代一个FileItem对象，调用isFormFile方法判断是否是上传文件
                for (FileItem fileItem : fileItems) {
                    System.out.println(fileItem);
                    if (fileItem.isFormField()){
                        //普通表单，则调用方法
                        processFromField(fileItem);

                    }else {
                        //file类型表单
                        String fileName = fileItem.getName();  //上传文件名称
                        System.out.println("原文件名："+fileName);
                        String suffix = fileName.substring(fileName.lastIndexOf('.')); //获取文件后缀名
                        System.out.println("后缀名："+suffix); // .jpg
                        //新文件名，唯一（时间戳）
                        String newFileName = new Date().getTime() + suffix;
                        System.out.println("新文件名："+newFileName);

                        //写入文件到web服务器：
                        //文件存储位置
                        ServletContext context = this.getServletContext();
                        // 获取绝对路径目录(D:\PRoject\JavaWeb\out\artifacts……)
                        String serverPath = context.getRealPath("")+imgFileName;
                        System.out.println(serverPath);
                        // 如果文件夹不存在则创建
                        File headFile = new File(serverPath);
                        if (!headFile.exists()) {
                            headFile.mkdirs();
                        }
                        //将图片存储到文件夹（serverPath：目录 ；newFileName：文件名）
                        File image = new File(serverPath, newFileName);
                        //将上传文件写到服务器上指定文件夹
                        fileItem.write(image);
                        //调用FileItem的delete()方法，删除临时文件
                        fileItem.delete();

                        //将图片路径（imgUrl）存储到数据库
                        // 拼接相对相对路径
                        imgUrl=imgFileName+"/"+newFileName;
                        System.out.println(imgUrl);
                        //存储图片路径到bean对象
                        commodityBean.setImage(imgUrl);
                    }
                }
                System.out.println(commodityBean);

                //调用service存储表单数据到数据库
                CommodityService service=new CommodityServiceImpl();
                int n = service.addCommodity(commodityBean);
                if (n>0){
                    //存储成功
                    //存储图片地址到request，用于页面回显
                    request.setAttribute("imgUrl",imgUrl);
                    request.getRequestDispatcher("/publish.jsp").forward(request,response);
                }

            } catch (FileUploadException e) {
                e.printStackTrace();
            } catch (Exception e) {
                e.printStackTrace();
            }

        }

    }
    //普通表单，给bean对象设置值 的方法
    private void processFromField(FileItem fileItem) throws UnsupportedEncodingException {
        String fieldName = fileItem.getFieldName();                  //字段名 name
        String fieldValue = fileItem.getString("UTF-8");    //字段值 value
        if ("name".equals(fieldName)) {
            commodityBean.setNaem(fieldValue);
        }
        if ("level".equals(fieldName)) {
            commodityBean.setLevel(fieldValue);
        }
        if ("pricenow".equals(fieldName)) {
            commodityBean.setPricenow(Double.parseDouble(fieldValue));
        }
        if ("priceold".equals(fieldName)){
            commodityBean.setPriceold(Double.parseDouble(fieldValue));
        }
        if ("count".equals(fieldName)){
            commodityBean.setCount(Integer.parseInt(fieldValue));
        }
        if ("remark".equals(fieldName)){
            commodityBean.setRemark(fieldValue);
        }
        if ("sort".equals(fieldName)){
            commodityBean.setSort(fieldValue);
        }
        if ("uid".equals(fieldName)){
            commodityBean.setUid(Integer.parseInt(fieldValue));
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doPost(request, response);
    }
}
```

#### service:逻辑操作

接口：

```java
public interface CommodityService {
    /**
     * 商品发布信息
     * @param comm
     * @return
     */
    int addCommodity(CommodityBean comm);
}
```

实现类：

```java
public class CommodityServiceImpl implements CommodityService {
    CommodityDao dao=new CommodityDaoImpl();
    @Override
    public int addCommodity(CommodityBean comm) {
        int n = dao.addCommodity(comm);
        return n;
    }
}
```

#### dao:数据库操作

接口：

```java
public interface CommodityDao {
    /**
     * 商品发布信息
     * @param comm
     * @return
     */
    int addCommodity(CommodityBean comm);
}
```

实现类：

```java
public class CommodityDaoImpl implements CommodityDao {
    private JdbcTemplate template=new JdbcTemplate(JDBCUtils.getDataSource());
    @Override
    public int addCommodity(CommodityBean comm) { //添加数据到商品表
        String sql="insert into commodity values(null,?,?,?,?,?,?,?,?,?)";
        int n = template.update(sql, comm.getNaem(),
                comm.getLevel(),
                comm.getRemark(),
                comm.getPricenow(),
                comm.getPriceold(),
                comm.getCount(),
                comm.getSort(),
                comm.getUid(),
                comm.getImage());
        return n;
    }
}
```

#### domain：javaBean类

```java
public class CommodityBean {
    private int id;  //主键
    private String naem; //商品名称
    private String level; //成色
    private String remark;  // 详情
    private double pricenow;  //价格
    private double priceold;  //原价格
    private int count;  // 数量
    private String sort;  //类别
    private int uid;  //发布的用户id
    private String image;  //商品图片地址
    	//省略get/set和toString
    }
```



