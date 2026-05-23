# Web Technologies — All Code Examples (Units III, IV, V)

---

# UNIT–III: SERVLETS

# 1. Servlet Life Cycle Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class DemoServlet extends HttpServlet
{
    String msg;

    public void init()
    {
        msg = "Welcome to Servlets";
    }

    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter out = res.getWriter();

        out.println("<h1>" + msg + "</h1>");
    }

    public void destroy()
    {
        System.out.println("Servlet Destroyed");
    }
}
```

---

# 2. Servlet API Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class UserServlet extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        String b = req.getParameter("name");

        res.setContentType("text/html");

        PrintWriter c = res.getWriter();

        c.println("<h1>Hello " + b + "</h1>");
    }
}
```

---

# 3. HTML Form Example

```html
<html>
<body>

<form action="UserServlet">

Name:
<input type="text" name="name">

<input type="submit" value="Submit">

</form>

</body>
</html>
```

---

# 4. Reading Servlet Parameters

```java
import java.io.*;
import java.util.Arrays;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class FormServlet extends HttpServlet
{
    public void doPost(HttpServletRequest req,
                       HttpServletResponse res)
                       throws IOException
    {
        String b = req.getParameter("username");

        String[] c =
        req.getParameterValues("hobbies");

        res.setContentType("text/html");

        PrintWriter e = res.getWriter();

        e.println("<h2>User: " + b + "</h2>");

        if(c != null)
        {
            e.println("Hobbies: "
            + Arrays.toString(c));
        }
    }
}
```

---

# 5. Initialization Parameter Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class DemoServlet extends HttpServlet
{
    String b;

    public void init() throws ServletException
    {
        ServletConfig c = getServletConfig();

        b = c.getInitParameter("username");
    }

    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter e = res.getWriter();

        e.println("<h2>User Name: "
                  + b + "</h2>");
    }
}
```

---

# 6. web.xml Example

```xml
<web-app>

<servlet>

    <servlet-name>DemoServlet</servlet-name>

    <servlet-class>DemoServlet</servlet-class>

    <init-param>

        <param-name>username</param-name>

        <param-value>admin</param-value>

    </init-param>

</servlet>

</web-app>
```

---

# 7. HTTP Request & Response Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class DemoServlet extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        String b = req.getParameter("username");

        String c =
        req.getHeader("User-Agent");

        res.setContentType("text/html");

        PrintWriter e = res.getWriter();

        e.println("<h2>Welcome "
                  + b + "</h2>");

        e.println("<h3>Browser: "
                  + c + "</h3>");
    }
}
```

---

# 8. Simple Servlet Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class HelloServlet
extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter b =
        res.getWriter();

        b.println("<h1>Hello World</h1>");
    }
}
```

---

# 9. Hidden Field Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class FirstServlet
extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        String b = req.getParameter("user");

        res.setContentType("text/html");

        PrintWriter c =
        res.getWriter();

        c.println("<form action='SecondServlet' method='post'>");

        c.println("<input type='hidden' name='username' value='"
                  + b + "'>");

        c.println("<input type='submit' value='Next'>");

        c.println("</form>");
    }
}
```

---

# 10. Cookie Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class CookieServlet
extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        Cookie b =
        new Cookie("username", "Vinay");

        res.addCookie(b);

        res.setContentType("text/html");

        PrintWriter c =
        res.getWriter();

        c.println("Cookie Added");
    }
}
```

---

# 11. Session Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class SessionServlet
extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        HttpSession b =
        req.getSession();

        b.setAttribute("user", "Vinay");

        res.setContentType("text/html");

        PrintWriter c =
        res.getWriter();

        c.println("Session Created");
    }
}
```

---

# 12. Request Dispatcher Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class FirstServlet
extends HttpServlet
{
    public void doPost(HttpServletRequest req,
                       HttpServletResponse res)
                       throws IOException,
                       ServletException
    {
        String b =
        req.getParameter("username");

        req.setAttribute("user", b);

        RequestDispatcher c =
        req.getRequestDispatcher("SecondServlet");

        c.forward(req, res);
    }
}
```

---

# 13. JDBC with Servlet Example

```java
import java.io.*;
import java.sql.*;

import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class JdbcServlet
extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter b =
        res.getWriter();

        try
        {
            Class.forName(
            "com.mysql.cj.jdbc.Driver");

            Connection c =
            DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/test",
            "root",
            "password");

            String q =
            "SELECT * FROM users";

            PreparedStatement d =
            c.prepareStatement(q);

            ResultSet e =
            d.executeQuery();

            while(e.next())
            {
                b.println(
                e.getInt("id")
                + " "
                + e.getString("name")
                + "<br>");
            }

            e.close();
            d.close();
            c.close();
        }
        catch(Exception x)
        {
            b.println(x);
        }
    }
}
```

---

# UNIT–IV: JSP

# 14. Simple JSP Example

```jsp
<%@ page language="java"
         contentType="text/html" %>

<html>

<body>

<h2>Welcome to JSP</h2>

<%
String b = "Vinay";
%>

<h3>Hello <%= b %></h3>

</body>

</html>
```

---

# 15. JSP Declaration Example

```jsp
<%!
int b = 100;

public int add(int x, int y)
{
    return x + y;
}
%>
```

---

# 16. JSP Expression Example

```jsp
<%= 10 + 20 %>
```

---

# 17. JSP Implicit Object Example

```jsp
<%@ page language="java"
         contentType="text/html" %>

