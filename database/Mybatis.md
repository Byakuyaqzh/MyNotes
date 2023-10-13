



#### 文件结构

```
main
 |- java
     |- com.example
     	 |- mapper
     	      |- UserMapper.java

 |- resource
 	|-  com.example
 		 |- mapper
 		 	  |- UserMapper.xml
  
```

在mapper下的UserMapper接口，声明方法名及传递参数，在resource下的相同目录下的UserMapper.xml定义具体的sql语句



##### UserMapper.java

```java
@Mapper
public interface UserMapper {
	//  删除单个id
    public void delete(Integer id);

    //  删除多个id
    public void deletes(ArrayList<Integer> ids);
}
```

##### UserMapper.xml

```xml
<!-- 文件头 -->
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">

<!--具体的实现-->
<!--标签mapper中，在namespace上写明UserMapper.java在包中的路径-->
<mapper namespace="com.example.mapper.UserMapper">
    <!--id为对应的方法名-->
    <delete id="delete">
        delete from emp.user where id = #{id}
    </delete>

    <delete id="deletes">
        delete from emp.user where id in
        <foreach collection="ids" item="id" separator="," open="(" close=")" >
             #{id}
        </foreach>>

    </delete>
</mapper>
```





#### 动态SQL

##### if

```xml
<select id = "select">
    select * from table
    <!--根据子标签的内容动态生成语句，并能自动去除多余的and/or-->
    <where>
        <!--test内编写判断语句-->
        <if test = "name != null">
            <!--拼接，%是占位符-->
            name like concat('%', #{name}, '%')
        </if>
        <if test = "age != null">
            and age > #{age}
        </if>
        <if test = "begin != null and end != null">
        	and entrydate between #{begin} and #{end}
        </if>
    </where>
    <!--根据update_time倒序排序-->
	order by update_time desc
</select>



```



##### foreach

```xml
<delete id="deletes">
    delete from emp.user where id in
    <!--  结果：(id1, id2, id3)  -->
    <!-- collection 是集合 -->
    <!-- item 是其中的一个元素 -->
    <!-- separator 是分隔符 -->
    <!-- open 是开头 -->
    <!-- close 是最后 -->
    <foreach collection="ids" item="id" separator="," open="(" close=")" >
        #{id}
    </foreach>>

</delete>
```



##### sql/include

将相同的代码抽象出去，在需要使用时使用include引用

```xml
<!-- 为避免使用 select *，将各个字段封装出来 -->
<sql id = "commonCode">
	select id, name, age 
    from table
</sql>
```

```xml
<delete id="delete">
    <include refid = "commonCode" />
    <where>
    	<!-- ... -->
    </where>
</delete>
```

















