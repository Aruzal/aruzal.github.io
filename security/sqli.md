# SQL Injection (SQLi)

### What is SQLi?
SQLi is a type of injection attack that is targetted towards exploiting databases and their implementations. It occurs when a user inputs a valid SQL query into the form that escapes it's previous statement, thus allowing it to execute. SQLi allows attackers to steal credentials, bypass authentication and even insert their own entries into a databse.

### Detecting SQLi
For SQLi to work in the first place the users input need to escape its current SQL query. To understand what this means lets look at a simple SQL statement that selects the username and password from the users table and then compares them the user input {username} and {password} to check if they match.

`"SELECT username, password FROM users WHERE username='{username}' AND password='{password}'"`

As an example exploit we use `admin` for the username and then `' OR '1'='1`, If we look at what this looks like when it's inserted into the SQL statement above we notice that it close the ' and allows the rest of the statement to complete, returning a match because the password will always match, '1'='1' is evaluates to true.

`"SELECT username, password FROM users WHERE username='admin' AND password='' OR '1'='1'"`

### Preventing SQLi
Since SQLi can be quite impactful it is important to know how to prevent it.

##### SQL Prepared Statements
The cause of SQLi like many other vulnerabilities is due to mixing control data with actual data. This causes the data to be confused with the contrpl data when executing the SQL statement. SQL prepared statements help to separate the control data and the data by first providing a schema of what the SQL statement will look like and then inserted the values for the data. An example of what a prepared statement looks like is below, the '?' is used to represent that data will be input into the statement at that location.

`("SELECT username, password FROM users WHERE username= ? AND password= ?", "admin", "' OR '1'='1")`

Since the SQL statement above is a prepared statement, even though the same values are input by the user, it will no longer execute and result in a match.

##### DBMS's
A DBMS is a DataBase Management System which provides an interface between the developer and the database itself. The DBMS is responsible for actually querying the database and will use prepared statements as well as other techniques to prevent SQLi. Some databases also use other alternatives to SQL such as XML or json.

##### WAFS or Filtering

Sqlite3
[MySQL Cheat Sheet](pentestmonkey.net/cheat-sheet/sql-injection/mysql-sql-injection-cheat-sheet)

### Tools
[SQLMap](https://github.com/sqlmapproject/sqlmap)