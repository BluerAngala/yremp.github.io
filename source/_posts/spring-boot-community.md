---
title: Spring Boot 社区项目
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-8-6 18:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot
description: 使用Spring Boot 开发的交流社区项目，项目特点是接入了github登录，支持markdown语法编辑，回复评论通知等功能。
photos: https://yremp.live/wp-content/uploads/2019/08/透明的雨伞-插画少女背景4k动漫壁纸_彼岸图网-min.jpg
---
<!-- wp:heading {"level":3} -->
### 1.图片预览：

#### 1.主页
![](http://yremp.hk.ufileos.com/38ae6d89-5de4-44c3-8ee9-703c962432cd.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=q2oyg%2BotvDmb6IjT3NR%2F72XuH68%3D&Expires=1880288397)
#### 2.帖子详情
![](http://yremp.hk.ufileos.com/bdf1cbab-1be6-4dfc-af2f-ff57064b0199.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=azCuVUGOxEUj3%2FZ4sEAZcfr1hg0%3D&Expires=1880288722)
#### 3.回复和评论
![](http://yremp.hk.ufileos.com/75665e02-252f-4295-82da-a174d5430fc3.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=G2FIXPULPGAef0EzgYTJTMkBzac%3D&Expires=1880288840)
#### 4.个人资料
![](http://yremp.hk.ufileos.com/9f34b6fc-6280-4f06-b532-811fddcf8af1.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=0McqMH40VePPvAzurjIBcDszH9U%3D&Expires=1880288973)
![](http://yremp.hk.ufileos.com/1887c95d-f645-46df-97b2-53166a3a6cf4.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=AFayW12hx1W7kjiY09EIv3fOa6M%3D&Expires=1880288990)
![](http://yremp.hk.ufileos.com/1dbff5ae-f910-4234-b3c9-01ec481b1522.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=WemP%2FVVBLhBJkkKjlDlTT4E3t5s%3D&Expires=1880289014)
![](http://yremp.hk.ufileos.com/2bb452c7-ee07-4b69-aad7-8fbb28994e07.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=LOcBj1T8uT%2FXdFMWQC2MzAmGFU8%3D&Expires=1880289025)

#### 公共资料面板
![](http://yremp.hk.ufileos.com/6198ce14-398e-4e63-bfc8-5606806fc1f1.png?UCloudPublicKey=TOKEN_c8840aa4-b6d1-4b64-b8d0-4f759247250b&Signature=9oZv9wbnJ6mDiIhBk1AY06v0DHs%3D&Expires=1880289942)

#### 个人资料的前端页面还有很大修改的空间
<h3>2.项目地址：</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>话不多说，先给出项目地址。</p>
<!-- /wp:paragraph -->

<!-- wp:list {"ordered":true} -->
<ol><li><a href="https://github.com/yremp/community">Github 地址</a></li><li><a href="http://www.yremp.live:1234/">在线预览地址</a></li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>3.项目核心：</h3>
<!-- /wp:heading -->

<!-- wp:list {"ordered":true} -->
<ol><li>接入github，使用户可以直接使用github账号登录。</li><li>集成<a href="https://github.com/yremp/editormd">editormd</a>插件，实现markdown语法编辑并显示为html。</li><li>在editormd中使用ucloud上传图片。</li><li>数据库查询分页。</li><li>使用ajax提交请求，实现二级评论的加载。</li></ol>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>4.核心代码</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>1.Github登录相关</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>1.编写AccessTokenDTO.class 用于github access_token</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
    private String client_id;
    private String client_secret;
    private String code;
    private String redirect_uri;
    private String state;

    public String getClient_id() {
        return client_id;
    }

    public void setClient_id(String client_id) {
        this.client_id = client_id;
    }

    public String getClient_secret() {
        return client_secret;
    }

    public void setClient_secret(String client_secret) {
        this.client_secret = client_secret;
    }

    public String getCode() {
        return code;
    }

    public void setCode(String code) {
        this.code = code;
    }

    public String getRedirect_uri() {
        return redirect_uri;
    }

    public void setRedirect_uri(String redirect_uri) {
        this.redirect_uri = redirect_uri;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>2.编写GithubProvider.class:调用github官方给出的 OAuth Apps api，实现Github登录 </p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Component
public class GithubProvider {
    public String getAccessToken(AccessTokenDTO accessTokenDto){
        MediaType mediaType
                = MediaType.get("application/json; charset=utf-8");
        OkHttpClient client = new OkHttpClient();
            RequestBody body = RequestBody.create(mediaType,JSON.toJSONString(accessTokenDto));
            Request request = new Request.Builder()
                    .url("https://github.com/login/oauth/access_token")
                    .post(body)
                    .build();
            try (Response response = client.newCall(request).execute()) {
               String string =response.body().string();
               String access_token=string.split("&amp;")[0].split("=")[1];
                return access_token;
            }catch (Exception e)
            {
                e.printStackTrace();
            }
        return null;
    }
    public GithubUserDTO getGithubUser(String accessToken) {

        OkHttpClient client = new OkHttpClient();
        Request request = new Request.Builder()
                .url("https://api.github.com/user?access_token=" + accessToken)
                .build();
        try {
            Response response = client.newCall(request).execute();
            String string = response.body().string();
            GithubUserDTO githubUserDTO = JSON.parseObject(string, GithubUserDTO.class);
            return githubUserDTO;
        } catch (IOException e) {
            return null;
        }
    }
      }
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>Controller中调用GithubProvider获取用户数据并写入数据库</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Controller
public class AuthorizeController {
    @Autowired
    private GithubProvider githubProvider = null;
    @Autowired
    private UserService userService = null;
    @Value("${github.client.id}")
    private String clientID;
    @Value("${github.client.secret}")
    private String clientSC;
    @Value("${github.redirect.url}")
    private String redirectURL;
    @Autowired
    QuesDtoService quesDtoService;
    @RequestMapping("/callback")
    public String callback(@RequestParam(name = "code") String code,
                           @RequestParam(name = "state") String state,
                           HttpServletResponse response,
                           HttpServletRequest request) {
        AccessTokenDTO accessTokenDto = new AccessTokenDTO();
        accessTokenDto.setCode(code);
        accessTokenDto.setState(state);
        accessTokenDto.setClient_id(clientID);
        accessTokenDto.setClient_secret(clientSC);
        accessTokenDto.setRedirect_uri(redirectURL);
        String accesstaken = githubProvider.getAccessToken(accessTokenDto);
        GithubUserDTO githubUserDTO = githubProvider.getGithubUser(accesstaken);
        if (githubUserDTO != null) {
            User user1 = null;
            String token = UUID.randomUUID().toString();
            try {
                user1 = userService.findByGithubId(String.valueOf(githubUserDTO.getId()));
                if (user1 != null) {
                    response.addCookie(new Cookie("token", token));
                    user1.setUser_token(token);
                    userService.upTokenById(token, user1.getUser_id());
                } else {
                    User user = new User();
                    user.setUser_token(token);
                    user.setUser_name(githubUserDTO.getName());
                    user.setAccount_id(String.valueOf(githubUserDTO.getId()));
                    user.setGmt_create(System.currentTimeMillis());
                    user.setGmt_modified(user.getGmt_create());
                    user.setUser_img(githubUserDTO.getAvatarUrl());
                    user.setUser_bio(githubUserDTO.getBio());
                    user.setUser_blog(githubUserDTO.getBlog());
                    user.setUser_github(githubUserDTO.getHtml_url());
                    userService.Insert(user);
                    request.getSession().setAttribute("user", user);
                    response.addCookie(new Cookie("token", token));
                }
            } catch (Exception w) {

            }
            return "redirect:/";
        } else {

            return "redirect:/";
        }
    }
```
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>2.Ucloud  <strong>对象存储 UFile</strong> </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p> 1.UcloudProvider.class:</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
//ucloud上传文件
@Service
public class UcloudProvider {
    private String buckname = "yremp";
    @Value("${ucloud.publickey}")
    private String publickey;
    @Value("${ucloud.privatekey}")
    private String privatekey;
    public String upload(InputStream fileStream, String mimeType, String filename) {
        String fileName;
        String[] FilleName = filename.split("\\.");
        if (FilleName.length > 1) {
            fileName = UUID.randomUUID().toString() + "." + FilleName[FilleName.length - 1];

        } else {
            return null;
        }
        try {
            //    授权
            ObjectAuthorization OBJECT_AUTHORIZER = new UfileObjectLocalAuthorization(publickey, privatekey);
            //    配置
            ObjectConfig config = new ObjectConfig("hk", "ufileos.com");
            PutObjectResultBean response = UfileClient.object(OBJECT_AUTHORIZER, config)
                    .putObject(fileStream, mimeType)
                    .nameAs(fileName)
                    .toBucket(buckname)
                    .setOnProgressListener(new OnProgressListener() {
                        @Override
                        public void onProgress(long bytesWritten, long contentLength) {

                        }
                    })

                    .execute();
            if (response != null &amp;&amp; response.getRetCode() == 0) {
                String url = UfileClient.object(OBJECT_AUTHORIZER, config)
                        .getDownloadUrlFromPrivateBucket(fileName, buckname, 24 * 60 * 60 * 365 *10)
                        .createUrl();
                return url;
            } else {
                throw new PeculiarException(PeculiarExceptionCodeAndMessage.FILE_UPLOAD_ERROR);
            }
        } catch (UfileClientException e) {
            throw new PeculiarException(PeculiarExceptionCodeAndMessage.FILE_UPLOAD_ERROR);
        } catch (UfileServerException e) {
            throw new PeculiarException(PeculiarExceptionCodeAndMessage.FILE_UPLOAD_ERROR);
        }
    }

}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>2.前端请求后调用UcloudProvider</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Controller
public class FileUploadController {
    private String fileurl;
    @Autowired
    private UcloudProvider ucloudProvider;
    @RequestMapping("/file/upload")
    @ResponseBody
    public FileDTO upload(HttpServletRequest request){
        MultipartHttpServletRequest multipartHttpServletRequest=(MultipartHttpServletRequest) request;
        MultipartFile file = multipartHttpServletRequest.getFile("editormd-image-file");
        try {
          //ucloudProvider 拿到文件url
          String fileurl=  ucloudProvider.upload(file.getInputStream(),file.getContentType(),file.getOriginalFilename());
            FileDTO fileDTO = new FileDTO();
            fileDTO.setSuccess(1);
            fileDTO.setMessage("成功");
            fileDTO.setUrl(fileurl);
            return fileDTO;
        } catch (Exception e) {
            e.printStackTrace();
        }
        FileDTO fileDTO = new FileDTO();
        fileDTO.setSuccess(1);
        fileDTO.setMessage("成功");
        fileDTO.setUrl(fileurl);
        return fileDTO;
    }
}
```
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>3.其他</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>至于集成editormd、数据库分页、和ajax 的简单使用感觉比较简单，教程也很多就不细说。</p>
<!-- /wp:paragraph -->