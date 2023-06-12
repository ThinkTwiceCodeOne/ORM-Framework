# ORM-Framework
A framework for developer

# ORM-Framework
It is an ORM framework

**Note : You should have JAVA_HOME set in your path if you're using Linux or Mac

Using this framwork, developer do not need to write SQL statement. There are some method which developer can use like **save,update,delete,query,view**

I made this for MySQL

There is one example in orm folder named as test.java you can check that.

Let see one by one 

First you need to make a **conf.json** file which should have following this and the file should be in working directory

```
{
"jdbc-driver":"com.mysql.cj.jdbc.Driver",
"connection-url":"jdbc:mysql://localhost:3306/tmdbschool",
"username":"tmwebrockuser",
"password":"tmwebrockuser",
"package":"com.blue.code",
"jar-file":"pojo.jar"
}
```

First you need to run this code in a file like this so it'll create **POJO** classes

Now when you run this it'll create **POJO** files for all the tables that is in you DataBase which you specify in **conf.json** for you in **src** folder and compiled pojo classes in a jar file in **dist** folder. Name of jar file will be taken from conf.json.
```
import java.util.Date;
import java.text.*;
import java.util.*;
import com.blue.code.annotations.*;
import com.blue.code.DataManager.*;
class testpsp
{
public static void main(String gg[])
{
try
{
DataManager dm=DataManager.getDataManager()
}catch(Exception e)
{
System.out.println(e);
}
}
```
Now you need to compile and run

To Compile i use on my machine line this 

```
javac -classpath "/Users/yashmundra/Desktop/del/orm/lib/*:/Users/yashmundra/Desktop/del/orm:." *.java
```

To run

```
java -classpath "/Users/yashmundra/Desktop/del/orm/lib/*:/Users/yashmundra/Desktop/del/orm:." testpsp
```

Now you can edit the java file for different operation
Now suppose you want to **save** a record in Student table so you write 

You've to write this at very first line so you can get DataManager object.
```
DataManager dm=DataManager.getDataManager();
```

```
DataManager dm=DataManager.getDataManager();    
dm.begin();
Student s=new Student();
s.setfirstName("Ishan");
s.setlastName("Kishan");
s.setgender("M");
s.setrollNumber(1009);
s.setcourseCode(2);
s.setaadharCardNumber("98fffff");
String dateString="1997-11-10";
try
{
DateFormat df=new SimpleDateFormat("yyyy-MM-dd");
Date date=df.parse(dateString);
s.setdateOfBirth(date);
}catch(Exception e)
{
System.out.println(e);
}
dm.save(s).fire();
dm.end();
```

To compile and run this code



To Compile i use on my machine line this 

```
javac -classpath "/Users/yashmundra/Desktop/del/orm/lib/*:/Users/yashmundra/Desktop/del/orm/dist:." *.java
```
To run

```
java -classpath "/Users/yashmundra/Desktop/del/orm/lib/*:/Users/yashmundra/Desktop/del/orm/dist:." testpsp
```

Same code for **Update** also just use like this 

```
dm.update(s).fire();
```

Now if you want to **delete** Note that you've to provide primary key while calling delete otherwise it'll throw error
```
dm.begin();
dm.delete(Student.class,1008).fire();
dm.end();
```
  
For **select**
```
dm.begin();
Object o=dm.query(Student.class).fire();
List<Object> list=(List<Object>)o;
for(Object oo:list)
{
Student st=(Student)oo;
System.out.println(st.getrollNumber());
System.out.println(st.getfirstName());
System.out.println(st.getlastName());
System.out.println(st.getaadharCardNumber());
System.out.println(st.getgender());
System.out.println(st.getcourseCode());
System.out.println(st.getdateOfBirth().toString());
System.out.println("-----------------------");
}
dm.end();
```

Now for **Joins** you can make view in DataBase and then call view function and provide name of view
```
dm.begin();
Object o=dm.view(Student.class,"getRecordGreaterThan1001").fire();
List<Object> list=(List<Object>)o;
for(Object oo:list)
{
Student st=(Student)oo;
System.out.println(st.getrollNumber());
System.out.println(st.getfirstName());
System.out.println(st.getlastName());
System.out.println(st.getaadharCardNumber());
System.out.println(st.getgender());
System.out.println(st.getcourseCode());
System.out.println(st.getdateOfBirth().toString());
System.out.println("-----------------------");
}
dm.end();
```

Now I provide some feature you can use with query like **and,or,gt,le,eq,ne**

**and**: And
**or**: Or
**gt**: >
**le**:<
**eq**:==
**ne**:!=
```
dm.begin();
Object o=dm.query(Student.class).where("rollNumber").gt("1001").fire();
System.out.println("done");
List<Object> list=(List<Object>)o;
for(Object oo:list)
{
Student st=(Student)oo;
System.out.println(st.getrollNumber());
System.out.println(st.getfirstName());
System.out.println(st.getlastName());
System.out.println(st.getaadharCardNumber());
System.out.println(st.getgender());
System.out.println(st.getcourseCode());
System.out.println(st.getdateOfBirth().toString());
System.out.println("-----------------------");
}
dm.end();
```

Thank You



