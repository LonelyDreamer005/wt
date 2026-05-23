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

# WEB TECHNOLOGIES – ALL PYQ ANSWERS (10M)

# UNIT–I

# 1. Write HTML and CSS code to create a navigation bar with dropdown menus and floating layout using float, display, and position properties.

## Introduction

A navigation bar is used to provide links for navigating different pages of a website. CSS properties like float, display, and position are used to design dropdown menus.

---

## HTML Code

```html
<!DOCTYPE html>
<html>
<head>
<title>Navigation Bar</title>
<style>
body{
    margin:0;
    font-family:Arial;
}

ul{
    list-style-type:none;
    margin:0;
    padding:0;
    overflow:hidden;
    background-color:#333;
}

li{
    float:left;
}

li a, .dropbtn{
    display:inline-block;
    color:white;
    text-align:center;
    padding:14px 16px;
    text-decoration:none;
}

li a:hover, .dropdown:hover .dropbtn{
    background-color:red;
}

li.dropdown{
    display:inline-block;
}

.dropdown-content{
    display:none;
    position:absolute;
    background-color:#f9f9f9;
    min-width:160px;
}

.dropdown-content a{
    color:black;
    padding:12px 16px;
    text-decoration:none;
    display:block;
}

.dropdown-content a:hover{
    background-color:#ddd;
}

.dropdown:hover .dropdown-content{
    display:block;
}
</style>
</head>
<body>

<ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>

    <li class="dropdown">
        <a href="#" class="dropbtn">Courses</a>

        <div class="dropdown-content">
            <a href="#">Java</a>
            <a href="#">Python</a>
            <a href="#">Web Tech</a>
        </div>
    </li>
</ul>

</body>
</html>
```

---

## Output

A horizontal navigation bar with dropdown menu is displayed.

---

## CSS Properties Used

| Property | Purpose                          |
| -------- | -------------------------------- |
| float    | Align menu items horizontally    |
| display  | Controls visibility/layout       |
| position | Places dropdown correctly        |
| hover    | Displays dropdown on mouse hover |

---

## Conclusion

Thus, a navigation bar with dropdown menus is created using HTML and CSS.

# 2. Explain the Box Model in CSS with labelled diagram.

## Introduction

The CSS Box Model describes how elements are displayed in a rectangular box.

Every HTML element consists of:

1. Content
2. Padding
3. Border
4. Margin

---

## Diagram

```text
 ---------------------------
|          Margin           |
|  -----------------------  |
| |        Border         | |
| |  -------------------  | |
| | |      Padding      | | |
| | |  ---------------  | | |
| | | |    Content    | | | |
| | |  ---------------  | | |
| |  -------------------  | |
|  -----------------------  |
 ---------------------------
```

---

## Components

### 1. Content

Actual text or image.

### 2. Padding

Space between content and border.

### 3. Border

Boundary around padding and content.

### 4. Margin

Space outside the border.

---

## Example

```html
<!DOCTYPE html>
<html>
<head>
<style>
div{
    width:200px;
    padding:20px;
    border:5px solid black;
    margin:30px;
}
</style>
</head>
<body>

<div>
CSS Box Model Example
</div>

</body>
</html>
```

---

## Total Width Formula

```text
Total Width = Content + Padding + Border + Margin
```

---

## Conclusion

Thus, the CSS Box Model controls spacing and layout of web elements.

# UNIT–II

# 3. Explain the role of DOM in JavaScript. Show how to access an HTML element with example.

## Introduction

DOM (Document Object Model) represents an HTML document as a tree structure.

JavaScript uses DOM to:

* Access elements
* Modify content
* Change styles
* Handle events

---

## DOM Structure

```text
Document
   |
 HTML
  / \
Head Body
      |
     h1
```

---

## Example Program

