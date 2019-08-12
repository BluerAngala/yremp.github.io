---
title: Spring Boot 文件上传
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-26 18:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot 
description: 在Spring Boot 项目中如何上传文件，今天在这里分享一下。
photos: https://yremp.live/wp-content/uploads/2019/07/cropped-66764420_p0.png
---
<!-- wp:paragraph -->
<p>在Spring Boot 项目中如何上传文件，今天在这里分享一下。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>Step 1：前端准备：</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>fileupload.html,一个简单的表单：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
    &lt;meta charset="UTF-8">
    &lt;title>Title&lt;/title>
&lt;/head>
&lt;body>
&lt;form action="/upload" method="post"  enctype="multipart/form-data">
    &lt;input type="file" id="photo" name="photo">
    &lt;input type="submit">
&lt;/form>
&lt;/body>
&lt;/html></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Step2：application.properties配置</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>application.properties配置文件中如下配置：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#临时目录文件夹
spring.servlet.multipart.location=f:/temp/

#自定义文件保存目录
app.upload.path=f:upload/

#单个文件上传最大大小
spring.servlet.multipart.max-file-size=10MB

#单个请求最大上传大小
spring.servlet.multipart.max-request-size=50MB</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Step 3：后台Controller：</h3>
<!-- /wp:heading -->

<!-- wp:code -->
```java
@Controller
public class FileUploadController {

//   返回文件上传界面
    @RequestMapping("/")
    public String index(){
        return "fileupload";
    }

//    使用配置文件中自定义文件保存路径
@Value("${app.upload.path}")
    private String path=null;
    @PostMapping("/upload")

//    MultipartFile是上传文件接口，对应保存临时文件
//    参数名要和前端name属性保持一致
    public ModelAndView upload(@RequestParam("photo") MultipartFile photo) throws IOException {

//        文件保存的路径
//        String path="f:/upload/";

//        文件使用原有名称命名
//        String filename=photo.getOriginalFilename();

//        文件使用上传的时间命名
        String filename=new SimpleDateFormat("yyyyMMddHHmmssSSS").format(new Date());

//        文件扩展名
        String suffix=  photo.getOriginalFilename().substring(photo.getOriginalFilename().lastIndexOf("."));

//        限制上传的文件类型
        if(!suffix.equals(".jpg")){
            throw  new RuntimeException("图片格式错误");
        }

//        Spring 提供了一个文件操作类FileCopyUtils
        FileCopyUtils.copy(photo.getInputStream(),new FileOutputStream(path+filename+suffix));
        return null;
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->