<html>

<body>

<%
String b =
request.getParameter("name");

session.setAttribute(
"user",
b);
%>

<h2>
Welcome
<%= session.getAttribute("user") %>
</h2>

</body>

</html>
```

---

# 18. JavaBean Example

```java
package demo;

public class UserBean
{
    private String name;

    public UserBean()
    {

    }

    public void setName(String b)
    {
        name = b;
    }

    public String getName()
    {
        return name;
    }
}
```

---

# 19. JSP Bean Usage Example

```jsp
<jsp:useBean
id="obj"
class="demo.UserBean" />

<jsp:setProperty
name="obj"
property="name"
param="userName" />

<html>

<body>

<h2>
Welcome
<jsp:getProperty
name="obj"
property="name" />
</h2>

</body>

</html>
```

---

# 20. JSP Cookie Example

```jsp
<%@ page import="jakarta.servlet.http.Cookie" %>

<html>

<body>

<%
Cookie b =
new Cookie("username",
           "Vinay");

response.addCookie(b);

out.println("Cookie Created");
%>

</body>

</html>
```

---

# 21. JSP Session Example

```jsp
<html>

<body>

<%
session.setAttribute(
"user",
"Vinay");

String b =
(String)session.getAttribute(
"user");
%>

<h2>
Welcome <%= b %>
</h2>

</body>

</html>
```

---

# 22. JDBC with JSP Example

```jsp
<%@ page import="java.sql.*" %>

<html>

<body>

<%
try
{
    Class.forName(
    "com.mysql.cj.jdbc.Driver");

    Connection b =
    DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/test",
    "root",
    "password");

    String q =
    "SELECT * FROM users";

    PreparedStatement c =
    b.prepareStatement(q);

    ResultSet d =
    c.executeQuery();

    while(d.next())
    {
        out.println(
        d.getInt("id")
        + " "
        + d.getString("name")
        + "<br>");
    }

    d.close();
    c.close();
    b.close();
}
catch(Exception e)
{
    out.println(e);
}
%>

</body>

</html>
```

---

# 23. MVC Servlet Example

```java
import java.io.*;
import jakarta.servlet.*;
import jakarta.servlet.http.*;

public class LoginServlet
extends HttpServlet
{
    public void doPost(HttpServletRequest req,
                       HttpServletResponse res)
                       throws IOException,
                       ServletException
    {
        String b =
        req.getParameter("user");

        UserBean c =
        new UserBean();

        c.setUser(b);

        req.setAttribute("data", c);

        RequestDispatcher d =
        req.getRequestDispatcher(
        "home.jsp");

        d.forward(req, res);
    }
}
```

---

# UNIT–V: HIBERNATE

# 24. Hibernate POJO Class

```java
public class Student
{
    private int id;
    private String name;

    public Student()
    {

    }

    public int getId()
    {
        return id;
    }

    public void setId(int b)
    {
        id = b;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String c)
    {
        name = c;
    }
}
```

---

# 25. Hibernate Configuration File

```xml
<hibernate-configuration>

<session-factory>

<property name=
"hibernate.connection.driver_class">

com.mysql.cj.jdbc.Driver

</property>

<property name=
"hibernate.connection.url">

jdbc:mysql://localhost:3306/test

</property>

<property name=
"hibernate.connection.username">

root

</property>

<property name=
"hibernate.connection.password">

password

</property>

<property name=
"hibernate.dialect">

org.hibernate.dialect.MySQLDialect

</property>

<mapping resource=
"student.hbm.xml"/>

</session-factory>

</hibernate-configuration>
```

---

# 26. Hibernate Mapping File

```xml
<hibernate-mapping>

<class name="Student"
       table="student">

<id name="id"
    column="id">

<generator class="assigned"/>

</id>

<property name="name"
          column="name"/>

</class>

</hibernate-mapping>
```

---

# 27. Hibernate Session Example

```java
Configuration b =
new Configuration();

b.configure();

SessionFactory c =
b.buildSessionFactory();

Session d =
c.openSession();

Transaction e =
d.beginTransaction();

Student f =
new Student();

f.setId(1);
f.setName("Vinay");

d.save(f);

e.commit();

d.close();
```

---

# 28. Hibernate Annotation Example

```java
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.Id;
import jakarta.persistence.Column;

@Entity

@Table(name="student")

public class Student
{
    @Id
    private int id;

    @Column(name="name")
    private String name;

    public Student()
    {

    }

    public int getId()
    {
        return id;
    }

    public void setId(int b)
    {
        id = b;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String c)
    {
        name = c;
    }
}
```

---

# 29. Hibernate HQL Example

```java
Configuration b =
new Configuration();

b.configure();

SessionFactory c =
b.buildSessionFactory();

Session d =
c.openSession();

Transaction e =
d.beginTransaction();

Query q =
d.createQuery(
"from Student");

List list =
q.list();

Iterator i =
list.iterator();

while(i.hasNext())
{
    Student f =
    (Student)i.next();

    System.out.println(
    f.getId()
    + " "
    + f.getName());
}

e.commit();

d.close();
```

---

# 30. HQL Update Example

```java
Query q =
session.createQuery(
"update Student set name='Rahul' where id=1");

int x =
q.executeUpdate();
```

---

# 31. HQL Delete Example

```java
Query q =
session.createQuery(
"delete from Student where id=1");

int x =
q.executeUpdate();
```

---

# End of All Important Code Examples