```html
<!DOCTYPE html>
<html>
<body>

<h1 id="msg">Hello</h1>

<button onclick="changeText()">Click</button>

<script>
function changeText()
{
    document.getElementById("msg").innerHTML=
    "Welcome to JavaScript DOM";
}
</script>

</body>
</html>
```

---

## Explanation

### document

Represents entire HTML page.

### getElementById()

Accesses HTML element using id.

### innerHTML

Changes content dynamically.

---

## Applications of DOM

1. Dynamic webpage updates
2. Form validation
3. Event handling
4. Interactive webpages

---

## Conclusion

Thus, DOM helps JavaScript interact with and modify HTML elements dynamically.

# 4. Write JavaScript code to demonstrate keyboard events.

## Introduction

Keyboard events occur when user presses or releases keys.

Common keyboard events:

* onkeydown
* onkeyup
* onkeypress

---

## Program

```html
<!DOCTYPE html>
<html>
<body>

Enter Name:
<input type="text"
       onkeydown="show()"
       onkeyup="release()">

<p id="p1"></p>
<p id="p2"></p>

<script>
function show()
{
    document.getElementById("p1").innerHTML=
    "Key Pressed";
}

function release()
{
    document.getElementById("p2").innerHTML=
    "Key Released";
}
</script>

</body>
</html>
```

---

## Explanation

| Event      | Purpose                        |
| ---------- | ------------------------------ |
| onkeydown  | Triggered when key is pressed  |
| onkeyup    | Triggered when key is released |
| onkeypress | Triggered when key is typed    |

---

## Applications

1. Form validation
2. Search suggestions
3. Gaming controls
4. Shortcut keys

---

## Conclusion

Thus, keyboard events are used to detect user keyboard interactions.

# 5. Write a well-structured XML document to store student information. Also write DTD to validate the XML document.

## XML Document

```xml
<?xml version="1.0"?>

<students>

    <student id="101">
        <name>Rahul</name>
        <branch>CSE</branch>
        <year>3</year>
        <email>rahul@gmail.com</email>
    </student>

    <student id="102">
        <name>Sneha</name>
        <branch>ECE</branch>
        <year>2</year>
        <email>sneha@gmail.com</email>
    </student>

</students>
```

---

# DTD

```xml
<!DOCTYPE students [

<!ELEMENT students (student+)>

<!ELEMENT student (name,branch,year,email)>

<!ATTLIST student id CDATA #REQUIRED>

<!ELEMENT name (#PCDATA)>
<!ELEMENT branch (#PCDATA)>
<!ELEMENT year (#PCDATA)>
<!ELEMENT email (#PCDATA)>

]>
```

---

## Explanation

| Element  | Purpose           |
| -------- | ----------------- |
| students | Root element      |
| student  | Child element     |
| ATTLIST  | Defines attribute |
| PCDATA   | Parsed text data  |

---

## Advantages of XML

1. Stores structured data
2. Platform independent
3. Easy data exchange
4. Self descriptive

---

## Conclusion

Thus, XML stores structured information and DTD validates document structure.

# UNIT–III

# 6. Describe the lifecycle of a servlet with role of each method and simple servlet program.

## Introduction

Servlet lifecycle defines stages through which servlet passes from creation to destruction.

Lifecycle methods:

1. init()
2. service()
3. destroy()

---

## Lifecycle Diagram

```text
Servlet Loaded
      |
    init()
      |
   service()
      |
 service()...
      |
   destroy()
```

---

## Methods

### 1. init()

Called only once.
Used for initialization.

### 2. service()

Handles client requests.

### 3. destroy()

Called before servlet removal.
Used for cleanup.

---

