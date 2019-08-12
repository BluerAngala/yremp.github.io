---
title: Spring Boot Mybatis的使用
author: yremp
avatar: https://cdn.jsdelivr.net/gh/yremp/cdn@2.1.4//img/custom/head.jpg
authorLink: ./
authorAbout: 
authorDesc: 
categories: 技术
date: 2019-7-28 19:16:01
comments: true
tags: 
 - web
 - Spring Boot
keywords: Spring Boot 
description: Spring Boot Mybatis的使用，有两种使用方式1.使用xml的方式，2.使用注解的方式。添加Mybatis对应的依赖
在application.properties添加配置信息
创建mybatis-config.xml文件
编写mybatis应用

photos: https://yremp.live/wp-content/uploads/2019/07/cropped-39473897_p0.jpg
---
<!-- wp:heading {"level":3} -->
<h3>Mybatis的两种使用方法：</h3>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>1.使用xml的方式</li><li>2.使用注解的方式</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":3} -->
<h3>一：XML方式的整合及增删改查</h3>
<!-- /wp:heading -->

<!-- wp:heading {"level":4} -->
<h4>主要步骤：</h4>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>添加Mybatis对应的依赖</li><li>在application.properties添加配置信息</li><li>创建mybatis-config.xml文件</li><li>编写mybatis应用</li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":4} -->
<h4>Step 1 :添加依赖</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>在pom.xml添加以下依赖：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;dependency>
  &lt;groupId>org.mybatis.spring.boot&lt;/groupId>
  &lt;artifactId>mybatis-spring-boot-starter&lt;/artifactId>
  &lt;version>2.1.0&lt;/version>
