---
title: Spring Boot SpringMVC常用的设置上下文方式
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-25 18:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot 
description: 在学习Spring Boot中，SpringMVC常用的设置上下文方式如下：1.ModelAndView ,2.Model , 3.HttpServletRequest, 4.WebRequest
photos: https://yremp.live/wp-content/uploads/2019/07/cropped-70149312_p0-1.png
---
<!-- wp:paragraph -->
<p>在学习Spring Boot中，SpringMVC常用的设置上下文方式如下：</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p> 首先看一下前端booklist.html： </p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>                    &lt;thead>
                    &lt;tr>
                        &lt;th>ID&lt;/th>
                        &lt;th>书名&lt;/th>
                        &lt;th>作者&lt;/th>
                        &lt;th>价格&lt;/th>
                        &lt;th>操作&lt;/th>
                    &lt;/tr>
                    &lt;/thead>
                    &lt;tbody>
                    &lt;tr th:each="book : ${books}">
                        &lt;td th:text="${book.id}">&lt;/td>
                        &lt;td th:text="${book.name}">&lt;/td>
                        &lt;td th:text="${book.author}">&lt;/td>
                        &lt;td th:text="${book.price}">&lt;/td>
                    &lt;/tr>
                    &lt;/tbody></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>1.ModelAndView</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>使用方法如下：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>@RequestMapping("/book")
    public ModelAndView queryAll(){
        List&lt;Book> books =bookDao.selectAll();
        ModelAndView modelAndView =new ModelAndView("booklist");
        modelAndView.addObject("books",books);
        return  modelAndView;
    }</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph {"textColor":"vivid-red"} -->
<p class="has-text-color has-vivid-red-color"> 1、高内聚低耦合原则。实质上上设计的函数尽量不带参数，便于不同系统间调用时更简单。 推荐使用ModelAndView， ModelAndView实质上是map，和web容器没有关系。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>2.Model</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>使用方法如下：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>@RequestMapping("/book")
public String queryAll(Model model){
     List&lt;Book> books =bookDao.selectAll();
     model.addAttribute("books" ,books);
     return "booklist";
 }</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>SpringMVC会自动创建Model对象，但是在一些特殊情况下需要手动创建对象。</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":3} -->
<h3>3.HttpServletRequest</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>使用方法如下：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code> @RequestMapping("/book")
    public String queryAll(HttpServletRequest request){
        List&lt;Book> books =bookDao.selectAll();
       request.setAttribute("books",books);
        return  "booklist";
    }</code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>4.WebRequest</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>使用方法如下：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>     @RequestMapping("/book")
    public String queryAll(WebRequest webRequest){
        List&lt;Book> books =bookDao.selectAll();
       webRequest.setAttribute("books",books,WebRequest.SCOPE_REQUEST);
        return  "booklist";
    }</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph {"ampFitText":true} -->
<p><amp-fit-text layout="fixed-height" min-font-size="6" max-font-size="72" height="80">WebRequest和HttpServletRequest这两种方法 和WEB容器强耦合, 不利于 更换容器或者扩展。不建议这两种方式 </amp-fit-text></p>
<!-- /wp:paragraph -->