## Servlet Program

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class LifeCycleServlet extends HttpServlet
{
    public void init()
    {
        System.out.println("Servlet Initialized");
    }

    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        PrintWriter w=res.getWriter();

        w.println("Servlet Service Method");
    }

    public void destroy()
    {
        System.out.println("Servlet Destroyed");
    }
}
```

---

## Advantages

1. Efficient request handling
2. Platform independent
3. Faster than CGI
4. Reusable components

---

## Conclusion

Thus, servlet lifecycle methods manage initialization, request processing, and destruction.

# 7. Explain session management techniques in servlets. Implement any one method with code example.

## Introduction

HTTP is stateless. Session management tracks user information across multiple requests.

---

## Session Tracking Techniques

1. Cookies
2. Hidden Form Fields
3. URL Rewriting
4. HttpSession

---

## 1. Cookies

Small text files stored in browser.

## 2. Hidden Fields

Hidden data passed through forms.

## 3. URL Rewriting

Session id added to URL.

## 4. HttpSession

Stores user data on server side.

---

# Example Using HttpSession

## First Servlet

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class FirstServlet extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter w=res.getWriter();

        HttpSession s=req.getSession();

        s.setAttribute("user","Vinay");

        w.println("Session Created");

        w.println("<a href='second'>Next</a>");
    }
}
```

---

## Second Servlet

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class SecondServlet extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        PrintWriter w=res.getWriter();

        HttpSession s=req.getSession(false);

        String u=(String)s.getAttribute("user");

        w.println("Welcome "+u);
    }
}
```

---

## Advantages

1. Maintains user data
2. Supports login systems
3. Used in shopping carts
4. Improves user interaction

---

## Conclusion

Thus, session management maintains client state across requests.

# 8. Develop a servlet that connects to a MySQL/Oracle database using JDBC, fetches employee records, and displays them in table format.

## Introduction

JDBC is used to connect Java applications with databases.

This servlet:

1. Connects to database
2. Retrieves employee records
3. Displays records in HTML table

---

## Database Table

```sql
CREATE TABLE employee(
    id INT PRIMARY KEY,
    name VARCHAR(50),
    department VARCHAR(50),
    salary DOUBLE
);
```

---

## Servlet Program

```java
import java.io.*;
import java.sql.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class EmployeeServlet extends HttpServlet
{
    public void doGet(HttpServletRequest req,
                      HttpServletResponse res)
                      throws IOException
    {
        res.setContentType("text/html");

        PrintWriter w=res.getWriter();

        try
        {
            Class.forName("com.mysql.cj.jdbc.Driver");

            Connection c=DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/test",
            "root",
            "root");

            Statement s=c.createStatement();

            ResultSet r=s.executeQuery(
            "select * from employee");

            w.println("<table border='1'>");
            w.println("<tr>");
            w.println("<th>ID</th>");
            w.println("<th>Name</th>");
            w.println("<th>Department</th>");
            w.println("<th>Salary</th>");
            w.println("</tr>");

            while(r.next())
            {
                w.println("<tr>");
                w.println("<td>"+r.getInt(1)+"</td>");
                w.println("<td>"+r.getString(2)+"</td>");
                w.println("<td>"+r.getString(3)+"</td>");
                w.println("<td>"+r.getDouble(4)+"</td>");
                w.println("</tr>");
            }

            w.println("</table>");

            c.close();
        }

        catch(Exception e)
        {
            w.println(e);
        }
    }
}
```

---

## Steps Involved

1. Load JDBC driver
2. Establish database connection
3. Execute SQL query
4. Fetch records using ResultSet
5. Display data in HTML table
6. Close connection

---

## Conclusion

Thus, servlet successfully connects to database and displays employee records.

# UNIT–IV

# 9. Explain the anatomy of a JSP page with examples. How are declarations, directives, scriptlets and expressions used in JSP?

## Introduction

JSP (Java Server Pages) is used to create dynamic web pages.

Main JSP elements:

1. Directives
2. Declarations
3. Scriptlets
4. Expressions

---

## Anatomy of JSP Page

```text
JSP Page
   |
