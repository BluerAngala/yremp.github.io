---
title: Spring Boot Thymeleaf模板引擎
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-24 18:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot 
description: 模板引擎将页面和数据进行分离，简化开发过程，主流模板引擎：Thymeleaf、 FreeMarker、Velocity、Groovy、Mustache 、JSP 、Beetl
Thymeleaf: 优点，主要集中在：模板即原型，前后端分离。缺点：模板必须符合xml规范，速度偏慢。适用于个人独立开发
photos: https://yremp.live/wp-content/uploads/2019/07/cropped-69447264_p14-1.png
---
<!-- wp:heading {"level":3} -->
<h3>1.模板 引擎简介 ：</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>模板引擎将页面和数据进行分离，简化开发过程，主流模板引擎：Thymeleaf、&nbsp;FreeMarker、Velocity、Groovy、Mustache 、JSP 、Beetl</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>Thymeleaf</strong>: <strong>优点</strong>，主要集中在：模板即原型，前后端分离。<strong>缺点</strong>：模板必须符合xml规范，速度偏慢。适用于个人独立开发</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>小结</strong>：工作中FreeMarker用的较多，前瞻学习Beetl。现在前端框架例如Bootstrap、Vue较为流行。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>2.Thymeleaf依赖引入</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>(1)在pom.xml 配置文件中添加以下代码引入thymeleaf:</h4>
<!-- /wp:heading -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;dependency>
            &lt;groupId>org.springframework.boot&lt;/groupId>
            &lt;artifactId>spring-boot-starter-thymeleaf&lt;/artifactId>
        &lt;/dependency></code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>(2)在html中引入thymeleaf命名空间，如下所示：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;html xmlns:th="http://www.thymeleaf.org" ></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>3.Thymeleaf 语法</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>1.常用语法简单介绍</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul><li>#{}  主要读取常量,例如读取配置文件中的 数据</li><li>${}  主要读取变量，程序中创建的，灵活改变的量</li><li>@{}  主要和路径有关系，比如在th:href="@{****}"中的使用</li></ul>
<!-- /wp:list -->

<!-- wp:paragraph -->
<p>2.更多语法详请参考<a href="https://www.thymeleaf.org/doc/tutorials/2.1/usingthymeleaf.html">官方文档</a></p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>4.Thymeleaf的使用：</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>1.前端</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;tr th:each="book : ${books}">
                        &lt;td th:text="${book.id}">&lt;/td>
                        &lt;td th:text="${book.name}">&lt;/td>
                        &lt;td th:text="${book.author}">&lt;/td>
                        &lt;td th:text="${book.price}">&lt;/td>
                        &lt;td>
                            &lt;a th:href="@{'/book/predit/'+${book.id}}" >&lt;button class="btn btn-sm btn-primary">编辑&lt;/button>&lt;/a>
                          &lt;a th:href="@{'/book/del/'+${book.id}}" >&lt;button class="btn btn-sm btn-danger" >删除&lt;/button>&lt;/a>
                        &lt;/td>
&lt;/tr></code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>2.后端</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>@Controller
public class bookController {
    @Autowired
    private BookDao bookDao;
    RendDao rendDao;
    @RequestMapping("/book")
   public String queryAll(Model model){
        List&lt;Book> books =bookDao.selectAll();
        model.addAttribute("books" ,books);
        return "booklist";
    }</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>booklist.html 在templates下，我只需在返回中输入"booklist" Thymeleaf会自动渲染出 booklist.html 。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->