&lt;/dependency></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>Step 2:配置 application </h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>1.配置DataSource</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>#DataSource
spring.datasource.url=jdbc:mysql://localhost:3306/example?useUnicode=true&amp;characterEncoding=utf-8&amp;serverTimezone=UTC&amp;allowMultiQueries=true
spring.datasource.username=root
spring.datasource.password=123456
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>2.mybatis配置：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
#mybatis相关配置
#mybatis核心配置文件路径
mybatis.config-location=classpath:/mybatis/mybatis-config.xml
#mapper文件
mybatis.mapper-locations=classpath:/mybatis/mapper/*.xml
#json序列化
spring.jackson.serialization.indent-output=true
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>3.在resources目录下新建mybatis文件夹，在mybatis文件夹中创建mybatis-config.xml，并且按照以下格式编写：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;?xml version="1.0" encoding="UTF-8" ?>
&lt;!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

&lt;configuration>

&lt;/configuration></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":3} -->
<h3>Step3：实现增删改查</h3>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>在主包下创建mapper包，创建对应一个实体类(Emp)的接口，例如EmpMapper，在resources-&gt;mybatis-&gt;下创建mapper文件夹，并且创建Emp对应的xml文件empMapper.xml</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>empMapper.xml中：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```xml
 &lt;?xml version="1.0" encoding="UTF-8"?>
 &lt;!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
 &lt;!--映射文件配置 namespace指向接口-->
    &lt;mapper namespace="com.yremp.mybatis.mapper.EmpMapper">
 &lt;!--select:表示查询，id:对应接口中的方法名,parameterType:参数类型-->
    &lt;select id="findById" parameterType="Integer" resultType="com.yremp.mybatis.entity.Emp">
         select * from emp where empid=#{value }
    &lt;/select>

 &lt;!-- java.util.Map:将查询到的每一条记录包装成map，key：字段名 value：字段值-->
    &lt;select id="findDeps" parameterType="java.util.Map" resultType="java.util.LinkedHashMap">
         select * from emp e,dep d where e.depid=d.depid
         &lt;if test="dname!=null">
             and d.depname=#{dname}
         &lt;/if>
        &lt;if test="salary!=null">
            and e.salary>#{salary}
        &lt;/if>
    &lt;/select>
 &lt;!--新增一条数据-->
    &lt;insert id="create" parameterType="com.yremp.mybatis.entity.Emp">
        INSERT INTO `example`.`emp`( `name`, `age`, `salary`, `depid`)
        VALUES ( #{name}, #{age}, #{salary}, #{depid})
 --         将id回填 select Last_INSERT_ID() 获取最新插入的id
        &lt;selectKey keyProperty="empid" keyColumn="empid" resultType="Integer" order="AFTER">
          select Last_INSERT_ID()
        &lt;/selectKey>
    &lt;/insert>
 &lt;!--    更新一条数据-->
    &lt;update id="update" parameterType="com.yremp.mybatis.entity.Emp">
        UPDATE `example`.`emp` SET `name` = #{name}, `age` = #{age}, `salary` = #{salary}, `depid` = #{depid} WHERE `empid` = #{empid};
    &lt;/update>
 &lt;!--    删除一条数据-->
    &lt;delete id="delete" parameterType="Integer">
        delete from emp where empid=#{value}
    &lt;/delete>

 &lt;/mapper>
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>entity：Emp实体类：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
public class Emp {
    private Integer empid;
    private String name;
    private Double salary;
    private Integer depid;
    private Integer age;

    public Integer getEmpid() {
        return empid;
    }

    public void setEmpid(Integer empid) {
        this.empid = empid;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Double getSalary() {
        return salary;
    }

    public void setSalary(Double salary) {
        this.salary = salary;
    }

    public Integer getDepid() {
        return depid;
    }

    public void setDepid(Integer depid) {
        this.depid = depid;
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>mapper：EmpMapper</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
public interface EmpMapper {

    public Emp findById(Integer id);

    public List&lt;Map>findDeps(Map param);

    public void create(Emp emp);

    public void update(Emp emp);

    public void delete(Integer empid);
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>service：EmpService</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Service
public class EmpService {
    @Resource
    private EmpMapper empMapper;
    public Emp findById(Integer id){
        return empMapper.findById(id);
    }

    public List&lt;Map>findDeps(String dname,Double salary){
        Map param =new HashMap();
        param.put("dname",dname);
        param.put("salary",salary);
        return empMapper.findDeps(param);
    }
    @Transactional(rollbackFor = Exception.class)
    public void create(Emp emp){
        empMapper.create(emp);
    }

    @Transactional(rollbackFor = Exception.class)
    public void update(Emp emp){
        empMapper.update(emp);
    }

    @Transactional(rollbackFor = Exception.class)
    public void delete(Integer empid){
        empMapper.delete(empid);
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>controller:EmpController</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Controller
public class EmpController {
    @Resource
//    根据id查询员工
private EmpService empService;
    @RequestMapping("/emp/{id}")
    @ResponseBody
public Emp findByid(@PathVariable("id")Integer id){
    return empService.findById(id);
}
//根据条件查询符合条件的员工列表
    @RequestMapping("/emp/query")
    @ResponseBody
public List&lt;Map>findDeps( String dep, Double salary){
        return empService.findDeps(dep,salary);
}
//新建一条员工记录
    @RequestMapping("/emp/create")
    @ResponseBody
    public Emp create(){
        Emp emp=new Emp();
        emp.setName("yhy");
        emp.setAge(28);
        emp.setDepid(1);
        emp.setSalary(5000.00);
        empService.create(emp);
        return emp;
    }
//更新一条员工记录
    @RequestMapping("/emp/update")
    @ResponseBody
    public Emp update(){
        Emp emp=empService.findById(5);
        emp.setName("yhy");
        emp.setAge(28);
        emp.setDepid(1);
        emp.setSalary(6000.00);
        empService.update(emp);
        return emp;
    }
//删除一条员工记录
    @RequestMapping("/emp/delete")
    @ResponseBody
    public String update(Integer empid){
        empService.delete(empid);
        return "success";
    }
}
```
<!-- /wp:code -->

<!-- wp:heading -->
<h2>二：注解方式的整合和增删改查</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>因为之前写的<a href="https://yremp.live/spring-boot-day-03/">图书管理系统</a>全部使用注解方式，所以下面就使用之前的代码</p>
<!-- /wp:paragraph -->

<!-- wp:heading {"level":4} -->
<h4>主要步骤：</h4>
<!-- /wp:heading -->

<!-- wp:list -->
<ul><li>1.添加依赖</li><li>2.编写mybatis应用 </li></ul>
<!-- /wp:list -->

<!-- wp:heading {"level":4} -->
<h4>Step 1 :添加依赖</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>在pom.xml添加以下依赖：</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
<pre class="wp-block-code"><code>&lt;dependency>
  &lt;groupId>org.mybatis.spring.boot&lt;/groupId>
  &lt;artifactId>mybatis-spring-boot-starter&lt;/artifactId>
  &lt;version>2.1.0&lt;/version>
&lt;/dependency></code></pre>
<!-- /wp:code -->

<!-- wp:heading {"level":4} -->
<h4>Step 2：编写代码</h4>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>1.实体类 Book</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
package com.springboot.book.model;

public class Book {
    private int id;

    private String name;

    private String author;

    public Double getPrice() {
        return price;
    }

    public void setPrice(Double price) {
        this.price = price;
    }

    private Double price;

    public String getImage() {
        return image;
    }

    public void setImage(String image) {
        this.image = image;
    }

    public String getDescription() {
        return description;
    }

    public void setDescription(String description) {
        this.description = description;
    }

    private String image;

    private String description;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }



    @Override
    public String toString() {
        return "Book{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", author='" + author + '\'' +
                ", price='" + price + '\'' +
                ", image='" + image + '\'' +
                ", description='" + description + '\'' +
                '}';
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>2.dao：BookDao</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Mapper
public interface BookDao {
    String table_name="book";
    String insert_filed="name,author,price,image,description";
    String select_field = " id, status, " + insert_filed;
//查询全部书籍
    @Select({"select * from",table_name})
    List&lt;Book> selectAll();
//根据name查找id
    @Select({"select id from",table_name,"where name=#{name}"})
    Book selectBookByName(String Name);
//根据id查找全部信息
    @Select({"select * from",table_name,"where id=#{id}"})
    Book selectBookById(@Param("id") int id);
//根据id删除指定书籍
    @Delete({"delete ","from",table_name,"where id=#{id}"})
    void deleteBookById(int id);
//根据指定的书名删除书籍
    @Delete({"delete ","from",table_name,"where name=#{name}"})
    void deleteBookByName(String name);
//添加新的书籍
    @Insert({"insert into",table_name,"(",insert_filed,")","values(#{name},#{author},#{price},#{image},#{description})"})
    void addBook(Book book);
    @Update({"update ", table_name, " set name=#{name},author=#{author},price=#{price},image=#{image},description=#{description} where id=#{id}"})
    void updateBookById(@Param("id") int id,@Param("name") String name,@Param("author") String author,
                        @Param("price") Double price,@Param("image") String image,@Param("description") String description);
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>3.cntroller：BookController</p>
<!-- /wp:paragraph -->

<!-- wp:code -->
```java
@Controller
public class bookController {
    @Autowired
    private BookDao bookDao;
    @RequestMapping("/book")
    public ModelAndView queryAll(){
        List&lt;Book> books =bookDao.selectAll();
        ModelAndView modelAndView =new ModelAndView("booklist");
        modelAndView.addObject("books",books);
        return  modelAndView;
    }


    @GetMapping("/book/del/{id}")
    public String deleteBook(@PathVariable("id") Integer Id,Model model){
       bookDao.deleteBookById(Id);
        List&lt;Book> books =bookDao.selectAll();
        model.addAttribute("books" ,books);
        return "redirect:/book";
    }

    @GetMapping("/book/predit/{id}")
    public String preUpdateBook(@PathVariable("id") Integer Id,Model model){
        Book book =bookDao.selectBookById(Id);
        model.addAttribute("book" ,book);
        System.out.println(book.toString());
        return "addbook";//复用代码
    }

    @PostMapping("/book/editok/{id}")
    public String UpdateBook(@PathVariable("id") Integer Id,
                             @RequestParam("name") String name,
                             @RequestParam("author") String author,
                             @RequestParam("price")String price,
                             @RequestParam("image") String image,
                             @RequestParam("description") String description){
        System.out.println(Id+name+author+price+image+description);
        Double Price = Double.parseDouble(price);
        bookDao.updateBookById(Id,name,author,Price,image,description);
        return "editsuccess";
    }
    @RequestMapping("/book/look/return")
    public String reBack()
    {
        return "redirect:/book";
    }

    @RequestMapping("/book/newbook")
    public String openAddBook(){
        return "addbook";
    }

    @PostMapping("/book/addbook")
    public String addBook(
            @RequestParam("name") String name,
            @RequestParam("author") String author,
            @RequestParam("price") String price,
            @RequestParam("image") String image,
            @RequestParam("description") String description)
    {
        Double Price =Double.parseDouble(price);
        Book book = new Book();
        book.setName(name);
        book.setAuthor(author);
        book.setPrice(Price);
        book.setImage(image);
        book.setDescription(description);
        bookDao.addBook(book);
        return "addsuccess";
    }
    @RequestMapping("/lookbook")
    public String queryAllbook(Model model){
        List&lt;Book> books =bookDao.selectAll();
        model.addAttribute("books" ,books);
        return "lookbook";
    }
}
```
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>以上就是Mybatis两种方式的使用方法。</p>
<!-- /wp:paragraph -->