---------------------------------
| Directives                    |
| Declarations                  |
| Scriptlets                    |
| Expressions                   |
---------------------------------
```

---

# 1. Directives

Used to provide instructions to JSP container.

## Syntax

```jsp
<%@ directive attribute="value" %>
```

## Example

```jsp
<%@ page language="java" %>
```

---

# 2. Declaration

Used to declare variables and methods.

## Syntax

```jsp
<%! code %>
```

## Example

```jsp
<%!
int a=10;
%>
```

---

# 3. Scriptlet

Contains Java code.

## Syntax

```jsp
<% code %>
```

## Example

```jsp
<%
out.println("Welcome");
%>
```

---

# 4. Expression

Displays output directly.

## Syntax

```jsp
<%= expression %>
```

## Example

```jsp
<%= new java.util.Date() %>
```

---

## Complete JSP Program

```jsp
<%@ page language="java" %>

<html>
<body>

<%!
int n=100;
%>

<%
out.println("Value is:");
%>

<%= n %>

</body>
</html>
```

---

## Advantages of JSP

1. Easy dynamic content generation
2. Reusable code
3. Platform independent
4. Supports MVC architecture

---

## Conclusion

Thus, JSP elements are used to create dynamic and interactive web pages.

# 10. Describe the MVC architecture with suitable diagram. How can MVC be implemented using JSP and JDBC in web application?

## Introduction

MVC stands for:

* Model
* View
* Controller

MVC separates application logic from presentation.

---

## MVC Diagram

```text
User
 |
View (JSP)
 |
Controller (Servlet)
 |
Model (JavaBean/JDBC)
 |
Database
```

---

## Components

### 1. Model

Handles business logic and database operations.

Example:

* JavaBean
* JDBC classes

### 2. View

Displays data to user.

Example:

* JSP pages

### 3. Controller

Handles requests and controls flow.

Example:

* Servlet

---

## MVC Working

1. User sends request
2. Servlet receives request
3. Servlet calls model
4. Model interacts with database
5. Data returned to servlet
6. Servlet forwards data to JSP
7. JSP displays output

---

## Example Flow

### Login.jsp

Accepts username/password.

### LoginServlet

Validates credentials.

### UserModel

Connects database using JDBC.

### Success.jsp

Displays success message.

---

## Advantages

1. Better code organization
2. Easy maintenance
3. Reusable components
4. Faster development

---

## Conclusion

Thus, MVC architecture separates business logic, presentation, and control for better web application design.

# UNIT–V

# 11. Explain Object Relational Mapping (ORM) with Hibernate. How does Hibernate solve problems associated with traditional JDBC?

## Introduction

ORM (Object Relational Mapping) maps Java objects with database tables.

Hibernate is an ORM framework used to simplify database operations.

---

## ORM Concept

```text
Java Class  <---->  Database Table
Object      <---->  Row
Attribute   <---->  Column
```

---

## Example

### Java Class

```java
public class Student
{
    int id;
    String name;
}
```

### Database Table

```text
Student
-----------------
| id | name      |
-----------------
```

---

## Problems in Traditional JDBC

1. Large amount of code
2. Manual SQL writing
3. Complex connection handling
4. Resource management difficulty
5. No automatic mapping

---

## How Hibernate Solves JDBC Problems

| JDBC Problem          | Hibernate Solution       |
| --------------------- | ------------------------ |
| Manual SQL            | Automatic query handling |
| Boilerplate code      | Less code                |
| Object-table mismatch | ORM mapping              |
| Connection handling   | Automatic management     |
| Portability issues    | Database independent     |

---

## Hibernate Advantages

1. Simplifies database operations
2. Reduces coding effort
3. Supports caching
4. Provides HQL
5. Better performance

---

## Hibernate Architecture

```text
Java Application
       |
   Hibernate API
       |
 Session Factory
       |
   JDBC Driver
       |
    Database
