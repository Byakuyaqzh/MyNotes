#### Driver

使用接口连接数据库

```java
//  1  读取配置文件的基本信息
//                    ↓ 这个是类名
InputStream is = ConnectionTest.class.getClassLoader().getResourceAsStream("jdbc.properties");
Properties pros = new Properties();
pros.load(is);
String user = pros.getProperty("user");
String password = pros.getProperty("password");
String url = pros.getProperty("url");
String driverClass = pros.getProperty("driverClass");

//  2  加载驱动
Class.forName(driverClass);

//  3  获取连接
Conneciton conn = DriverManager.getConnection(url, user, password);

//  4  定义SQL语句
String sql = "update account set password = 123456 where id = root";

//  5  获取执行SQL对象
Statment stmt = conn.createStatement();

//  6  执行SQL
//  返回受到影响的行数，这里的结果是1
int count = stmt.executeUpdate(sql);

//  7  释放资源
stmt.close();
conn.close();
```

```properties
#  将数据库连接需要的四个基本信息声明在配置文件中
#  文件名为 jdbc.properties
name=root
password=123456
#  jdbc:mysql://ip地址:端口号/数据库名
url=jdbc:mysql://localhost:3306/test
driverClass=com.mysql.jdbc.Driver
```



##### DriverManager

驱动管理类，作用：1、注册驱动，2、获取驱动连接

是一个工具类，其中包含了大量静态方法，可以直接用类型.方法名调用。



##### Connection

接口，作用：1、获取执行SQL对象，2、事务管理

```java
//  事务管理
//  数据库中的事务流程：开启事务 - 提交事务 - 回滚事务
try{
    //  开启事务
    conn.setAutoCommit(false);
    
    /*
      --  事务内容  --
    */
    
    //  提交事务
    conn.commit();
} catch(Exception e) {
    //  回滚事务
    conn.rollback();
    throwables.printStackTrace();
}
```



##### Statement

提供不同的方法，执行不同的SQL语句

```java
//  执行DML、DDL语句
int count = stmt.executeUpdate(sql);

//  执行DQL语句，rs返回收集的数据
ResultSet rs = stmt.executeQuery(sql);
while(rs.next()){
    //  括号内的数字是columnIndex，列数，也可以直接写数据库中
    //  数据库中，第一列是id，第二列是name
    int id = rs.getInt(1);
    String name = rs.getString("name");
}
```





##### PreparedStatement

表示预编译SQL语句的对象，用于预防SQL注入

```java
/*
	获取链接
*/
String name;
String password;

//  4  定义SQL语句
String sql = "select * from user where username = ? and password = ?";

//  5  获取pstmt对象
PreparedStatment pstmt = conn.preparedStatment(sql);

//  设置 ？ 的值
pstmt.setString(1, name);
pstmt.setString(2, password);

//  6  执行SQL
//  返回受到影响的行数，这里的结果是1
int count = stmt.executeUpdate();

//  7  释放资源
stmt.close();
conn.close();
```







##### 数据库连接池，Druid

- 数据库连接池是一个容器，负责分配、管理数据库连接
- 允许程序重复使用现有的数据库连接，而不是每次新建
- 施放空闲时间超过最大空闲时间的数据库连接，避免存在数据库连接未被释放
- 优点：
  - 资源复用
  - 提升系统响应速度
  - 避免数据库连接遗漏

标准接口：DataSource

```java
// 1. 导入durid的jar包
// 2. 定义配置文件，包含
//      driverClass，url，name，password
//      初始连接数量 initialSize，最大连接数 maxActive，最大等待时间 maxWait
// 3. 加载配置文件
Properties prop = new Properties;
prop.load(new FileInputStream("src/druid.properties"));
// 4. 获取连接池对象
DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
// 5. 获取数据库连接
Connection conn dataSource.getConnection();
```





#### 参考示例

```java
public void selectAll(){
    //  1. 获取Connection对象
    //  使用数据库连接池
    Properties prop = new Properties;
    prop.load(new FileInputStream("src/druid.properties"));
    DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
    Connection conn dataSource.getConnection();
    
    //  2. 定义SQL语句
    String sql = "select * from table";
    
    //  3. 获取pstmt对象
    PreparedStatement pstmt = conn.prepareStatement(sql);
    
    //  4. 设置参数
    
    //  5. 执行SQL
    ResultSet rs = pstmt.executeQuery();
    
    //  6. 处理结果
    while(rs.next()){
        int id = rs.get("id");
        String name = rs.get("name");
        //  ...
    }
    
    //  7. 释放资源
    rs.close();
    pstmt.close();
    conn.close();
}
```



--