```

---

## Conclusion

Thus, Hibernate ORM simplifies database programming and overcomes limitations of JDBC.

# 12. Explain the architecture of Hibernate with neat diagram. Describe role of each component.

## Introduction

Hibernate architecture provides communication between Java applications and databases.

---

## Hibernate Architecture Diagram

```text
Java Application
       |
Configuration Object
       |
SessionFactory
       |
Session
       |
Transaction
       |
Query/HQL
       |
Database
```

---

## Components

# 1. Configuration

Loads Hibernate configuration file.

Example:

* hibernate.cfg.xml

---

# 2. SessionFactory

Creates Session objects.
Only one SessionFactory per database.

---

# 3. Session

Used to perform CRUD operations.

Methods:

* save()
* update()
* delete()
* get()

---

# 4. Transaction

Ensures database consistency.

Methods:

* beginTransaction()
* commit()
* rollback()

---

# 5. Query/HQL

Used to execute database queries.

Example:

```java
Query q=session.createQuery("from Student");
```

---

# 6. Persistent Objects

Java objects mapped with database tables.

---

## Advantages

1. Simplifies ORM
2. Reduces SQL coding
3. Database independent
4. Supports caching
5. Better maintainability

---

## Conclusion

Thus, Hibernate architecture simplifies communication between Java applications and relational databases.

# 13. Write a Hibernate program to perform CRUD operations on Student table using annotations.

## Introduction

CRUD operations are:

1. Create
2. Read
3. Update
4. Delete

Hibernate annotations simplify database mapping.

---

# Step 1: Student Class

```java
import javax.persistence.*;

@Entity
@Table(name="student")

public class Student
{
    @Id
    int id;

    String name;
    String branch;

    public Student()
    {
    }

    public Student(int id,String name,String branch)
    {
        this.id=id;
        this.name=name;
        this.branch=branch;
    }

    public int getId()
    {
        return id;
    }

    public void setId(int id)
    {
        this.id=id;
    }

    public String getName()
    {
        return name;
    }

    public void setName(String name)
    {
        this.name=name;
    }

    public String getBranch()
    {
        return branch;
    }

    public void setBranch(String branch)
    {
        this.branch=branch;
    }
}
```

---

# Step 2: hibernate.cfg.xml

```xml
<?xml version="1.0"?>
<!DOCTYPE hibernate-configuration PUBLIC
"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
<session-factory>

<property name="hibernate.connection.driver_class">
com.mysql.cj.jdbc.Driver
</property>

<property name="hibernate.connection.url">
jdbc:mysql://localhost:3306/test
</property>

<property name="hibernate.connection.username">
root
</property>

<property name="hibernate.connection.password">
root
</property>

<property name="hibernate.dialect">
org.hibernate.dialect.MySQLDialect
</property>

<mapping class="Student"/>

</session-factory>
</hibernate-configuration>
```

---

# Step 3: Main Program

```java
import org.hibernate.*;
import org.hibernate.cfg.Configuration;

public class MainClass
{
    public static void main(String args[])
    {
        Configuration c=new Configuration();

        c.configure();

        SessionFactory sf=c.buildSessionFactory();

        Session s=sf.openSession();

        Transaction t=s.beginTransaction();

        // CREATE
        Student st=new Student(101,"Rahul","CSE");

        s.save(st);

        // READ
        Student x=s.get(Student.class,101);

        System.out.println(x.getName());

        // UPDATE
        x.setBranch("ECE");

        s.update(x);

        // DELETE
        s.delete(x);

        t.commit();

        s.close();
    }
}
```

---

## Steps Involved

1. Create persistent class
2. Configure Hibernate
3. Create SessionFactory
4. Open Session
5. Begin Transaction
6. Perform CRUD operations
7. Commit transaction
8. Close session

---

## Advantages

1. Less coding
2. Automatic table mapping
3. Simplified CRUD operations
4. Better maintainability

---

## Conclusion

Thus, Hibernate annotations simplify CRUD operations on database tables.

